---
title: "OOBE"
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

- Configure your device to connect to WiFI.
- Configure your device to connect to Azure IoT Hub using the IoT Edge device you configured in [Azure Resources.]({{ '/docs/Setup_Azure_resources/' | relative_url }})

## What will you need

- A configured Azure IoT Hub, with a configured Azure IoT Edge device for use with your Vision Ai DevKit hardware
- IoT Edge device connection string for your device.
  - This is the string obtained in [Azure Resources.]({{ '/docs/Setup_Azure_resources/' | relative_url }})

## Connect your PC to the Visual AI DevKit hardware Wi-Fi access point

Within 10 seconds of initial power up, you will see three Red LED lights. This indicates the device is in Wi-Fi access point mode. If your device LEDs are not flashing RED, review [Troubleshooting and Tips.]({{ '/docs/troubleshooting/' | relative_url }})

From your PC, connect to a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D).

### Notes

- The label at the bottom of the device will have the default Wi-Fi access point passphrase. If there is no label, see [Troubleshooting and Tips]({{ '/docs/troubleshooting/' | relative_url }}).
- If you have connected your device to a display via the HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

## Connect the Vision AI Dev Kit hardware to your Azure IoT Hub

1. Use your computer's web browser to visit [http://setupaicamera.ms](http://setupaicamera.ms){:target="_blank"}. If you do not see the below screen, verify your computer is connected to the Dev Kit hardware's access point.
    ![Vision AI Developer Kit starting screen]({{ '/assets/images/visual-ai-getting-started-screen.png' | relative_url }})

2. Tapping **Next** will open the SSH configuration screen, where you will enter the device's Wi-Fi access point passphrase.
    ![Vision AI Developer Kit SSH config screen]({{ '/assets/images/SSH_setup.png' | relative_url }})

3. Tapping **Next** will open the Wi-Fi configuration screen. where you will connect your Vision AI DevKit to the Wi-Fi network it will use during normal operation.
    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Wi-Fi_settings.png' | relative_url }})
    - Select the Wi-Fi network your camera will connect to from the drop down box, then enter the Wi-Fi passphrase. You will see a confirmation screen when the camera successfully connects to your selected Wi-Fi network.
    - The Wi-Fi passphrase cannot have spaces (even at the end of the passphrase string), or the camera will be unable to connect to the Wi-Fi network.

4. Tapping **Next** will open the **Connect to Microsoft Azure** screen, where you will add the IoT Edge Connection String.
    ![Vision AI Developer Kit Connect to Azure screen]({{ '/assets/images/Connect_to_Azure.png' | relative_url }})

5. Tapping **Next** will take you to the **connecting** and **connected** screens.
    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connecting.png' | relative_url }})

    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connected.png' | relative_url }})
