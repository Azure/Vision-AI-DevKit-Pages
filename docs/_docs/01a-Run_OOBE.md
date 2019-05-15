---
title: "Setup the Vision AI DevKit camera"
permalink: /docs/Run_OOBE/
excerpt: "Run OOBE (Ouf-Of-Box-Experience) - Connect device to WiFi and IoT Hub"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---
## What you will do

- Configure the Vision AI DevKit for your Wi-Fi network.
- Configure the Vision AI DevKit as an IoT Edge devic ein your Azure IoT Hub.

## What will you need

- A configured Azure IoT Edge device within Azure IoT Hub.
- The IoT Edge device connection string.
  - This is the string you recieved while configuring [Azure Resources]({{ '/docs/Setup_Azure_resources/' | relative_url }}).

{% include_relative OOBE.md %}