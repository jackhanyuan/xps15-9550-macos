### Laptop Specs

`XPS15-9550 ` `i5-6300HQ` `16GB` `PM961 512G` `4K Display` 

### What's Work

- 10.14 18A391 ( Model: MacBook Pro (15-inch, 2016) )
- CPU Dynamic Freq ( minimum 800 MHz )
- HDMI and USBC (to DP) hot plug
- Sleep/Wake ( Hibernation disabled )
- Correct battery status
- Correct brightness control
- Touchpad with `VoodooI2C` 
- Speaker and Headphone ( may need `PostInstall/ALC298PluginFix`)
- ...

**Almost everything works fine**

#### Untested 

- Thunderbolt 3
- Bluetooth Devices ( bluetooth mouse works fine )

- SD Card ( Disabled in BIOS )

## Note

Please don't forget to generate a new `SMBIOS-System-Serial Number` using `Clover Configurator` before you login in to an Apple account.

Create an issue with your hardware description( CPU, SSD, Display ... ) if you encounter any problem ( My writing in English is poooooor, but I can read ).

## Issues

### Booting macOS without Clover GUI

Open your `config.plist` with  `Clover Configurator` and set  `Timeout` to `0`  in `Boot` section.

See [Configuration/Boot](https://clover-wiki.zetam.org/Configuration/Boot)

### Native NTFS Read/Write

1. You should **disable Windows 10‘s Hibernation first**: Run `powercfg -h off`  in **powershell**.

2. Add `UUID=xxx none ntfs rw,auto,nobrowse` to `/etc/fstabb`, **xxx** is your Windows 10 partition's UUID

### Sleep and Disable Hibernation

```shell
sudo pmset -a hibernatemode 0
sudo pmset -a disksleep 0
sudo pmset -a standby 0
sudo pmset -b tcpkeepalive 0 (optional)
```

`-b` is for battery, `-c` is for AC Power, and `-a` means both.

### CPU Frequency

the `CPUFriendDataProvider.kext` ([CPUFriend/Instructions](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md)) in this repo is for `i5-6300HQ`.

Note that the plist file metioned in the above instructions should already be **modified** for your specific CPU.

修改教程可以参考 [开启完整HWP(SpeedShift)电源管理特性](http://bbs.pcbeta.com/viewthread-1737021-1-1.html) 。

### Framebuffer, USB and Audio

[Intel FB-Patcher v1.4.3](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-4-3.254559/)

### Single/Double Click Delay

See [is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-context-menu](https://apple.stackexchange.com/a/218181)

> Tapping with the trackpad has a delay while the trackpad decides which gesture you are performing. Disabling some gestures will remove this delay in certain cases:
>
> - If “Smart zoom” is turned on, then a two-finger tap needs to wait to see if you are performing a two-finger double tap.
> - If dragging is enabled (“with drag lock” or “without drag lock”), then a one-finger tap needs to wait to see if you are performing a double tap. (This setting hides in the Accessibility preference pane.)

## Credits

- The author of every link I mentioned.

