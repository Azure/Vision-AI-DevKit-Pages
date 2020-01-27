---
title: "Platform Tools"
permalink: /docs/platform_tools/
excerpt: "Platform Tools Instructions"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---
In order to communicate with the Vision AI DevKit using a command line, including updating the firmware when needed, you will need the Android SDK Platform Tools. The Vision AI DevKit specifically uses the Android Debug Bridge (ADB) and Fastboot.

## ADB

Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with a device. The ADB command facilitates a variety of device actions, such as installing and debugging apps, and it provides access to a Unix shell that you can use to run a variety of commands on a device. It is a client-server program that includes three components:

* A client, which sends commands. The client runs on your development machine. You can invoke a client from a command-line terminal by issuing an adb command.
* A daemon (adbd), which runs commands on a device. The daemon runs as a background process on each device.
* A server, which manages communication between the client and the daemon. The server runs as a background process on your development machine.

## Fastboot

Fastboot is a protocal for communicating with bootloaders over USB or ethernet. The Vision AI DevKit uses Fastboot for firmware updates.

## Installing

If you have a package manager installed (Chocolatey/Homebrew/Apt/Yum or similar), use a command-line similar to:

```cmd
choco install adb
```

(replacing 'choco' with the package manager of your choice) to install the Platform Tools. Alternatively, you can download and extract the zip containing the Platform Tools to a folder on your PC.

### Download Links

* [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip){:target="_blank"}
* [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip){:target="_blank"}
* [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip){:target="_blank"}

### Set path

Add the directory you extracted the platform tools into to your computer's path environment variable. For Windows, use the command line:

    ```cmd
    set path=%path%;<platform tools path>
    ```

## Common ADB commands  

* Show connected devices

   ```cmd
   adb devices
   ```
  
* Check device firmware version

   ```cmd
   adb shell cat /etc/version
   ```

* Check device battery level (provided as % value)

   ```cmd
   adb shell cat /sys/class/power_supply/battery/capacity
   ```
  
* Reboot the device

   ```cmd
   adb reboot
   ```

* Show available adb command options

   ```cmd
   adb
   ```

* Run a Linux command on the device

   ```cmd
   adb shell [command]
   ```

* Interactively run Linux commands on the device

   ```cmd
   adb shell
   ```
  
* Exit the shell

   ```cmd
   exit
   ```
## ADB commands with two devices connected

* In case you have two devices connected to your laptop you can define which one to controls with *adb -s [deviceID] shell*

For example:

   ```cmd
   adb -s f2ff30x9 shell docker ps
   ```