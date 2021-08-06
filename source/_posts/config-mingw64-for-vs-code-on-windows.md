---
title: 在 Windows 上配置 VS Code 与 C++ 开发环境
date: 2021-08-06 19:59:52
tags: 教程
---

## 背景知识

Visual Studio Code 与 Visual Studio、IDEA 等有着本质上的不同：前者为文本编辑器，而后者为 IDE（集成开发环境）。IDE 以语言为中心，为语言打造最贴身的开发工具，而编辑器只负责编辑，其他的功能都得由插件实现。但是编辑器相对于 IDE 来说

1. 更加轻量、快速，尤其是存储空间上二者甚至能差好几个数量级。
2. 跨语言开发时能最大限度地保留写代码的习惯。
3. 底层原理对使用者更透明，有利于新手了解编译等过程。

## 准备工作

1. 安装 [Visual Studio Code](https://code.visualstudio.com/download)

2. 转到 VS Code 侧边栏中 Extension 这个 tab，搜索安装插件[适用于 VS Code 的中文（简体）语言包](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans)

3. 安装插件 [C/C++ extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools).

4. 下载编译好的 [Mingw-w64](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/) 工具链（包含了最新的 GCC C++ 编译器）。

   下载方式：[SourceForge 官方](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/sjlj/x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z) / [百度网盘（密码：mysd）](https://pan.baidu.com/s/1nYG0T4J--V0pDShcDt_6WQ)

## 配置 MingW

1. 用 [7-Zip](https://www.7-zip.org/) 或其他解压软件打开下载的 [Mingw-w64](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/) 工具链，将 mingw-w64 复制到 C 盘根目录下。
2. 按下组合键 Win+R，输入 `sysdm.cpl`，选择高级 - 环境变量，在系统变量下找到 `Path` 这一行双击。
3. 点击新建，输入 `C:\mingw64\bin` 。然后一路确认。
4. 按下组合键 Win+R，输入 `cmd`，在命令行中输入 `gcc --version`  并回车，查看是否成功显示 gcc 版本。

**Side note: 为什么要这样做？**

刚才你将 mingw64 的可执行文件（binary）目录添加到了环境变量 `PATH` 中。在cmd等终端下运行可执行文件时，如果在当前目录找不到这个名称的文件，命令行就会自动从上到下在 `PATH` 环境变量中的目录寻找。这样，即使编辑器不知道我们把 mingw 放在哪里，也可以正常运行编译命令。

## 配置编译生成

1. 打开 VS Code，点击`打开文件夹`，并选择一个你想存放代码的文件夹。

2. 新建一个文件，命名为 `helloworld.cpp`，并输入如下代码：

   ```c++
   #include <iostream>
   #include <vector>
   #include <string>
   
   using namespace std;
   
   int main()
   {
       vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};
   
       for (const string& word : msg)
       {
           cout << word << " ";
       }
       cout << endl;
   }
   ```

   按下 Ctrl+S 保存代码。

3. 在顶部菜单栏，选择**终端** > **配置默认生成任务** > **g++.exe 生成活动文件**

4. 此时按下 Ctrl+Shift+B 或者点选 **终端** > **运行生成任务**，您可以看到 **终端** 选项卡弹出，并自动执行编译命令。

5. 用 + 按钮新建一个终端窗口并运行 `.\helloworld.exe`，此时您可以看到 Hello World 信息。

## 配置调试

1. 在顶部菜单栏，选择**运行** > **添加配置...** > **C++ (GDB/LLDB)** > **g++.exe 生成和调试活动文件**.

2. 按下 `F5` 或者点选 **运行** > **开始调试**.

3. 鼠标移动到行数指示器左侧，您可以看到红色圆点，单击后即为在该行下断点。调试时程序会运行到这一行前并停下。

   请在第 9 行下断点。

4. 重新开始调试，这时候您可以看到程序在第 9 行停下，请自行探索窗口上部出现的调试工具！

## 在此之后......

- 查阅 [Visual Studio Code 官方文档](https://code.visualstudio.com/docs)，建议阅读 [User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) 部分以及 User Guide 这一章。学习编辑技巧，大幅提高效率。
- 探索 VS Code 的各种配置选项和插件。出现问题？重装 VS Code 即可（x
- 寻找最适合自己的编辑器，尝试使用 [Vim](https://www.vim.org/)（[Neovim](https://neovim.io/)）、[Emacs](https://www.gnu.org/software/emacs/)。

