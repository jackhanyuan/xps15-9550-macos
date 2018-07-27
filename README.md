### 配置

6300hq 16GB pm961 512g 4K

### 当前运行情况

- 10.13.6（可无痛升级到10.14 PB4）
- 型号为macbook pro 13,3（请用 Clover Configurator 随机下序列）
- HDMI外接显示器正常
- Sleep正常（合盖测试两小时不到1%），Hiberation不正常
- 电量百分比显示正常（感谢 scottsanett）
- 触摸板功能正常 
- 外放正常，耳机请用ComboJack
- 外接ExFat移动硬盘正常

### 说明

配置主要来自[scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation)

---

1080p建议先别升10.14，Mojave似乎把Subpixel字体渲染移除了，字体显示效果很差。

本文只是简单介绍一些安装情况和问题，具体教程请参考Github上其他repo。

个人不太建议将kext放到`L/E`或`S/L/E`中，因为如果是这些kext出现了问题，将导致系统难以恢复（虽然曾经通过重装系统恢复过且个人文件都在）。最保险的方式还是就把这些kext放在Clover里，这样即使该Clover出现了问题，也可以通过U盘Clover来启动系统。

### 问题

#### 先安装WIN10再安装macOS

安装WIN10后，默认的EFI分区才100MB，而macOS要求的EFI分区大小至少是200MB，因此会出现无法为macOS新建分区的情况。解决方法就是想办法扩大EFI分区就可以了。（如果WIN10有恢复分区，可以直接把恢复分区删了扩展到EFI分区，WIN10在更新后会自动重新在分区最后增加恢复分区。

#### 升级到10.14卡IOConsolesUsers

尝试了好久一直卡IOConsolesUsers，折腾了好久才发现是因为`Lilu.kext`和`IntelGraphicsFixup`默认只在10.13及以下系统运行，所以需要在Clover的`boot arg`中加入`-lilubetaall -igfxbeta`。

#### 安装完成后的启动参数

安装完成后可以把启动参数中的`-v dart=0 kext-dev-mode=1`删除

#### 开机启动macOS

如果想要开机直接启动macOS，可以在Clover Configurator-Boot中设置Default Boot Volume为你的macOS盘的名字，并且设置Timeout为0。（还有一个`fast`选项，不同之处是用`fast`无法按任意键进入Clover选择界面）

#### 触摸板

目前触摸板使用的是`VoodooI2C`，这个驱动有个问题是**双击打开右键菜单需要两个手指先后触碰触摸板**才行。

默认的VoodooI2C因为一些原因无法在10.14下使用（参考 [Kernel panic on startup with macOS Mojave Beta 1](https://github.com/alexandred/VoodooI2C/issues/70)），本Repo使用的`VoodooI2C`来自上贴中的[stevezhengshiqi](https://github.com/stevezhengshiqi)，这个可以正常使用。

另外对附带的`ApplePS2SmartTouchPad.text`进行了一些配置：

- 去除拖移锁定，现在双指拖移窗口或选取内容后不再有锁定延迟
- 去除边缘滚动，默认情况下边缘滚动导致了底部和右边区域无法响应触摸
- 提高触摸精度和速度
- 改善双指滑动体验，个人感觉已经不错了
- 降低操作延迟，默认配置给每一个操作都加了很多的延迟

`ApplePS2SmartTouchPad.text` 有个最主要的问题是手势操作需要抬起手指后才激活。

#### 原生NTFS读写

原生NTFS读写需要**关闭WIN10的Hiberation**：在powershell里运行`powercfg -h off`后重启一下到WIN10。

回到macOS，使用`Disk Utility`查看WIN10分区的UUID，之后在terminal执行

```
sudo echo "UUID=xxx none ntfs rw,auto,nobrowse" >> /etc/fstab
```

重启后，应该会在finder的设备中看到WIN10分区，如果没有可以在finder中`command+shift+G`进入`/Volumes`，将其放入个人收藏中即可。

#### 将显存扩展到2048MB

请参考此贴[自动生成核显补丁,提升显存至2G](http://bbs.pcbeta.com/viewthread-1784050-1-1.html)

#### HDMI外接显示器

外接显示器参考此方法[To make external monitor works](https://github.com/corenel/XPS9550-macOS#tips)。

**Tip**：如果没有在列表中找到你的`Board-ID`，就新增一条，设置 attribute 为 `none`。

#### Brcm出错

在安装过程中可能会遇到Brcm出错，遇到这种情况请把`kexts/other`中`BrcmFirmwareData.kext`和`BrcmPatchRAM2.kext`暂时移走，待安装完成后再移动回来。

#### unallocate area（忘了英文具体是啥了，现在也应该不会有这个问题了）

安装中若遇到无法分配区域的错误，请根据[slide_calc](https://github.com/wmchris/DellXPS15-9550-OSX/blob/10.13/Additional/slide_calc.md)方法自行计算slide。



