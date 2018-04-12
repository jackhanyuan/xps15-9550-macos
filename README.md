### 配置

6300hq 4+4 GB pm961 256g 4k屏

### 当前运行情况

- 10.13.4 ，型号为macbook pro 13,1（请使用Clover Configurator选择适合自己的型号）
- HDMI外接显示器正常
- 不知是否真实睡眠，总之黑屏唤醒正常
- 电量百分比显示正常
- 触摸板设置正常显示但大部分功能不可用（不支持各种手势）
- 触摸板可双击选择和拖动窗口（辅助功能-鼠标和触摸板-触摸板选项中开启拖移）
- type-c接口接android手机无法正常使用

### 说明

本Clover的配置主要来自[corenel](https://github.com/corenel/XPS9550-macOS)，驱动主要来自[gunslinger](https://github.com/gunslinger23/XPS15-9560-High-Sierra)。

换了4k屏后发现win10下文字显示已足够清晰，至少代码显示足够清晰，因此就没有再使用macos的必要了，所以就备份下Clover文件。

请注意pm981目前无法安装macos，别像我一样傻傻地陷入出错-安装的死循环中T T。。。

当然论坛上有人使用10.13.4将pm981作为从盘驱动成功，评论表示仍然作不了安装盘。

需要使用该Clover安装请先把boot参数里的`slide=163`去掉并且加入`-v`显示调试信息。

本文只是简单介绍一些安装情况和问题，具体教程请参考Github上其他repo。

### 其他

#### 开机启动macOS

如果想要开机直接启动macOS，可以使用Clover Configurator-Boot中设置Default Boot Volume为你的macOS盘的名字，并且设置Timeout为0。

#### 触摸板

clover中的触摸板文件来自[gunslinger](https://github.com/gunslinger23/XPS15-9560-High-Sierra)，但我后来又安装了[OS-X-Voodoo-PS2-Controller](https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller/wiki/How-to-Install)所以我不太确定目前是哪个在起作用，之后才从13.3升级到13.4。

目前已知的情况是前者在10.13.3时是支持三指左右切换桌面，但触摸板设置空白。

#### Brcm出错

在安装过程中可能会因此Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### does printf work？

安装中若遇到does printf work，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



