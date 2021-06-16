---
title: "Rebooting"
permalink: /docs/Reboot/
excerpt: "Using the ADB shell to reboot the Vision AI DevKit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-28
---
## What you may need

* ADB command line utility. ([instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})

## Options to reboot the camera

* Click the reset button once, using the pin hole on the right side of the camera.
* Press the power button on the back once.
* Command line:

  ```cmd
  adb reboot
  ```
## To factory reset the camera

* Long press the power button more than 12 seconds, which will force the camera to reset. Then press the power button once or plug the camera in to power to turn the camera on.
