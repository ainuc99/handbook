# 云固件必备资源

欢迎您测试和使用AINUC®云固件。本文提供了安装和使用云固件时必须下载的文件资源，这些文件通常保存在百度网盘上，其中镜像文件通常超过10GiB，非会员下载速度受限，对下载速度有要求的用户建议付费购买会员。

## 云固件主程序

截至到2023/07/17本文更新时，最新发布版本为r23715，发布日期为2023/07/15。

### 修改记录 v1.4.23715 2023/07/15
- 支持RAW/HDD/IMG格式的镜像磁盘
- 修正VDs位于mbr格式磁盘上云固件启动不正常的错误
- 使用第三方EFI应用支持ISO格式镜像启动
- 固化辅助引导，支持配置helper参数

### 下载链接

**[百度网盘](https://pan.baidu.com/s/1D4NuMqWCKhRA8G49_SQwAg)**  

## 通用镜像

云固件通用镜像是指不受计算机型号限制的磁盘镜像，通常这类镜像是部署过程中的镜像，没有安装全部驱动程序，没有更新操作系统必须的补丁，但这些镜像适配绝大多数的计算机型号，对于未出现在云固件支持的“常见计算机型号”一文的计算机，建议选择通用镜像自行完善。对于需要定制特定部署的支持型号，您也可以选择通用镜像来完善。

**注意：云固件目前只支持x64（x86_64）位系统，没有特殊说明的话都是指64位系统，包括主程序和镜像文件内的操作系统**

*镜像内包含的操作系统、应用软件、品牌、商标等所有权均属于各自所有者*

### Windows 10

|标题|镜像级别|Short ID|下载链接|备注|
|:-----|:----:|:----|:----|:----|
|Windows 10 22H2（March 2023）|L0|a0b28d74|[百度网盘](https://pan.baidu.com/s/1yBnHt4Y9wGwSemmo7-JjpQ)|含7个版本L0释放镜像，*需配置后使用*|
|Windows 10 22H2（March 2023）Home|L1|a1c562f3|[百度网盘](https://pan.baidu.com/s/1Id10BXWeDKM1sMxWJo464g)|家庭版，*需配置后使用*|
|Windows 10 22H2（March 2023）Pro|L1|a1fe3133|[百度网盘](https://pan.baidu.com/s/1Ag1bGHk1tUoXN3jegazVIw)|专业版，*需配置后使用*|

配置说明参考此处（待更新）

## 常见计算机型号

云固件对常见机型提供了常见系统和环境的完善镜像（目前受限本人拥有的型号^_^），这些镜像完善程度可以达到L3~L5级别。

#### Intel NUC 猎豹峡谷 Panther Canyon

|标题|镜像级别|Short ID|下载链接|备注|
|:-----|:----:|:----|:----|:----|
|Windows 11 22H2 Pro NUC11PA|L3|b3056145|[百度网盘](https://pan.baidu.com/s/179oLGAB8DUwjDXsKv_y2kA)|**猎豹峡谷可直接使用**|

#### Intel NUC 豆子峡谷 Bean Canyon

|标题|镜像级别|Short ID|下载链接|备注|
|:-----|:----:|:----|:----|:----|
|Windows 10 22H2 Pro NUC8BE|L3|a37cc628|[百度网盘](https://pan.baidu.com/s/1OOIkpbeDWt3ZxMLAstLLNA)|**豆子峡谷可直接使用**|

## 更多计算机型号

### Intel NUC

猎豹峡谷 Panther Canyon 石英峡谷 寒霜峡谷 冥王峡谷 豆子峡谷 Bean Canyon

### Lenovo Thinkpad

E475

### HP ProDesk

600 G1 DM

### TOPFEEL

T68M