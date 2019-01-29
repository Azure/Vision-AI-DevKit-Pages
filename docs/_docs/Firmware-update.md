---
title: "Firmware Update"
permalink: /docs/firmware-update/
excerpt: "How to update the firmware for the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-01-28
---

## What you will learn
* Check the firmware version of the device
* Update the firmware in your device

## What you will need
* Vision AI Dev Kit hardware
* USB-C cable
* ADB (Andriod Debug Bridge) and Fastboot: Download the command-line tools - [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip), [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip) or [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)
* 7-Zip: Download the [7-Zip file archiver](https://www.7-zip.org/)

* An active Azure subscription. [Activate a free Microsoft Azure account with 12 months of free services.](https://azure.microsoft.com/en-us/free/).

## Useful ADB commands to run when the device is connected to Development system (PC) using the supplied USB cable
1.	Check the battery level
adb shell cat /sys/class/power_supply/battery/capacity
2.	Check to see if device is connected to PC
adb devices
3.	Check firmware version
adb shell cat /etc/version
4.	Type adb alone to display all available commands


