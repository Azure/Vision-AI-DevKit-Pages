---
title: "Setup Azure resources"
permalink: /docs/Setup_Azure_Resources/
excerpt: "Set up your Azure account, IoT Hub and IoT Edge for Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-11
---

## Obtain an Azure IoT Edge connection string
You will need an Azure IoT Edge connection string to connect your camera to Microsoft Azure. The connection string is created when you create an IoT Hub and register your Vision AI DevKit hardware as the configured IoT Edge device.

1. [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}
2. [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes
- When creating your IoT Edge device in the Azure portal, avoid using a device you may have used previously.
- Do not reuse a connection string for multiple devices.
- You may use any IoT Hub Region which is available in the Azure portal.
