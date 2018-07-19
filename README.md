### 配置

6300hq 16GB pm961 512g 4K

### 当前运行情况

- 10.14 PB4 18A336e（可从10.13无痛升级，注意更新程序要运行两次）
- 型号为macbook pro 13,3（请用 Clover Configurator 随机下序列）
- ~~HDMI外接显示器正常（升级后未测试）~~
- Sleep正常（合盖测试两小时不到1%），Hiberation不正常
- 电量百分比显示正常（感谢 scottsanett）
- 触摸板功能正常 
- 外放正常，耳机请用ComboJack
- 外接ExFat移动硬盘正常

### 说明

配置主要来自[scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation)

---

本文只是简单介绍一些安装情况和问题，具体教程请参考Github上其他repo。

个人不太建议将kext放到`L/E`或`S/L/E`中，因为如果是这些kext出现了问题，将导致系统难以恢复（虽然曾经通过重装系统恢复过且个人文件都在）。最保险的方式还是就把这些kext放在Clover里，这样即使该Clover出现了问题，也可以通过U盘Clover来启动系统。

### 问题

#### 升级到10.14卡IOConsolesUsers

尝试了好久一直卡IOConsolesUsers，折腾了好久才发现是因为`Lilu.kext`和`IntelGraphicsFixup`默认只在10.13及以下系统运行，所以需要在Clover的`boot arg`中加入`-lilubetaall -igfxbeta`。

#### 安装完成后的启动参数

安装完成后可以把启动参数中的`-v dart=0 kext-dev-mode=1`删除

#### 开机启动macOS

如果想要开机直接启动macOS，可以在Clover Configurator-Boot中设置Default Boot Volume为你的macOS盘的名字，并且设置Timeout为0。（还有一个`fast`选项，不同之处是用`fast`无法按任意键进入Clover选择界面）

#### 触摸板

目前触摸板驱动使用的是`ApplePS2SmartTouchPad.text`，进行了一些配置：
- 去除拖移锁定，现在双指拖移窗口或选取内容后不再有锁定延迟
- 去除边缘滚动，默认情况下边缘滚动导致了底部和右边区域无法响应触摸
- 提高触摸精度和速度
- 改善双指滑动体验，个人感觉已经不错了
- 降低操作延迟，默认配置给每一个操作都加了很多的延迟

当然，也可以选择`PostInstall`中的`VoodooI2C`，其优缺点如下：
- 更好的三指手势体验（无需抬起手指即可响应）
- 更好的触摸精度
- (Con.)双指轻触实际需要两只手指快速先后轻触触摸板，体验极差
- (Con.)双指滑动体验一般，有掉帧情况

默认的VoodooI2C因为一些原因无法在10.14下使用（参考 [Kernel panic on startup with macOS Mojave Beta 1](https://github.com/alexandred/VoodooI2C/issues/70)），所以本Repo附带的`VoodooI2C`来自上贴中的[stevezhengshiqi](https://github.com/stevezhengshiqi)，这个可以正常使用。

#### 将显存扩展到2048MB

请参考此贴[自动生成核显补丁,提升显存至2G](http://bbs.pcbeta.com/viewthread-1784050-1-1.html)

#### Brcm出错

在安装过程中可能会遇到Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### 先安装WIN10再安装macOS

安装WIN10后，默认的EFI分区才100MB，而macOS要求的EFI分区大小至少是200MB，因此会出现无法为macOS新建分区的情况。解决方法就是想办法扩大EFI分区就可以了。（如果WIN10有恢复分区，可以直接把恢复分区删了扩展到EFI分区，WIN10在更新后会自动重新在分区最后增加恢复分区。

#### unallocate area（忘了英文具体是啥了，现在也应该不会有这个问题了）

安装中若遇到无法分配区域的错误，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



