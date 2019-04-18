---
title: "Connect to the live video stream"
permalink: /docs/RTSP_stream/
excerpt: "Connect to the live RTSP video stream"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-18
---
## What you will do

* Obtain the IP address of the Vision AI DevKit
* View the live video stream from the Vision AI DevKit hardware

## What you will need

* Sample model or other vision model deployed to the Vision AI DevKit
* Media player supporting the RTSP protocol ([VLC Player](https://www.videolan.org/vlc/) or similar)
* PC and Vision AI DevKit connected to the same network

## Obtain the IP address of the Vision AI DevKit

### Using ADB shell

```
ADB Shell
ifconfig wlan0
```

### Using Azure IoT Hub

  1. Go to your device in Azure IoT Hub and select the model deployed on your device. (This example uses the VisionSample model.)
    ![Azure IoT Hub Edge device screen with model file highlighted]({{ '/assets/images/VisionSample_IoTHub2.png' | relative_url }})

  2. Click ***Module Identity Twin***
    ![Azure IoT Hub Edge device screen with Module Identity Twin highlighted]({{ '/assets/images/ModuleIdentityTwin.png' | relative_url }})

  3. Copy the IP address found in the Azure module.
    ![IP address highlighted in Module Identity Twin screen]({{ '/assets/images/IP_Address_Module_Identity_Twin.png' | relative_url }})

## Connect to the video strea
Any media player supporting the RTSP protocol can be used to display the live video stream from the Vision AI DevKit. (This example will use VLC Media Player.)

1. Open VLC Media Player, select the ***Media*** tab, then select ***Open Network Stream***.

    ![IP address high-lighted in Module Identity Twin sceen]({{ '/assets/images/VLC_Media_menu.png' | relative_url }})

2. Enter the RTSP address in the form

    ```
    http://<IP address>:8000/live
    ```
under on the ***Network*** tab, then select ***Play***.

    ![VLC Open Media dialog box]({{ '/assets/images/VLC_RTSP_Dialog.png' | relative_url }})
