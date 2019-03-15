---
title: "Azure Resources"
permalink: /docs/Setup_Azure_resources/
excerpt: "Set up your Azure account, IoT Hub and IoT Edge for Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

## Configuring Azure resources for use with the Vision AI DevKit

The Vision AI Dev Kit will need to be associated with [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/) as an IoT Edge Device to utilize Azure services. You can use an existing Azure IoT Hub instance, or create a new one for your Vision AI project.

### Using Azure IoT Hub

Azure IoT Hub enables reliable and secure bi-directional communications between devices and a solution back end. You will need to create a new or use an existing Azure IoT Hub instance to work with the Vision AI DevKit. These instructions cover creating a new IoT Hub instance:

#### [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}

### Register the Vision AI Dev Kit hardware as an Azure IoT Edge device

Before you can use your Vision AI DevKit hardware with Azure IoT Edge, you will need to register it with your IoT hub. Once you register the device, you receive a connection string which will be used when running OOBE, where you set up the DevKit hardware for Edge workloads. Use these instructions:

#### [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes

- When creating an IoT Edge device in the Azure portal, avoid using a device name you may have used previously.
- Each hardware device you connect to Azure IoT Hub must use a unique connection string.
- You may use any IoT Hub Region available in the Azure portal.
