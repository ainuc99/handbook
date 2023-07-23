# 云固件镜像演练场

云固件为常见系统和常见计算机类型提供了制作完备的各个分层镜像。

发行的磁盘镜像分成两种类型：需配置后使用及直接使用。

- 配置后使用的镜像，通常为分层规范中的中间格式，提供该镜像的目的是给使用者在此基础上进一步部署后使用。  
配合[云固件镜像演练场](https://pan.baidu.com/s/1NxE7xWEQ1zyGDaCV4T56NQ)镜像，使用者可以通过复制或者差分该基础镜像进行后续加工处理。  

- 直接使用的镜像，通常为制作完毕的镜像  
制作者提供了差分好的子镜像和helper辅助引导（后续可取消），并添加了menu.config中的引导参数。使用者只需引入全局vd.config即可在启动界面上看到对应的选择菜单。当然，使用者还可以继续创建差分或者进一步加工到自己需要的更高层级使用环境。

## Helper辅助引导

Helper是专门为不受云固件支持、但操作系统和基于操作系统的驱动程序支持的虚拟磁盘格式准备的。此类镜像只需配合对应的helper辅助启动镜像即可完成云固件内和原始支持格式相同的方式进行启动。

云固件截至到2023/07/15日，原生支持的镜像格式为raw及固定、动态的VHD类型，通常Windows使用的vhdx格式尚未支持，需要使用Helper来辅助引导vhdx镜像。

vhdx格式受云固件支持后，面向Windows的helper原则上就可以废弃了。


## 启动配置

云固件使用过程最重要的配置文件就是云固件镜像的主入口配置：vd.config。该文件保存在VDs分区，也可能和其他系统的文件混合在一次。但vd.config必须位于某个分区的根目录。

vd.config通常作为主入口配置文件，因此，它一般只使用include参数来配置，核心作用是把分散到各个镜像文件夹下的menu.config合并为一个总入口文件供云固件使用。如下例：

``` shell
include \99887766\menu.config
```

menu.config文件是每个镜像文件夹下的启动配置文件。如下例：

``` shell
menuentry "AINUC Multiware Playground" {
  icon "\99887766\win11.png"
  helper "\99887766\win-11-helper-Work.vhd"
  vdisk "\99887766\Work.vhdx"
  vdtype vhdx
}
```

各个参数项说明：
- menuentry "name or something different"  
该参数定义了在云固件主界面上显示的镜像选择菜单，引号后的文字就是选择的提示标题，通常是操作系统名称或者环境名称
- icon "\99887766\work.png"  
镜像选择菜单的图片，支持png和bmp格式，建议使用png格式
- helper "some boot loader vhd"  
独立的启动分区镜像文件，用来辅助引导云固件不支持的镜像文件格式，必须使用固定格式或者动态格式的VHD文件
- vdisk "some virtual disk file name"  
主镜像文件，含路径和文件名
- vdtype "vd format name"  
主镜像文件格式，只支持vhd/raw两种格式，其他名称都会被当做raw格式对待。如果使用了辅助引导，vdisk和vdtype参数都会被忽略

启动配置文件内可以配置多个menuentry段，代表多个镜像选择菜单项。

menu.config配置也可以更名，更名后在主入口配置文件vd.config中需要引入更名后的名称方能有效。

menuentry也可以直接在vd.config主入口配置文件中添加，但添加后破坏了主入口的单一功能，逻辑会混乱，非特殊情况不建议这样修改。

## 使用镜像

直接使用的镜像可以在vd.config中直接引入，就可以在云固件主界面看到镜像选择菜单。配置后使用的镜像，需要配置演练场内的辅助启动和配置来使用。

演练场文件夹下包含了Windows10/11两种操作系统的helper，比如“win-10-helper-**Code**.vhd”对应“**Code**.vhdx”，只需将需要启动的Windows10镜像
- 复制为Code.vhdx
- 差分为Code.vhdx  

然后添加到menu.config，并将menu.config在外层的vd.config引入，那么重新启动后就可以看到Code镜像对应的镜像选择菜单按钮，选择后即可启动Code镜像。

### 复制模式

镜像文件复制到演练场文件夹下，改名为演练场内提供的“Code”、“Work”、“Office”、“Home”、“Game”名称，比如Code.vhdx。

### 差分模式

使用差分时，Windows在父子镜像文件跨文件夹时存在问题，所以需要把父子镜像都放在相同文件夹下。Windows下可使用演练场内提供额Bootice来完成。

![创建差分磁盘](/manuals/images/bootice-make-diff.png)

创建后的差分镜像文件名称也要使用演练场内提供的名称，如Code.vhdx等。

*注意：复制和差分操作后，都需要修改menu.config和vd.config完成设置，方能在云固件主界面看到镜像选择菜单。*

## 总结

由于Linux等系统原生是不支持vhdx格式，所以需要独立制备helper，但helper的制备过程较为复杂，云固件的支持上也有没完善之处，在镜像提供的文件夹内会包含helper辅助引导，所以演练场就不提供针对Linux的内容。

对于Windows7、8、8.1等旧版系统，后续会更新到演练场内供下载使用。

更多说明可参考知乎上“AINUC云固件”专栏文章和视频。  
云固件相关文章和视频可在搜索引擎上搜索“云固件”或者“AINUC云固件”。  
欲了解更多信息可微信搜索“AINUC99”添加云固件小助手咨询。

云固件及云固件镜像提及的品牌、商标均为各自的所有者所拥有。