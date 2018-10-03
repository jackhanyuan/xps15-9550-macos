### Laptop Specs

`XPS15-9550 ` `i5-6300HQ` `16GB` `PM961 512G` `4K Display` 

### What's Work

- 10.14 18A391 ( Model: MacBook Pro (15-inch, 2016) )
- CPU Dynamic Freq ( minimum 800 MHz )
- HDMI and USBC (to DP) hot plug
- Sleep/Wake ( Hibernate disabled )
- Correct battery status
- Correct Brightness Control
- Touchpad with `VoodooI2C` 
- Speaker and Headphone ( may need `PostInstall/ALC298PluginFix`)
- ...

**Almost Everything works fine** ( from my personal experience )

#### Untested 

- Thunderbolt 3
- Bluetooth Devices ( bluetooth mouse works fine )

- SD Card ( Disabled in BIOS )

## Note

If you are using this Clover config, please don't forget to generate a new `SMBIOS/System/Serial Number` using `Clover Configurator` before you login an Apple Account.

Please create an issue if you encounter any problem. ( I am poor at English writing, but I can read. )

## 更新记录

### 10.3

使用 [Intel FB-Patcher v1.4.5](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-5.254559/) 重新生成 Framebuffer Patching 和 `USBPort.kext`。之前 Patching 的过程有点问题， `ig-platform-id` 是错误的，这应该是导致 4K 屏直接睡死的主要原因。之前用的 `USBPort.kext` 也是错误的，导致需要额外的补丁才能使外接显示器运作。

- 删除了一些无用的 DSDT/SSDT，同时添加了每个 DSDT 的简单描述信息。
- 使用 `USBPort.kext` 替代之前的 `SSDT-XHC.aml`

改用 [wmchris/DellXPS15-9550-OSX](https://github.com/wmchris/DellXPS15-9550-OSX) 中的 `AppleBacklightInjector.kext`和亮度相关的 dsdt。现在最低亮度比之前低了很多。

### 10.2

改用 [corenel/XPS9550-macOS](https://github.com/corenel/XPS9550-macOS) 的 SSDT/DSDT，其他基本保持不变，主要做了如下修改：

- 删除 `SSDT-ALC298a` ，现在是用 `config.plist` 中注入
- 删除 `SSDT-pr.aml`，这个是来实现 CPU 变频的。现在使用 `CPUFriend` 实现
- 替换 `SSDT-XOSI.aml` 以支持 `VoodooI2C`
- 删除 `USBPort.kext` ，他应该是在 `SSDT-XHC.aml` 里实现了 USB 接口注入
- 增加 `SSDT_IGPU_Syspref.aml` 配合 `agdpmod=vit9696` 以实现外接显示器

换用这个的主要原因是 USB 接口的问题。 `USBPort.kext` 以及 `USBInjectAll.kext`似乎不太稳定，至少我遇到了 Kernel Panic、睡眠失败以及睡眠唤醒后 USB 无法工作这些问题。

### 9.30

使用 [Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/) 和 [[Guide] Intel Framebuffer patching using WhateverGreen](https://www.tonymacx86.com/threads/guide-intel-framebuffer-patching-using-whatevergreen.256490/)，生成了 `HD530` 的 framebuffer。据作者所说，使用这个配合 `WhateverGreen.kext` 后，不再需要任何跟 IGPU 和 HDMI 有关的 kext、补丁以及 Config 配置（所以我全删了），当然禁用独显的补丁 `SSDT-RMDGPU.aml` 还是需要的。

使用 [Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/) 生成了 `USBPort.kext`，它要自己一个个测接口，不知什么原因我的 TypeC/雷电口没有在软件中显示。对照了下其他 USB 口的数据，发现和 [jardenliu/XPS15-9560-Mojave](https://github.com/jardenliu/XPS15-9560-Mojave) 的 `USBPower.kext` 中的一致，因此直接使用了他的。据作者说，使用这个 kext 后，可以把 `USBInjectAll.kext` 和 `SSDT-UIAC.aml` 删了。个人测试发现把 `SSDT-TYPC.aml` 和 `SSDT-YTBT.aml` 删了也没出现什么问题，所以也都删了。

使用 [CPUFriend的教程](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md) 以及 [6300hq 的 plist](https://github.com/corenel/XPS9550-macOS/commit/7089feb37fbcf841c4cf7196153a2270185bc29c) 生成 `CPUFriendDataProvider.kext`。需要注意的是这个 plist 文件有点老。虽然效果不错，但是感觉会有更 native 的方式，以后尝试。

### 9.29

基于 [jardenliu/XPS15-9560-Mojave](https://github.com/jardenliu/XPS15-9560-Mojave) 。添加 `VirtualSMC` 删除 `FakeSMC*`

- 移除 `SMCLightSensor.kext`，用于获取笔记本光感信息，没啥必要（默认会在 Console 疯狂输出）
- 移除 `SSDT-BATC.aml`。`SMCBatteryManager.text` 不需要这个补丁
- 从 [scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation) 拿了一些与 9550 有关的文件

## 问题

### 先安装 WIN10 再安装 macOS

安装WIN10后，默认的EFI分区只有 100MB，而 macOS 要求的 EFI 分区大小至少是 **200MB**，因此会出现无法为macOS新建分区的情况。

解决方法就是**扩大EFI分区到 200MB 以上**就可以了（如果WIN10有恢复分区，可以直接把恢复分区删了扩展到EFI分区，WIN10在更新后会自动重新在分区最后增加恢复分区。

### 开机启动 macOS

如果想要开机直接启动 macOS，可以在 `Clover Configurator-Boot` 中设置 `Default Boot Volume` 为你的macOS 卷的名字，并且设置 Timeout 为 0（设置为 -1 表示不自动启动）。

另一种方式是勾选 `fast` 选项，勾选 `fast` 无法按任意键进入 Clover 界面

### 原生NTFS读写

原生NTFS读写需要**关闭WIN10的Hiberation**：在 powershell 里运行 `powercfg -h off` 后重启一下。

回到macOS，使用 `Disk Utility` 查看 WIN10 分区的 UUID，将以下内容写入到 `/etc/fstab`。

```
UUID=xxx none ntfs rw,auto,nobrowse
```

**xxx** 即为分区的 UUID。

### 睡眠问题

```shell
sudo pmset -a hibernatemode 0
sudo pmset -a disksleep 0
sudo pmset -b tcpkeepalive 0 (optional)
sudo pmset -b standbydelay 3600 (optional)
```

### CPU变频

我的 CPU 是 `i5-6300hq`， `CPUFriendDataProvider.kext` 中的数据是针对这个 CPU 的。

所以其他型号的 CPU 请自行寻找合适的 `CPUFriendDataProvider.kext` 或者使用 [CPUFriend的教程](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md) 。需要注意的是，你需要提供的是一个针对你的 CPU 型号**已经修改过的**一个 plist 文件。

修改教程可以参考 [开启完整HWP(SpeedShift)电源管理特性](http://bbs.pcbeta.com/viewthread-1737021-1-1.html) 。

### Framebuffer, USB 和 Audio

请看 [Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/)

### 单指和双指的单击延迟

参考 [is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-con](https://apple.stackexchange.com/questions/218179/is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-con)

macOS 有一个检测手势的延时。单指单击的延迟是 `双击拖移` 造成的，双指单击的延迟是 `智能缩放` 造成的。因此想要降低单击的延迟，前者可以改用 `三指拖移`，后者取消即可。

## Credits

- Author in any link.