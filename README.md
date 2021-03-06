## Laptop Specs

`XPS15-9550`  `i5-6300HQ`  `16GB`  `PM961 512G`  `4K Display`  `1080P Monitor`

`10.14.4 18E226`  `MacBookPro13,3 `

### Not Working 

- eGPU (See [TB3 eGPU (AMD RX580) detection](https://www.tonymacx86.com/threads/lenovo-t480s-tb3-egpu-amd-rx580-detection.272391/#post-1915926))
- SD Card (Disabled in BIOS)

## Note

You may refer to [wmchris's tutorial](https://github.com/wmchris/DellXPS15-9550-OSX) for the installation guide and solutions to some common issues. 

But note that please create an issue **in my repository** if you encounter any problem when **using my files or following my tutorial** ( Please don't disturb others ). My writing in English is poooooor:(, but I can read :).

*After updating system, you should run `sudo kextcache -i /` to make some kexts work(e.g. touchpad).

## Issues

### Skip Clover GUI

Open `config.plist` and set  `Timeout` to `0`  in `Boot` section. (See [Configuration/Boot](https://clover-wiki.zetam.org/Configuration/Boot))

### Disable Hibernation and Fix Sleep Issues

```shell
sudo pmset -a hibernatemode 0
sudo pmset -a autopoweroff 0
sudo pmset -a disksleep 0
sudo pmset -a standby 0
sudo pmset -b tcpkeepalive 0 (optional)
```

`-b` - Battery, `-c` - AC Power, and `-a` means both.

Please uncheck all options (except `Prevent computer from sleeping...`) in the `Energy Saver` panel.

### Headphone

@qeeqez found layout-id 30 is good to drive headphone without PluginFix([Overall Audio State](https://github.com/daliansky/XiaoMi-Pro/issues/96)), and it also works for me. 

So, you can uninstall `ALC298PluginFix`(if installed) and check whether headphone is still working properly, if not, you have to put [CodecCommander](https://bitbucket.org/RehabMan/os-x-eapd-codec-commander/downloads/) back to `kexts/Other` and reinstall `ALC298PluginFix`.

### Non-Retina Display

#### Font Rendering

```shell
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO
```

#### Boot UI Scaling

Open `config.plist` and set  `UIScale` to `1`  in `BootGraphics` section.

### Enable NTFS Writing

- If your NTFS driver contains Windows 10 partition, please run `powercfg -h off`  in Windows 10's powershell to disable hibernation first.
- Add `UUID=xxx none ntfs rw,auto,nobrowse` to `/etc/fstab`, **xxx** is the UUID of your NTFS partition.

### Avoid Tap Delay

- Turn off `Enable dragging` or use `three finger drag` to avoid one-finger tap delay.
- Turn off `Smart zoom` to avoid two-finger tap delay.

See [is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-context-menu](https://apple.stackexchange.com/a/218181)

## Credits

- Authors mentioned in this repo.

