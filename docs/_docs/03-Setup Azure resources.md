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

## Creating IoT Hub and IoT Edge
Vision AI Dev Kit communicates with the Azure Cloud using IoT Hub and Vision AI Dev Kit needs to be associated with IoT Hub as an IoT Edge Device. You can use an existing IoT Hub instance if you have one and create a new IoT Edge device under that one as well.

There will be a connection string given to IoT Edge device that you'll need as an input when running OOBE where you define to which IoT Hub instance the device connects to.

1. [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}
2. [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes
- When creating your IoT Edge device in the Azure portal, avoid using a device you may have used previously.
- Do not reuse a connection string for multiple devices.
- You may use any IoT Hub Region which is available in the Azure portal.
