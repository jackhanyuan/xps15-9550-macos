| AML           | Description                   | Related Patches                                              |
| ------------- | ----------------------------- | ------------------------------------------------------------ |
| SSDT-BRT6     | brightness control keymaps    | Rename Method BRT6,2 to BRTX,2                               |
| SSDT-DDGPU    | disable dGPU                  |                                                              |
| SSDT-DeepIDLE | deep idle                     |                                                              |
| SSDT-DMAC     | DMA Controller                |                                                              |
| SSDT-HDEF     | to load Audio                 | Change HDAS to HDEF                                          |
| SSDT-HPET     | disable HPET device           | Rename HPET to XPET                                          |
| SSDT-I2C      | I2C Device (Interrupts)       | Change _STA to XSTA<br />Change _CRS to XCRS                 |
| SSDT-LPC      | force AppleLPC to load        |                                                              |
| SSDT-MEM2     | add missing MEM2 device       |                                                              |
| SSDT-MCHC     | exposes the memory controller |                                                              |
| SSDT-PMCR     | to load AppleIntelPCHPMC      |                                                              |
| SSDT-PNLF     | for correct brightness        |                                                              |
| SSDT-PTSWAK   | for correct shutdown          | Change Method(\_PTS,1,N) to ZPTS<br />Change Method(\_WAK,1,N) to ZWAK |
| SSDT-RMCF     | control many SSDTs            | Change GFX0 to IGPU                                          |
| SSDT-SATA     | SATA Controller               | Change SAT0 to SATA                                          |
| SSDT-SMBUS    | identifies the SMBus          |                                                              |
| SSDT-TYPC     | Type-C hot-plug               | Rename _RMV to XRMV                                          |
| SSDT-UPRW     | disable "wake on USB"         | Rename method UPRW to XPRW<br />Rename method GPRW to YPRW   |
| SSDT-USBX     | set USB current               |                                                              |
| SSDT-XOSI     | VoodooI2C                     | Change OSID to XSID<br />Change _OSI to XOSI                 |
| SSDT-YTBT     | DSDT recursion issue          | ~~Rename XTBT to YTBT~~                                      |

### Credits

[KNNSpeed/guide-dell-xps-15-9560](https://www.tonymacx86.com/threads/guide-dell-xps-15-9560-4k-touch-1tb-ssd-32gb-ram-100-adobergb.224486/), [RehabMan/OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config) and [corenel/XPS9550-macOS](https://github.com/corenel/XPS9550-macOS)

