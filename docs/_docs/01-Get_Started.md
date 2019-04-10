---
title: "Quick Start Guide"
permalink: /docs/Get_Started/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

For first-time users of the **Vision AI DevKit**, this page will help you get your device ready for use. All the instructions for steps introduced in page can be found from the left side menu.

## Initial setup

* There are a few steps to take in order to get the Vision AI Dev Kit set up.
* The picture below illustrates the steps and the dependencies between them.
* Initial setup also includes deploying VisionSample that is an example module with image recognition capabilities built in.

    ![High level steps to take for the initial Vision AI Dev Kit setup]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## [Platform Tools]({{ '/docs/platform_tools/' | relative_url }})

You will need an installation of platform tools, which include the Android Debug Bridge (ADB) and Fastboot. These tools are used for checking device connectivity and running various command-line tasks included firmware updates.

## [Firmware Update]({{ '/docs/Firmware/' | relative_url }})

Although not absolutely mandatory we strongly recommend you to check the firmware version of you device and update it to latest version if needed before starting to use Vision AI Dev Kit.

## [Azure account, Azure IoT Hub and IoT Edge]({{ '/docs/Setup_Azure_resources/' | relative_url }})

The Azure IoT Hub portal and a configured IoT Edge device are used for deployment of machine learning and other modules and control of data traffic between your device and the cloud. Use of these tools requires an active Azure account.

## [OOBE (Out-of-Box Experience)]({{ '/docs/Run_OOBE/' | relative_url }})

All the steps described above are pre-requisites for OOBE, even though some of them can be completed independent from each other. During OOBE, you will link your device with correct Azure IoT Hub and configure its Wi-Fi access.

## Post-OOBE

Once OOBE is complete, your camera device is ready to receive modules, such as the VisionSample ML module (providing example image recognition capabilities.) Modules can be deployed via [VS Code](https://code.visualstudio.com/), [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/) or from [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps).

## [Deploying a model using IoT Hub]({{ '/docs/Deploy_Model_IoT_Hub/' | relative_url }})

This section provides instructions for deploying the VisionSample model to your device using IoT Hub. This step can also be pre-configured during the IoT Hub and IoT Edge device setup prior to running OOBE.

## Setting up your SW development environment

There are several ways to train machine learning models and develop additional logic for the Vision AI Dev Kit. We highly recommend using [Visual Studio (VS) Code](https://code.visualstudio.com).

## [Deploying a model using VS Code]({{ '/docs/Deploy_Model_VS_Code/' | relative_url }})

This section provides instructions for deploying the VisionSample model to your device using VS Code
