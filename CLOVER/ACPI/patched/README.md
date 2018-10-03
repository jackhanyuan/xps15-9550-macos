| AML           | From     | Description                   | Related Patches                                              |
| ------------- | -------- | ----------------------------- | ------------------------------------------------------------ |
| SSDT-ADP1     | @corenel | AC Power                      | Device AC rename to ADP1                                     |
| SSDT-ALS0     | @corenel | fake ALS to save brightness   |                                                              |
| SSDT-BRT6     | @wmchirs | brightness control            | Rename Method BRT6,2 to BRTX,2                               |
| SSDT-Config   | @wmchirs | Config many things            | change GFX0 to IGPU                                          |
| SSDT-DeepIDLE | @corenel | for sleep                     |                                                              |
| SSDT-DDGPU    | @corenel | disable dGPU                  |                                                              |
| SSDT-DMAC     | @corenel | DMA Controller                |                                                              |
| SSDT-GPRW     | @corenel | disabling "wake on USB"       | change Method(GPRW,2,N) to XPRW                              |
| SSDT-I2C      | @wmchirs | I2C Device                    | change _STA to XSTA<br />change _CRS to XCRS in Device TPD1  |
| SSDT-LPC      | @corenel | force AppleLPC to load        |                                                              |
| SSDT-MCHC     | @corenel | Exposes the memory controller |                                                              |
| SSDT-PMCR     | @corenel | to load AppleIntelPCHPMC      |                                                              |
| SSDT-PNLF     | @wmchirs | brightness control            |                                                              |
| SSDT-PTSWAK   | @corenel | for correct shutdown          | change Method(\_PTS,1,N) to ZPTS<br />change Method(\_WAK,1,N) to ZWAK |
| SSDT-SATA     | @corenel | enable the SATA controller    | change SAT0 to SATA                                          |
| SSDT-SMBUS    | @corenel | identifies the SMBus          |                                                              |
| SSDT-TB       | @corenel | usb-c hot-plug                |                                                              |
| SSDT-XOSI     | @wmchirs | for VoodooI2C                 | Change OSID to XSID<br />change _OSI to XOSI                 |
