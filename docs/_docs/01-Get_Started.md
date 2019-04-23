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

For first-time users of the **Vision AI DevKit**, the links below will take you from setting up your Azure account to seeing video output showing recognized objects using the VisionSample model.

  ![High level steps to take for the initial Vision AI Dev Kit setup]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## Setup an Azure account

### Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)

if you don't alrdy have an Azure subscription.

## Setup Azure IoT Hub and IoT Edge device

Azure IoT Hub enables reliable and secure bi-directional communications between devices and the solution back end. To use your Vision AI DevKit hardware with Azure IoT Hub for edge workloads, you will need to register your DevKitas an IoT Edge device. During registration, you are provided a connection string. You will use this string during the DevKit hardware setup. Please ensure you make copy the string somewhere you can refer to.

### [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}

### [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

## Setup your DevKit

During device setup, you will link your DevKit with your configured Azure IoT Hub (using the IoT Edge device connection string obtained earlier), as well as connect the device to Wi-Fi.

### [DevKit setup]({{ '/docs/Run_OOBE/' | relative_url }})

## Deploy the VisionSample model

Once device setup is complete, you are ready to deploy the VisionSample ML model to the DevKit.

### [Deploy the sample model]({{ '/docs/Deploy_Model_IoT_Hub/' | relative_url }})

## See objects being recognized

Once the VisionSample model is deployed, and a monitor is connected to the HDMI port on your DevKit, you should see bounding boxes drawn around recognized objects in the field of view of your DevKit's camera.
