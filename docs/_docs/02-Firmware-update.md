---
title: "Firmware Update"
permalink: /docs/Firmware-update/
excerpt: "How to update the firmware for the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-07
---

## What you will do
* Check the firmware version of the device
* Update the firmware in your device, if necessary

## What you will need
* Vision AI Dev Kit hardware
* USB-C cable
* Installed ADB (Android Debug Bridge) and Fastboot tool. Download for [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip), [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip){:target="_blank"} or [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip){:target="_blank"}
* Zip archive extractor (such as the [7-Zip file archiver](https://www.7-zip.org/){:target="_blank"})

## Verify your computer is connected to the Vision AI Dev Kit hardware
* Connect your computer and the Vision AI Dev Kit camera using a USB-C cable
* Open a command line prompt on your computer and use the command
    ```
    adb devices
    ```
You should see output similar to this, if your computer and camera are connected properly.
    ```
    C:\Tools>adb devices
    List of devices attached
    efb99xxx        device
    ```
If you do not see the device, try rebooting the camera hardware. There are several methods available to reboot:

* Use the pin hole on the right side of the camera to click once.
* Press the power button on the back once.
* Use the command:
    ```
    adb reboot
    ```
* Long press the power button for longer than 12 seconds to force a shut down. Then hold the power button for longer than 12 seconds again to start the device.

## Useful ADB commands when the device is connected to a computer using a USB-C cable
1.	Check to see if device is connected to PC
    ```
    adb devices
    ```
2.	Check the battery level
    ```
    adb shell cat /sys/class/power_supply/battery/capacity
    ```
3.	Check firmware version
    ```
    adb shell cat /etc/version
    ```

## Updating the Firmware
The Vision AI Dev Kit hardware **must be charged for at least 10 minutes** (using a 2A charger) before starting the firmware flashing process.

### Downloading and Extracting the latest Device Firmware
1. Confirm that the platform tools directory (created when installing ADB and Fastboot) is included in your computer's path environment variable. For Windows, use the command line:
    ```
    set path=%path%;<platform tools path>
    ```
2. Download the latest firmware/image released by Altek (website link TBA)

3. Extract the contents of the .TGZ file downloaded. If you end up with a .TAR file, extract the contents of this file as well. You should end up with more than 120 files located in the final extraction folder.

4. Download [FastBootUpgrade.bat]({{ '/Needed/FastbootUpgrad.zip' | relative_url }}) and extract it into the directory you extracted the firmware files to.

5. To verify the camera is attached and recognized, run the following in a command prompt:
    ```
    adb devices
    ```

6. Run FastBootUpgrade.bat

7. Follow the instructions given, the camera will update and reboot when the process is complete.
    * If you get stuck at the message *waiting for device*, please reboot the camera hardware and run FastBootUpgrade.bat again. If you keep hitting the same message, please charge the device for 10+ minutes to make sure that the battery is charged.

8. To confirm your device has accepted the updated firmware, check the version by running the following in a command prompt:
    ```
    adb shell cat /etc/version
    ```