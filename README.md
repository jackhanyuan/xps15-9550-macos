### 配置

6300hq 16GB pm961 512g 4k

### 当前运行情况

- 10.13.5 无痛升级到 10.13.6 （更新程序要运行两次）
- 型号为macbook pro 13,3（使用Clover Configurator选择适合的型号）
- HDMI外接显示器正常（升级后未测试）
- 不知是否真实睡眠，总之黑屏唤醒正常
- 电量百分比显示正常（拔出接入电源时更新会有一点延迟）
- 触摸板功能正常（辅助功能-鼠标和触摸板-触摸板选项中开启拖移）
- type-c接口接android手机无法正常使用

### 说明

本Clover的配置主要来自[corenel](https://github.com/corenel/XPS9550-macOS)

---

本文只是简单介绍一些安装情况和问题，具体教程请参考Github上其他repo。

个人不太建议将kext放到`L/E`或`S/L/E`中，因为如果是这些kext出现了问题，将导致系统难以恢复（虽然曾经通过重装系统恢复过且个人文件都在）。最保险的方式还是就把这些kext放在Clover里，这样即使该Clover出现了问题，也可以通过U盘Clover来启动系统。

### 其他

#### 开机启动macOS

如果想要开机直接启动macOS，可以使用Clover Configurator-Boot中设置Default Boot Volume为你的macOS盘的名字，并且设置Timeout为0。

#### 触摸板

目前触摸板驱动使用的是`ApplePS2SmartTouchPad.text`，虽然在触摸精确度和延迟上不太好，但至少滚动体验要好于Voodoo。另外修改了拖动的参数，拖动完成后不会有300ms的延时了。
有个问题是触摸板底部‘按键’区域无法直接识别到触摸，目前还没有找到解决方法。

#### Brcm出错

在安装过程中可能会遇到Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### unallocate area（忘了英文具体是啥了）

安装中若遇到无法分配区域的错误，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



