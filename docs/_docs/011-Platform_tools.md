---
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

> adb

Shows you all the available adb commands


