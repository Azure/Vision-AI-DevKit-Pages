---
title: "Quick Start"
permalink: /docs/Get_Started/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---

For first-time users of the **Vision AI DevKit**, the links here will help you get your device ready to go and deploy the VisionSample model from GitHub.

## Azure account and hardware setup

  ![High level steps to take for the initial Vision AI Dev Kit setup]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## [Azure account and Azure IoT Hub with IoT Edge device]({{ '/docs/Setup_Azure_resources/' | relative_url }})

The Azure IoT Hub portal with a configured IoT Edge device is used for deploying models and control of data traffic between your device and the cloud. Note: these tools require an active Azure account.

## [Setup your device]({{ '/docs/Run_OOBE/' | relative_url }})

During device setup, you will link your device with your configured Azure IoT Hub, as well as connect the device to Wi-Fi.

## Deploy the VisionSample model

Once device setup is complete, you are ready to deploy models to the device, such as the VisionSample ML model. Deployment can be done using [Visual Studio Code](https://code.visualstudio.com/), [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/) or from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps).

## [Deploy the sample model using IoT Hub]({{ '/docs/Deploy_Model_IoT_Hub/' | relative_url }})

## [Deploy the sample model using Visual Studio Code]({{ '/docs/Deploy_Model_VS_Code/' | relative_url }})
