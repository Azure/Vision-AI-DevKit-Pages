---
title: "Firmware update"
permalink: /docs/Firmware/
excerpt: "Downloading and updating Vision AI Dev Kit hardware firmware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-07-03
---

## What you will do

* Verify connectivity between your computer and the Vision AI Dev Kit hardware
* Update the Vision AI Dev Kit firmware

## What you will need

* Vision AI Dev Kit hardware
* USB-C cable
* Previously installed Platform Tools (ADB command line utility and Fastboot tool) ([instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})

## Verify hardware connection

1. Connect your computer and the Vision AI DevKit camera using a USB-C cable.
2. Open a command line prompt on your computer, then use the command line:

     ```terminal
     adb devices
     ```

    You should see output similar to this, confirming your computer and DevKit are connected properly:  

    ```terminal
    C:\Tools>adb devices
    List of devices attached  
    efb99xxx        device
    ```  

    If your DevKit is not listed, try rebooting the camera hardware using one of these methods:

    * Click the reset button once, using the pin hole on the right side of the camera.
    * Press the power button on the back once.
    * Use the command line:

        ```terminal
        adb reboot
        ```

    * Long press the power button for more than 12 seconds, to force a power down of the hardware. Then hold the power button for more than 12 seconds again to power up the hardware.

## Updating the firmware

The Vision AI Dev Kit hardware **must be at least 50% charged** before starting the firmware flashing process.

### Download and extract the latest firmware

1. Confirm that the platform tools directory (containing the ADB and Fastboot utilities) is included in your computer's path environment variable. For Windows, use the command line:

    ```terminal
    set path=%path%;<platform tools path>
    ```

2. Download the latest firmware released by Altek for the Vision AI DevKit - [Latest Firmware](https://store.altek.com.tw/qualcomm/downloads/Azure-IoT-Starter-Kit)

3. Extract the contents to a directory on your computer.

4. Download [FastBootUpgrade.bat]({{ '/Needed/FastbootUpgrad.zip' | relative_url }}) and extract it into the same directory as the firmware from the previous step.

### Update the firmware

1. Run FastBootUpgrade.bat

2. Follow the instructions given by the batch file. The camera will update and reboot when the process is complete.
    * If you get stuck at the message *waiting for device*, please reboot the DevKit and run FastBootUpgrade.bat again.

3. To confirm your device has accepted the updated firmware, check the version using this command line, after the DevKit has rebooted:

    ```ternunal
    adb shell cat /etc/version
    ```
