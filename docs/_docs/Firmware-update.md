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
* ADB (Android Debug Bridge) and Fastboot: Download the command-line tools - [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip), [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip) or [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)
* 7-Zip: Download the [7-Zip file archiver](https://www.7-zip.org/)

* An active Azure subscription. [Activate a free Microsoft Azure account with 12 months of free services.](https://azure.microsoft.com/en-us/free/).

## Useful ADB commands to run when the device is connected to Development system (PC) using the supplied USB cable
1.	Check to see if device is connected to PC
    * _adb devices_
2.	Check the battery level
    * _adb shell cat /sys/class/power_supply/battery/capacity_
3.	Check firmware version
    * _adb shell cat /etc/version_
4.	Type _adb_ alone to display all available commands

## Updating the Firmware

Downloading and Extracting the latest Device Firmware

1.  Get the latest firmware/image released by Altek

2.  Download and extract the .TGZ file with 7zip. After extraction you will see a tar file. Next extract again. You will see more than 120 files located in a folder, for example in folder such as v0.2600_Perf.

3.  Make sure that your platform tools directory is included in your path environment variable. From a CMD window, a simple set path=%path%;F:\AI-CAM\platform-tools_r28.0.1-windows\platform-tools (replace with the right path) would do.

4.  Copy FastBootUpgrad.bat into the directory you extracted the firmware to.

5.  From a CMD window run adb devices to check if the camera is attached/recognized

6.  Run FastBootUpgrade.bat

7.  Follow the instructions given, the camera will update and reboot when done.

8.  If you are stuck at the message <waiting for device>, please reboot it and run FastBootUpgrad.bat again. If you keep hitting the same message, please charge the device for 10+minutes to make sure that the battery is charged.

9.  In your CMD prompt type:

    * _adb shell cat /etc/version_ and confirm that you see the firmware version you are updating to.



