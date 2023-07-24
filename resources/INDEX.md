# 云固件镜像仓库

云固件官方提供了常见系统及常见机型的[虚拟磁盘镜像文件仓库](https://github.com/ainuc99/DiskHub)，仓库内保存有镜像文件的说明及配套文件，镜像文件及镜像文件压缩文件可参考下载地址，通常使用百度网盘提供。

## 默认格式

云固件通常使用VHDx作为标准的镜像格式，云固件镜像既可以支持物理机启动也可以支持虚拟机启动。仓库内镜像文件，统一使用VHDx动态格式，容量为256G，区块大小为默认值；分区使用GPT格式。

## 分层规范

云固件支持差分格式的磁盘镜像格式，为了让制作的镜像文件能够得到最大化的利用，云固件提出了如下分层规范：

1. 分层按照L0-L9来定义；
1. 高层级镜像原则上要求包含低层级全部镜像内容；
1. 除L0级别外，每个层级均可以生成差分级别；
1. 同层级的差分镜像使用层级加两位数的顺序号来区分，如301，305，501，511等；

## 分层约定

根据分层规范要求，约定各层级的具体要求。

### L0层

    L0层为待安装操作系统层，仅对Windows系列有效。
    使用GPT格式进行磁盘分区；
    可通过dism命令将wim文件展开到系统分区，使用bcdboot添加引导文件；亦可通过Windows安装程序在虚拟机内进行部署至待重启为止。

### L1层

    本层为基本安装层。
    Windows系统或者Linux执行基本安装过程，安装期间断开网络，防止自动更新；
    用户名me，无密码或者有密码统一为“I@mtheNo.1”，不包含引号部分；

### L2层

    L2层为完善驱动层。
    本层在L1的基础上，安装完善宿主机需要的全部驱动程序，包括自动更新驱动的服务程序，如Thinkpad的System Updater、NUC上的Intel® Driver & Support Assistant (Intel® DSA)等。
    对于DIY主机，由于独立显卡的差异，本层会分化出一个L2.5层，满足针对N卡、A卡、I卡（Intel Arc系列独立显卡）一次性部署需求。
    针对Linux系统，也需更新包括集成显卡、独立显卡、网卡等驱动程序。

### L3层

    L3层为系统更新层。
    本层执行系统非跨版本更新，更新时限为制作时。如Windows 10 1809，不可跨版本升级到1903版本。

### L4层

    L4层为系统激活层。
    用户根据自身需要使用企业内部KMS服务器激活Windows系统。
    默认激活服务器为KMS.local。
    用户也可以在本层使用sysprep更新用户设置信息。

### L5-L9层

    L5到L9层为用户自定义层。
    用户可以在本层安装用户所需的应用程序或者数据文件，比如Microsoft Office、电子邮件客户端、开发工具等。
    用户也可以在这些层级上定义不同目的镜像分层。

## 发行方式

云固件虚拟磁盘镜像仓库为常见系统和常见计算机类型提供了制作完备的各个分层镜像。这些镜像通常使用UUID来进行区分，UUID的前8位通常会被用来命名来文件夹，镜像文件使用7-zip压缩后存储在该文件夹下。

通常情况下，该文件夹下还会包含README.txt进行说明，该文件通常还包含镜像文件压缩前和压缩后的校验码。

发行的磁盘镜像分成两种类型：需配置后使用及直接使用。

### 配置后使用的镜像

配置后使用的镜像，通常为分层规范中的中间格式，提供该镜像的目的是给使用者在此基础上进一步部署后使用。

![需配置后使用的镜像参考](/manuals/images/just-storage-vhdx.png)

配合[云固件演练场](https://pan.baidu.com/s/1NxE7xWEQ1zyGDaCV4T56NQ)镜像，使用者可以通过复制或者差分该基础镜像进行后续加工处理，具体操作可参考演练场README.txt。

### 直接使用的镜像

直接使用的镜像，通常为制作完毕的镜像，制作者提供了差分好的子镜像和helper辅助引导（后续可取消），并添加了menu.config中的引导参数。使用者只需引入全局vd.config即可在启动界面上看到对应的选择菜单。当然，使用者还可以继续创建差分或者进一步加工到自己需要的更高层级使用环境。

![直接使用的镜像参考](/manuals/images/ready-to-play.png)

需配置后使用和直接使用的镜像的最大区别就是是否存在menu.config文件，没有启动配置文件通常都是中间过程的镜像，不适合最终用户直接使用。

## 常用系统

### Windows 10

- Windows 10 22H2 
  - ISO [Consumer Editions](https://pan.baidu.com/s/1Wb5gTyIuD8JgEMMpv_x_ZQ) [Bussiness Editions](https://pan.baidu.com/s/1GKe7htF1Lc1oVu9Jirfs2g)
  - 全部发行版本 [L0](https://pan.baidu.com/s/1yBnHt4Y9wGwSemmo7-JjpQ)
  - Home [L1](https://pan.baidu.com/s/1Id10BXWeDKM1sMxWJo464g)
  - Professional [L1](https://pan.baidu.com/s/1ukgKcCC6gTQzOdjHVBFd4A)

### Windows 11

- Windows 11 22H2  
  - ISO [Consumer Editions](https://pan.baidu.com/s/1V8N_koNqofwmqdIBHvhuMQ) [Bussiness Editions](https://pan.baidu.com/s/1XG1RV4fEvHcWjVGrSJGiIA)
  - 全部发行版本 [L0](https://pan.baidu.com/s/1papzhJQ6WFSvsVgvdIgomg)
  - Home [L1](https://pan.baidu.com/s/1SRXtGjbSSQukLQ2NluQBxw)
  - Professional [L1](https://pan.baidu.com/s/1qpRqRhTlG5PTk0EfspJomw)

### Ubuntu Desktop

- 22.04 LTS [22.04.2 固定格式VHD，36G](https://pan.baidu.com/s/1rKlwZh4NaLQRG7H11JIDPQ)

## 常见计算机

### Intel NUC

- 豆子峡谷 Bean Canyon
  - Windows 10 22H2 Home [L2](https://pan.baidu.com/s/12vi411sUy-iqx0DbFvKnHA) [L3](https://pan.baidu.com/s/1IOKpeWqS0U438_Vovp9zoA) 
  - Windows 10 22H2 Professional [L2](https://pan.baidu.com/s/1X9G1mIxPqYd469pxFBhg5A) [L3](https://pan.baidu.com/s/1MIRgfN6pMWliEOgJ9UVT0w) 
  - Windows 11 22H2 Home [L2](https://pan.baidu.com/s/1yLpgGj4s0OBA6HIVCBlwrA) [L3](https://pan.baidu.com/s/1raZZIzNCAYLXf1wJQngg4w)
- 猎豹峡谷 Panther Canyon 
  - Windows 11 22H2 Professional [L2](https://pan.baidu.com/s/1CcrC6yY_CiZrFeb3hdfmLg) [L3](https://pan.baidu.com/s/179oLGAB8DUwjDXsKv_y2kA) 

## 结语

更多说明可参考知乎上“AINUC云固件”专栏文章和视频。  
云固件相关文章和视频可在搜索引擎上搜索“云固件”或者“AINUC云固件”。  
欲了解更多信息可微信搜索“AINUC99”添加云固件小助手咨询。

云固件及云固件镜像提及的品牌、商标均为各自的所有者所拥有。
