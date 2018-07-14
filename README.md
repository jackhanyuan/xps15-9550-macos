### 配置

6300hq 16GB pm961 512g 4k

### 当前运行情况

- 10.13.6 （可无痛升级，注意更新程序要运行两次）
- 型号为macbook pro 13,3（请用Clover Configurator随机下序列）
- HDMI外接显示器正常（升级后未测试）
- Sleep正常（合盖基本不掉电）
- 电量百分比显示正常
- 触摸板功能正常
- type-c接口接android手机无法正常使用

### 说明

配置主要来自[scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation)

---

本文只是简单介绍一些安装情况和问题，具体教程请参考Github上其他repo。

个人不太建议将kext放到`L/E`或`S/L/E`中，因为如果是这些kext出现了问题，将导致系统难以恢复（虽然曾经通过重装系统恢复过且个人文件都在）。最保险的方式还是就把这些kext放在Clover里，这样即使该Clover出现了问题，也可以通过U盘Clover来启动系统。

### 其他

#### 开机启动macOS

如果想要开机直接启动macOS，可以使用Clover Configurator-Boot中设置Default Boot Volume为你的macOS盘的名字，并且设置Timeout为0。（还有一个`fast`选项，和设置Timeout的不同之处是用`fast`无法按任意键进入Clover选择界面）

#### 触摸板

默认触摸板使用的是`VoodooI2c`的方案，个人测试感觉还行，就是手势不是太完美。可以考虑换成`ApplePS2SmartTouchPad.text`，注意换用该驱动需要把`kexts/Other`中的`VoodooI2C.kext`，`VoodooI2CHID.kext`和`VoodooPS2Controller.kext`都删了，不然会产生冲突。

~~目前触摸板驱动使用的是`ApplePS2SmartTouchPad.text`，虽然在触摸精确度和延迟上不太好，但至少滚动体验要好于Voodoo。另外修改了拖动的参数，拖动完成后不会有300ms的延时了。
有个问题是触摸板底部‘按键’区域无法直接识别到触摸，目前还没有找到解决方法。~~

#### Brcm出错

在安装过程中可能会遇到Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### 先安装WIN10再安装macOS

安装WIN10后，默认的EFI分区才100MB，而macOS要求的EFI分区大小至少是200MB，因此会出现无法为macOS新建分区的情况。解决方法就是想办法扩大EFI分区就可以了。

#### unallocate area（忘了英文具体是啥了）

安装中若遇到无法分配区域的错误，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



