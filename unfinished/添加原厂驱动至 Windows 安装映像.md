你购买了一台崭新的 Windows 笔记本电脑，拿回来一看，预装了一大堆软件！虽然大部分都可以卸载，但是还是非常烦人。过了一段时间你因为各种原因需要重装系统，摆在你面前的有两个选择：

- 设置 - 更新与安全 - 重置此电脑：我发现重置时新增了一个选项叫“云下载”，可以下载原厂镜像重新安装，但是同时就有很烦人的预装软件。
- 下载刻录原版 Windows ISO 镜像安装：所有驱动都会丢失，Windows Update 一般下不全。如果装上什么驱动大师之类的那还不如上面那个选项。

所幸可以备份目前运行的 Windows 系统上的驱动，甚至可以直接嵌入 ISO 镜像中，安装时不再需要额外下载任何驱动。

踩了一天的坑，现在记录一下。如果没有特别指出，本文所有代码都应该输入到管理员权限下的 CMD 中。

## 备份

```
Dism /Online /Export-Driver /Destination:C:\DriversBak
```

备份出的驱动文件位于 `C:\DriversBak`

## 添加驱动至 install.wim

1. 挂载你下载好的原版 ISO 文件。
2. 复制到 `C:\iso` 目录下
3. `Dism /Get-WimInfo /WimFile:C:\iso\sources\install.wim` 查看你要修改的 Index
4. `Dism /Mount-Image /ImageFile:C:\iso\sources\install.wim /Index:1 /MountDir:C:\wimmnt` 这里根据实际情况修改 `/Index:` 后的数字，最大可能需要 15 GB 的空间
5. `Dism /Image:C:\wimmnt /Add-Driver /Driver:C:\DriversBak /Recurse`
6. `Dism /Unmount-Image /MountDir:C:\wimmnt /Commit`

如果你只是想创建 USB 安装盘，只需把 `C:\iso` 目录下的所有文件复制到 FAT32 格式的 U 盘中即可，如果 `install.wim` 超过 4 GB 则需要文件分片：

1. 格式化 U 盘为 FAT32
2. `robocopy C:/iso G: /s /max:3800000000` G 为 U 盘盘符，根据实际情况更改
3. `Dism /Split-Image /ImageFile:C:\iso\sources\install.wim /SWMFile:G:\sources\install.swm /FileSize:3800`

## 创建 ISO 文件

下载 CDImage 程序，并在 `cdimage.exe` 同目录下新建 `CreateISO.bat` 内容为

```
SET ISOPATH=D:\Driver_SW_DVD9_WIN_ENT_LTSC_2021_64BIT_ChnSimp_MLF_X22-84402
SET DVDLABEL=LENOVO-PRO14-LTSC-2021-ZH-CN
SET DVDISO=LTSC-2021-EN-US.iso
bin\cdimage.exe -bootdata:2#p0,e,b"%ISOPATH%\boot\etfsboot.com"#pEF,e,b"%ISOPATH%\efi\Microsoft\boot\efisys.bin" -o -h -m -u2 -udfver102 -l%DVDLABEL% %ISOPATH% %DVDISO%
pause
```

请自行更改 `ISOPATH`（要导出为 ISO 的文件夹） `DVDLABEL`（光盘名称） `DVDISO`（输出文件名）

然后双击运行即可。

参考：

- https://www.tenforums.com/tutorials/72031-create-windows-10-iso-image-existing-installation.html
- https://www.tenforums.com/tutorials/95008-dism-add-remove-drivers-offline-image.html
- https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/add-and-remove-drivers-to-an-offline-windows-image?view=windows-11
- https://www.tenforums.com/tutorials/2570-esd-iso-create-bootable-iso-windows-10-esd-file.html
- https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/oscdimg-command-line-options?view=windows-11
- https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/install-windows-from-a-usb-flash-drive?view=windows-11#if-your-windows-image-is-larger-than-4gb
