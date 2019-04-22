---
title: "Configure Azure IoT Hub and IoT Edge device"
permalink: /docs/Setup_Azure_resources/
excerpt: "Set up your Azure account, IoT Hub and IoT Edge device for Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

## What you will do

* Create an Azure IoT Hub instance
* Associate the Vision AI DevKit as as an IoT Edge Device

### Azure IoT Hub

Azure IoT Hub enables reliable and secure bi-directional communications between devices and a solution back end. You will need to create a new or use an existing Azure IoT Hub instance to work with the Vision AI DevKit.

#### [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}

### Azure IoT Edge device

To use your Vision AI DevKit hardware with Azure IoT Hub for Edge workloads, you will need to register the hardware as an IoT Edge device. Upon registration, you are provided a connection string you will use during Vision AI DevKit hardware setup. Please ensure you make copy the string somewhere you can refer to.

#### [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes

- When creating an IoT Edge device in the Azure portal, avoid using a device name you may have used previously.
- Each hardware device you connect to Azure IoT Hub must use a unique connection string.
- You may use any IoT Hub Region available in the Azure portal.
