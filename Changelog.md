## 更新记录

### 10.4

这应该是最近最后一次改动了。

将 `SSDT-TB.aml` 换为 `SSDT-TYPC.aml+SSDT-YTBT.aml` 以解决 type-c 的连接问题 。

~~使用 `SATA-100-series-unsupported.text` 替代  `SSDT-SATA.aml` 以及有关的 hot-patch。~~

删除了一些没有用的文件。

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