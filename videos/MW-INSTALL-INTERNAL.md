# 云固件内置模式安装

云固件支持多种方式的安装，包括内置模式安装、外置引导模式安装、移动模式安装以及混合模式安装，最后还会有固化到计算机BIOS里面的发行方式。

本视频讲解内置模式安装，也就是将云固件的主程序安装到计算机内置的硬盘里。

## 前提与准备

- 2010年以后生产的个人计算机一台
- 预装Windows PE的U盘一个
- 云固件安装包
- 云固件虚拟磁盘镜像文件

云固件安装包及虚拟磁盘镜像文件，大家可以查看视频下方评论区，我会把下载页面的链接贴出来。

## 开始安装

连接计算机键盘、鼠标、显示器及电源，使用U盘启动计算机，进入Windows PE系统。
我使用的启动U盘是特殊定制的，用云固件自身来启动，支持多个ISO光盘镜像直接启动。在后续的外置引导模式和移动模式安装视频里面也会讲解。

### 1.硬盘分区及格式化

云固件的使用需要至少2个分区，分别为云固件程序所在的EFI系统分区（ESP）、虚拟磁盘存储分区（VDs）。用户也可根据多系统共享数据需要创建数据分区（DATA）。

创建EFI系统分区，分区大小为100M，卷标为ESP，分区格式为FAT（FAT16）。ESP分区不建议超过100M，过大空间没有利用价值。

创建虚拟磁盘存储分区，分区大小为物理硬盘剩余空间，卷标为VDs，分区格式为NTFS（不支持压缩、不支持加密）。

可选创建数据分区，分区大小由用户自定义，卷标为DATA，分区格式建议为exFAT，这样可方便Windows及Linux读写。

### 2.复制云固件主程序

将下载的云固件程序解压缩，得到EFI文件夹，将此文件夹复制到ESP分区。
将vd.config文件复制到VDs分区根目录下。

### 3.复制虚拟磁盘镜像

将下载的云固件虚拟磁盘镜像文件夹复制到VDs分区根目录下。

修改vd.config配置文件，将虚拟磁盘镜像加入引导配置菜单。如menu.config配置文件已经引入，可不修改。

镜像文件夹内的文件如果是压缩的7z文件，需要解压缩到当前文件夹。

### 4.（可选）添加启动项

曾经安装过系统的计算机，Windows或者Linux会在BIOS里写入引导菜单选项，绝大多数时候不会影响云固件的启动，大家可以不用做这一步。云固件会被BIOS识别为“UEFI OS”这个启动选项，然后也可以直接启动。

我们用Bootice查看和修改一下，把“UEFI OS”名称修改“AINUC Multiware”，调整为第一个顺序位，保存即可。

## 重新启动

安全退出云固件及虚拟磁盘镜像存储的介质，拔下存储介质。在Windows PE下选择重新启动。
系统进入重新启动后，拔下Windows PE启动U盘。
重新启动后，计算机应该会自动进入云固件的启动界面，用户选择需要启动的虚拟磁盘图标即可启动对应的虚拟磁盘系统。

## 结语

云固件内置模式的安装是非常简单和快速的，欢迎大家测试和体验。
云固件的更多信息大家可以使用“云固件”或者“AINUC云固件”作为关键词搜索，各大平台一般都会有对应的结果，首选知乎、B站和百度。
谢谢大家收看，再见！