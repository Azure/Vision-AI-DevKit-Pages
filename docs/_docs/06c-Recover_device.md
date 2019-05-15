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
## What you will need

Some troubleshooting steps require the use of an ADB command line. For more information (and to install the ADB utility, please visit the [Platform Tools]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"} section.)

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
