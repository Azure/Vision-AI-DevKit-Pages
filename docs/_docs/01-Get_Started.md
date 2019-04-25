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

### Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F){:target="_blank"}

if you don't already have an Azure subscription.

## Setup Azure IoT Hub and IoT Edge device

[Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub){:target="_blank"} enables reliable and secure bi-directional communications between devices and a cloud-hosted solution back end. To use your Vision AI DevKit hardware with Azure IoT Hub for edge workloads, you will need to register your DevKit as an IoT Edge device. During registration, you are provided a connection string. You will use this string in the section **Setup your DevKit**. Please ensure you make copy the string somewhere you can refer to.

### [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal#create-an-iot-hub){:target="_blank"}

### [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal#create-a-device){:target="_blank"}

## Configure the Vision AI DevKit

As you configure your DevKit for use, you will connect the device to your Wi-Fi network, then link the hardware with the Azure IoT Hub you configured, using the IoT Edge device connection string you were provided in the previous step.

### [DevKit setup]({{ '/docs/Run_OOBE/' | relative_url }})

## Deploy the VisionSample model

Once device configuration is complete, you are ready to deploy the VisionSample ML model to the DevKit.

### [Deploy the sample model]({{ '/docs/Deploy_Model_IoT_Hub/' | relative_url }})

## See objects being recognized

Once the VisionSample model is deployed, and a monitor is connected to the HDMI port on your DevKit, you should see bounding boxes drawn around recognized objects in the field of view of your DevKit's camera.
