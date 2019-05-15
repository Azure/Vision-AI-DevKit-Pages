---
title: "Rebooting"
permalink: /docs/Reboot/
excerpt: "Using the ADB shell to reboot the Vision AI DevKit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
## What you will need
* ADB command line utility. ([Installation]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"} section.)

## Reboot the Vision AI DevKit hardware

* Click the reset button once, using the pin hole on the right side of the camera.
* Press the power button on the back once.
* Use the command line

  ```cmd
  adb reboot
  ```

* Long press the power button more than 12 seconds, to force a power down of the hardware. Then hold the power button for more than 12 seconds again to power up the hardware.
