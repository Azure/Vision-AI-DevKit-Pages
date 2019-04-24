---
title: "Firmware update"
permalink: /docs/Firmware/
excerpt: "Downloading and updating Vision AI Dev Kit hardware firmware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

## What you will do

* Verify connectivity between your computer and the Vision AI Dev Kit hardware
* Update the Vision AI Dev Kit firmware

## What you will need

* Vision AI Dev Kit hardware
* USB-C cable
* Installed ADB (Android Debug Bridge) and Fastboot tool. (See [Platform Tools]({{ '/docs/platform_tools' | relative_url}}) for installation instructions.)

## Verify hardware connection

1. Connect your computer and the Vision AI Dev Kit camera using a USB-C cable
2. Open a command line prompt on your computer and use the command

     ```cmd
     adb devices
     ```

    You should see output similar to this, if your computer and camera are connected properly:  

         C:\Tools>adb devices
         List of devices attached  
         efb99xxx        device  

    If you do not see the device, try rebooting the camera hardware using one of these methods:

    * Click the reset button once, using the pin hole on the right side of the camera.
    * Press the power button on the back once.
    * Use the command line:

        ```cmd
        adb reboot
        ```

    * Long press the power button for more than 12 seconds, to force a power down of the hardware. Then hold the power button for more than 12 seconds again to power up the hardware.

## Firmware Update

The Vision AI Dev Kit hardware **must be charged for at least 10 minutes or have greater than 50% charge** (using a 2A charger) before starting the firmware flashing process.

### Downloading and Extracting the latest Device Firmware

1. Confirm that the platform tools directory (created when installing ADB and Fastboot) is included in your computer's path environment variable. For Windows, use the command line:

    ```cmd
    set path=%path%;<platform tools path>
    ```

2. Download the latest firmware/image released by Altek *(website link TBD)* [*(Internal-only Microsoft link)*](https://microsoftapc.sharepoint.com/teams/Selfhost-VisionAIDevKit/Shared%20Documents/General/Altek%20FW%20Image/NextUnderTest)

3. Extract the contents of the .TGZ file downloaded. If you end up with a .TAR file, extract the contents of this file as well. You should end up with more than 120 files located in the final extraction folder.

4. Download [FastBootUpgrade.bat]({{ '/Needed/FastbootUpgrad.zip' | relative_url }}) and extract it into the directory you extracted the firmware files to.

### Updating the firmware

1. To verify the camera is attached and recognized, run the following command line:

    ```cmd
    adb devices
    ```

2. Run FastBootUpgrade.bat

3. Follow the instructions given by the batch file. The camera will update and reboot when the process is complete.
    * If you get stuck at the message *waiting for device*, please reboot the camera hardware and run FastBootUpgrade.bat again. If you keep hitting the same message, please charge the device for 10+ minutes to make sure that the battery is charged to at least 50%.

4. To confirm your device has accepted the updated firmware, check the version using this command line:

    ```cmd
    adb shell cat /etc/version
    ```
