##  更新记录

### 2.11

#### Audio

1. 参考 [Overall Audio State](https://github.com/daliansky/XiaoMi-Pro/issues/96) 将 layout-id 改为 30 以解决耳机失真
2. 删除 `CodecCommander` 

现在你可以卸载 `ALC298PluginFix` 看看耳机是否能正常工作。

#### Kext

更新 `Lilu`、`AppleALC` 和 `CPUFriend`

加回 `NoTouchID`，13,3 在安装的时候还是会出现 TouchID 设置

#### SSDT

将 `SSDT-GPRW` 换成 `SSDT-UPRW` （据 [issue#14](https://github.com/xxxzc/xps15-9550-macos/issues/14)）

加回 `SSDT-HPET`和 `SSDT-MEM2` 

#### Clover

更新 Clover 到 4871，更新 drivers

#### 其他

更新 README.md

### 1.16

更新 `AirportBrcmFixup` 到 `1.1.9` 并加上 `brcmfx-country=#a` 以解决 WiFi 5G 速度问题，见 [issues#12](https://github.com/xxxzc/xps15-9550-macos/issues/12)，感谢 @CyJaySong 。

### 1.4

#### Kext

更新 `Lilu`、`WhateverGreen`、`AirportBrcmFixup`

更新 `CPUFriend` 和 `CPUFriendDataProvider`。我才发现之前用的 CPUFriend 居然是 `1.1.3`。。难怪需要启动参数才能 enable。现在这些 kext 都默认支持 10.14，不需要 `-lilubetaall` 了。 

删除 `NoTouchID`，因为 MacBookPro 13,3 模型没有 Touch ID，不需要这个 kext。

#### SSDT

更新 `SSDT-RMCF.aml` 和 `SSDT-PNLF.aml` （from [RehabMan/OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config)）

#### Theme

更新 Nightwish(256)（from `CloverThemeManager`）

### 12.23

更新 `Lilu`、`AppleALC`、`VirtualSMC`、`WhateverGreen`、`AirportBrcmFixup`

删除 `AppleBacklightFixup`，已经集成到了 WhateverGreen 里

更新 Clover 到 4813，但是 Clover Configurator 里还是显示 4603

修改了一点 `config.plist` 配置

- 删除 Framebuffer Connectors，之前没有这些连不了外接显示器，现在不知道为什么删了还可以，所以删了
- 去掉了 AppleRTC 和 KernelPM，似乎没啥用

### 11.2

更新 Lilu、AppleALC、VirtualSMC、WhateverGreen

修正 USBPorts.kext 里两个 USB2.0 的值为 3，根据如下：

```
HSxx ports connected to USB3 ports should be set to USB3
```

（希望我没有会错意= =）

删除 SSDT-ALS0.aml

### 10.15

使用 [Rehabman/AppleBacklightFixup](https://github.com/RehabMan/AppleBacklightFixup) 代替 `AppleBacklightInjector` 

### 10.10

将 Clover 更新到 Rehabman 版本的 R4697。

尝试修复唤醒无声的问题，还需要多测试。

将主题换成了 Nightwish(256)，默认使用 Nightwish256。

更新了一些 SSDT 和 kexts。

- 将 SSDT-Config 更新为 SSDT-RMCF （from [RehabMan/OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config)），并更新一些相关的 SSDT。主要是删除了所有 IGPU 和 Audio 的 Injection。
- 更新 `AirportBrcmFixup` ， `CodecCommander`，  `VoodooPS2Controller` 以及 `BT4LEContiunityFixup`

删除提高 VRAM 的 patching。

另外发现将 `brcmfx-country` 设置成 `CN` 会导致一些 WiFi 连不上。

### 10.4

将 `SSDT-TB.aml` 换为 `SSDT-TYPC.aml+SSDT-YTBT.aml` 以解决 type-c 的连接问题 。

### 10.3

使用 [Intel FB-Patcher v1.4.5](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-5.254559/) 重新生成 Framebuffer Patching 和 `USBPort.kext`。之前 Patching 的 `ig-platform-id` 是错误的，这应该是导致 4K 屏直接睡死的主要原因。之前用的 `USBPort.kext` 也是错误的。

- 删除了一些无用的 DSDT/SSDT，同时添加了每个 DSDT 的简单描述信息。
- 使用 `USBPort.kext` 替代之前的 `SSDT-XHC.aml`

改用 [wmchris/DellXPS15-9550-OSX](https://github.com/wmchris/DellXPS15-9550-OSX) 中的 `AppleBacklightInjector.kext`和亮度相关的 dsdt。现在最低亮度比之前低了很多。

### 10.2

改用 [corenel/XPS9550-macOS](https://github.com/corenel/XPS9550-macOS) 的 SSDT/DSDT，其他基本保持不变，主要做了如下修改：

- 删除 `SSDT-ALC298a` ，现在是用 `config.plist` 中注入
- 删除 `SSDT-pr.aml`，现在使用 `CPUFriend` 实现
- 替换 `SSDT-XOSI.aml` 以支持 `VoodooI2C`
- 删除 `USBPort.kext` ，他应该是在 `SSDT-XHC.aml` 里实现了 USB 接口注入
- 增加 `SSDT_IGPU_Syspref.aml` 配合 `agdpmod=vit9696` 以实现外接显示器

换用这个的主要原因之前的 USB 接口有问题。

### 9.30

使用 [Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/) 和 [[Guide] Intel Framebuffer patching using WhateverGreen](https://www.tonymacx86.com/threads/guide-intel-framebuffer-patching-using-whatevergreen.256490/)，生成了 `HD530` 的 framebuffer。使用这个配合 `WhateverGreen.kext` 后，不再需要任何跟 IGPU 和 HDMI 有关的 kext、补丁以及 Config 配置，当然禁用独显的补丁 `SSDT-DDGPU.aml` 还是需要的。

使用 [Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/) 生成 `USBPort.kext` 用来替换  `USBInjectAll.kext` 和 `SSDT-UIAC.aml` 删了。

使用 [CPUFriend的教程](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md) 以及 [6300hq 的 plist](https://github.com/corenel/XPS9550-macOS/commit/7089feb37fbcf841c4cf7196153a2270185bc29c) 生成 `CPUFriendDataProvider.kext`。

### 9.29

基于 [jardenliu/XPS15-9560-Mojave](https://github.com/jardenliu/XPS15-9560-Mojave) 。添加 `VirtualSMC` 删除 `FakeSMC*`

- 移除 `SMCLightSensor.kext`，用于获取笔记本光感信息，没啥必要（默认会在 Console 疯狂输出）
- 移除 `SSDT-BATC.aml`。`SMCBatteryManager.text` 不需要这个补丁
- 从 [scottsanett/M5510-4K-High-Sierra-Installation](https://github.com/scottsanett/M5510-4K-High-Sierra-Installation) 拿了一些与 9550 有关的文件