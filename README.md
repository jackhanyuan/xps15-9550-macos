### 配置

6300hq 16GB pm961 512g 4k

### 当前运行情况

- 10.13.6 （可无痛升级，注意更新程序要运行两次）
- 型号为macbook pro 13,3（请用Clover Configurator随机下序列）
- HDMI外接显示器正常（升级后未测试）
- sleep正常（合盖基本不掉电），hiberation不正常
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

目前触摸板驱动使用的是`ApplePS2SmartTouchPad.text`，进行了一些配置：
- 去除拖移锁定，现在双指拖移窗口或选取内容后不再有锁定延迟
- 去除边缘滚动，默认情况开启了边缘滚动，导致底部和右边区域无法响应触摸
- 提高触摸精度和速度
- 改善双指滑动体验，不过依然没有WIN10来得爽
- 降低操作延迟，默认配置给每一个操作都加了很多的延迟

当然，也可以选择`PostInstall`中的`VoodooI2C`，其优缺点如下：
- 更好的三指手势体验
- 更好的触摸精度
- 双指轻触需要一定按压力度才能响应
- 双指滑动体验一般，有掉帧情况

#### Brcm出错

在安装过程中可能会遇到Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### 先安装WIN10再安装macOS

安装WIN10后，默认的EFI分区才100MB，而macOS要求的EFI分区大小至少是200MB，因此会出现无法为macOS新建分区的情况。解决方法就是想办法扩大EFI分区就可以了。

#### unallocate area（忘了英文具体是啥了，现在也应该不会有这个问题了）

安装中若遇到无法分配区域的错误，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



