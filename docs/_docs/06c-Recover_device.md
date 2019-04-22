---
title: "Firmware update failure"
permalink: /docs/Recover_device/
excerpt: "Recover from a failed firmware update"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
## Recover Vision AI Dev Kit hardware after a failed firmware update

Re-flash using Fastboot, a part of the platform tools, if the device will enter fastboot mode.

```terminal
    > $ adb reboot bootloader
    > $ fastboot devices
    > $ fastboot flash abl abl.elf
    > $ fastboot flash boot qcs605-boot.img
    > $ fastboot flash system qcs605-sysfs.ext4
    > $ fastboot flash userdata qcs605-usrfs.ext4
    > $ fastboot flash persist qcs605-persist.ext4
    > $ fastboot flash cache qcs605-cache.ext4
    > $ fastboot flash systemrw qcs605-systemrw.ext4
    > $ fastboot reboot
```
