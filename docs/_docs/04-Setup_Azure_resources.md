---
title: "Setup Azure resources"
permalink: /docs/Setup_Azure_Resources/
excerpt: "Set up your Azure account, IoT Hub and IoT Edge for Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-13
---

## Creating IoT Hub and IoT Edge instances

The Vision AI Dev Kit will need to be associated with [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/) as an IoT Edge Device to utilized Azure services. You can use an existing Azure IoT Hub instance, or create a new one for your Vision AI project.

A connection string will be given to the IoT Edge device which you will use as an input when running OOBE, when you define the IoT Hub instance the device will connect to.

1. [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}
2. [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes

- When creating an IoT Edge device in the Azure portal, avoid using a device name you may have used previously.
- Do not use a single connection string for multiple devices.
- You may use any IoT Hub Region available in the Azure portal.
