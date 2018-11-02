### Laptop Specs

`XPS15-9550 ` `i5-6300HQ` `16GB` `PM961 512G` `4K Display` `1080P Monitor`

`10.14.1 18B75` `MacBookPro13,3 `

### Untested 

- Thunderbolt 3
- Bluetooth Devices ( bluetooth mouse works fine )

- SD Card ( Disabled in BIOS )

## Note

You may refer to [wmchris's tutorial](https://github.com/wmchris/DellXPS15-9550-OSX) for the installation guide and solutions to some common issues. 

But note that please create an issue **in my repository**  if you encounter any problem when **using my files or folloing my tutorial** ( Please don't disturb others ). My writing in English is poooooor:(, but I can read :).

You may need to **generate a new `Serial Number`** in SMBIOS section before you login in to an Apple account.

## Issues

### Boot macOS without Clover GUI

Open your `config.plist` with  `Clover Configurator` and set  `Timeout` to `0`  in `Boot` section.

See [Configuration/Boot](https://clover-wiki.zetam.org/Configuration/Boot)

### Native NTFS Read/Write

1. You should **disable Windows 10's hibernation first**: run `powercfg -h off`  in **powershell**.

2. Add `UUID=xxx none ntfs rw,auto,nobrowse` to `/etc/fstab`, **xxx** is the UUID of your Windows 10 partition

### Disable Hibernation

```shell
sudo pmset -a hibernatemode 0
sudo pmset -a autopoweroff 0
sudo pmset -a disksleep 0
sudo pmset -a standby 0
sudo pmset -b tcpkeepalive 0 (optional)
```

`-b` - battery, `-c` - AC Power, and `-a` means both.

(You may need to uncheck any option shown on the `Energy Saver` panel.)

### Headphone

You may need `PostInstall/ALC298PluginFix` to make headphone works properly.

Credit @gooodwin for this plugin and @daliansky for the `install/uninstall.command`

### Font Rendering

(for non-retina display)

```shell
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO
```

### Touchpad doesn't Work after System Update

Rebuild kextcache.

```shell
sudo kextcache -i /
```

### CPU Frequency

the `CPUFriendDataProvider.kext` ([CPUFriend/Instructions](https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md)) in this repo is for `i5-6300HQ` ( Credit @corenel for [the modified plist file](https://github.com/corenel/XPS9550-macOS/commit/7089feb37fbcf841c4cf7196153a2270185bc29c#diff-d9bb32289e5df55b61274ddb859aaff2) ).

Note that the plist file metioned in the CPUFriend/Instructions should already be **modified** for your specific CPU. You may refer to this guide  [HWP(Intel Speed Shift) enable](https://www.insanelymac.com/forum/topic/321021-guide-hwpintel-speed-shift-enable-with-full-power-management/).

### Single/Double Click Delay

See [is-it-possible-to-get-rid-of-the-delay-between-right-clicking-and-seeing-the-context-menu](https://apple.stackexchange.com/a/218181)

> Tapping with the trackpad has a delay while the trackpad decides which gesture you are performing. Disabling some gestures will remove this delay in certain cases:
>
> - If “Smart zoom” is turned on, then a two-finger tap needs to wait to see if you are performing a two-finger double tap.
> - If dragging is enabled (“with drag lock” or “without drag lock”), then a one-finger tap needs to 

## Credits

- The author of every article/repo I mentioned.

