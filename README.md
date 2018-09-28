### 配置

`i5-6300HQ` `16GB` `PM961 512G` `1080p` 

### 当前运行情况

- 10.14 正式版
- 型号为 MacBook Pro (15-inch, 2016)
- HDMI 和 Typec 热插拔外接显示器正常
- Sleep正常（合盖基本不掉电）
- Hiberation 禁用（可以有，但没必要）
- 电量百分比显示不太正常，延迟很高
- 触摸板使用 `VoodooI2C`
- 外放和耳机正常（见问题 4）
- 外接ExFat移动硬盘正常

#### 未测试

- 蓝牙
- 雷电

### 说明

配置主要来自[jardenliu/XPS15-9560-Mojave](https://github.com/jardenliu/XPS15-9560-Mojave)

使用了[scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation) 的部分 `ACPI/patched` 和 `config.plist` 以适应 9550 以及支持 TypeC/雷电口 的热插拔

---

本文只是简单介绍一些安装情况和问题，具体教程请参考 Github 上其他 repo。

个人不太建议将 kext 放到`L/E`或`S/L/E`中，这些kext出现了问题将导致系统难以恢复。最保险的方式还是就把这些kext放在 Clover 里，这样即使该 Clover 出现了问题，也可以通过U盘 Clover 来启动系统。

### 问题

#### 1. 先安装 WIN10 再安装 macOS

安装WIN10后，默认的EFI分区只有 100MB，而 macOS 要求的 EFI 分区大小至少是 **200MB**，因此会出现无法为macOS新建分区的情况。

解决方法就是想办法**扩大EFI分区到 200MB 以上**就可以了。（如果WIN10有恢复分区，可以直接把恢复分区删了扩展到EFI分区，WIN10在更新后会自动重新在分区最后增加恢复分区。

#### 2. 安装完成后的启动参数

安装完成后可以把启动参数中的 `-v dart=0` 删除

#### 3. 开机启动macOS

如果想要开机直接启动 macOS，可以在 `Clover Configurator-Boot` 中设置 `Default Boot Volume` 为你的macOS 卷的名字，并且设置 Timeout 为 0（设置为 -1 表示不自动启动）。

另一种方式是勾选 `fast` 选项，勾选 `fast` 无法按任意键进入 Clover 界面

#### 4. 驱动耳机

默认下外放应该是正常的

耳机则需要安装 `PostInstall/ALC298PluginFix` ，直接运行 `install双击自动安装.command` 即可。

#### 5. 原生NTFS读写

原生NTFS读写需要**关闭WIN10的Hiberation**：在 powershell 里运行 `powercfg -h off` 后重启一下。

回到macOS，使用 `Disk Utility` 查看 WIN10 分区的 UUID，之后在终端执行

```
sudo echo "UUID=xxx none ntfs rw,auto,nobrowse" >> /etc/fstab
```

重启后，应该会在 finder 中看到 WIN10分区，如果没有可以在finder中 `command+shift+G` 进入 `/Volumes`，将其放入个人收藏中即可。

#### 6. 外接显示器

外接显示器如果无法工作，请参考此方法[To make external monitor works](https://github.com/corenel/XPS9550-macOS#tips)。

**Tip: **如果没有在列表中找到你的`Board-ID`，就新增一条，设置 attribute 为 `none`。

#### 7. Brcm 死循环

在安装过程中可能会遇到 Brcm 死循环（Mojave 装了两次没遇到），请把 `kexts/other` 中 `BrcmFirmwareData.kext` 和`BrcmPatchRAM2.kext` 暂时移走，待安装完成后再移动回来。

#### 8. 声音无法调节？

遇到了一个很奇怪的问题，声音刚安装好的时候是可以调节的，然后改了点东西后居然无法调节了。试了好久才发现是因为。。。

**外接显示器后默认的音频输出被改为了显示器的音频输出，而我的显示器并没有外放！！！**

改回使用内置扬声器就好了。

#### 9. 单击和双击延迟

See [is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-con](https://apple.stackexchange.com/questions/218179/is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-con)

macOS 有一个用于检测延时的机制。单击的延迟是 `双击拖移` 造成的，双击的延迟是 `智能缩放` 造成的。

因此，单击的延迟可以通过选择使用 `三指拖移` 来关闭，双击的延迟则可以通过关闭 `智能缩放` 来关闭。

#### 10. 合盖睡眠

```
sudo pmset -a hibernatemode 0
sudo pmset -a disksleep 0
```

SSD 耗电小而且 SSD 睡眠还有可能造成数据出错，因此没有使硬盘进入睡眠的必要。