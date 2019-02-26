-
title: "ADB Platform Tools"
permalink: /docs/adb_platform_tools/
excerpt: "Instructions for ADB platform tools"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-25
---


In order to be able to communicate with Vision AI Dev Kit from the command line and update the firmware when needed you'll need Platform Tools. Platform tools is a collection of command line tools of which the most essential ones are ADB and Fastboot.

## What is ADB?
Android Debug Bridge (adb) is a versatile command-line tool that lets you communicate with a device. 
The adb command facilitates a variety of device actions, such as installing and debugging apps, 
and it provides access to a Unix shell that you can use to run a variety of commands on a device.

## What is Fastboot?
Fastboot is a protocal that can be used to perform a firmware update to Vision AI Dev Kit and flash the device.

## Platform Tools
* Install ADB (Android Debug Bridge) and Fastboot tool. Download for [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip), [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip){:target="_blank"} or [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip){:target="_blank"}

## Most popular ADB commands

Show you all the available adb commands <br>
  `adb`

Check that device is recognized <br>
  `adb devices`
  
In order to run Linux commands in a device <br>
  `adb shell [command]` 
  or <br>
  `adb shell`
  that allows you to run multiple commands in shell
  
Type <br>
  `exit` 
to exit shell

Check the firmware version of the device <br>
  `adb shell cat /etc/version`

Check the battery level of teh device (notice that the answer is provided as % without a %-sign as an example 80)
  `adb shell cat /sys/class/power_supply/battery/capacity`

You can find other usefull adb commands from the troubleshooting section
