---
title: "Quick Start"
permalink: /docs/quick_start/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-02
---
This guide will start you on your vision AI journey with the **Vision AI DevKit**, taking you from setting up your Microsoft Azure account to seeing video output of recognized objects by the DevKit camera. We will use a VisionSample model for this process, which has been trained to recognize up to 183 different objects.

  ![Flow chart of the steps taken for the first use of the Vision AI Dev Kit, covered in the 'What you will do' section of this document]({{ '/assets/images/new_OOBE_flow.PNG' | relative_url }})

## What you will do

- Connect the Vision AI DevKit camera to Wi-Fi
- Create necessary Azure IoT resources (Resource Group, IoT Hub, IoT Edge device)
- Connect the Vision AI DevKit camera to a created IoT Edge Device
- See video output from the camera to a connected monitor or connected video streaming client

## What you will need

- Active Azure account
- Vision AI DevKit camera hardware
- Monitor supporting HDMI input with an HDMI cable (do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}

## Configure your DevKit

### Azure account

The Vision AI DevKit is configured to work with Microsoft Azure IoT resources. To get started, you will need a new or existing Azure account. You can create a free account by visiting this link: [https://azure.microsoft.com/free](https://aka.ms/azureaccount/){:target="_blank"}.

## Setup your DevKit camera

These steps will configure your DevKit camera for Wi-Fi and connect the the camera to the IoT Edge device you created earlier in Azure IoT Hub.

{% include_relative OOBE.md %}

## View DevKit camera output

You can view the DevKit camera output with a web browser, using the URL given on the final device setup page. You can also connect an HDMI montior to the HDMI port on the camera directly or a video playback application (such as VLC Player) that supports RTSP video. Note: If using a cable, there should be no adapters at either end.

For more information on using RTSP streaming, see the topic [**View RTSP video stream**]({{ '/docs/RTSP_stream/#connect-to-the-video-stream' | relative_url }}){:target="_blank"}.

## Basic setup

After setting up the device, you will have a following setup.



## Next steps

In this quick start, you configured the Vision AI DevKit camera to display output for objects recognized by the VisionSample model to a monitor or RTSP capable video player.

From here, your next step is to create and deploy a custom vision ML model using the Azure Custom Vision service.

[Create and deploy a vision ML model using the Azure Custom Vision service]({{ '/docs/Tutorial-HOL_Using_the_VisionSample/' | relative_url }}){:target="_blank"}
