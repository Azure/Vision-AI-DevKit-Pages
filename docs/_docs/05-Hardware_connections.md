---
title: "Hardware Connections"
permalink: /docs/Hardware_connections/
excerpt: "Verify hardware connections between the Vision AI DevKit hardware and your computer."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-10
---

## What you will do

* Connect to a computer
* Connect to a computer monitor

## What you will need

* Vision AI DevKit camera hardware
* Vision AI DevKit power supply
* USB-C cable
* HDMI Cable
* Monitor with HDMI port
* ADB command line utility. ([instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})

## USB connection

The Vision AI DevKit camera hardware has a USB-C connector for connection with a computer.

### USB port use cases

* Updating the Vision AI DevKit hardware firmware
* Using ADB (Android Device Bridge) commands to control and obtain status from the Vision AI DevKit hardware via command line parameters

### Connecting and verifying the USB connection to a computer

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

## Monitor connection

The Vision AI DevKit can send the output of camera inferencing to a monitor directly connected to the camera hardware using the HDMI port.

### Monitor requirements

* Your display must have a minimum resoltion of 1080p.
* The HDMI cable connecting the Vision AI DevKit to the monitor cannot have any port adapters attached.
* Televisions or gaming specific monitors may not be recognized by the Vision AI DevKit.

### Connecting and verifying the HDMI monitor connection

Connect the HDMI cable to the HDMI port on both the Vision AI DevKit hardware and your monitor. Your monitor will start to display the camera video, with bounding boxes drawing around recognized objects, a few minutes after your model is deployed to the camera.

### Notes

* The object label presented in the bounding box may appear incorrect. If a new object appears in the space befor the bounding box is drawn, the label of the last object detected will be presented. This is not an inferencing bug.
