---
title: "Run OOBE"
permalink: /docs/Run_OOBE/
excerpt: "Run OOBE (Ouf-Of-Box-Experience) - Connect device to WiFi and IoT Hub"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-13
---
## What you will do
- Configure your device to connect to WiFI
- Configure your device to connect to Azure IoT Hub

## What will you need
- An configured Azure IoT Hub
- IoT Edge device connection string for your device

## Connect your PC to the Visual AI DevKit hardware Wi-Fi access point
On initial power up, you will see three Red LED lights. The LEDs will start flashing within 10 seconds of power up, indicating the device is in Wi-Fi access point mode.

1. From your PC, look for a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D).
2. Connect to the MSIOT_xxxxxx Wi-Fi access point.
  * Check the label at the bottom of the device to identify the default Wi-Fi AP passphrase. If there is no label, see [Troubleshooting]({{ '/docs/troubleshooting/' | relative_url }}).

### Notes
- If your device LEDs are not flashing RED, review the [Troubleshooting]({{ '/docs/troubleshooting/' | relative_url }}) section.
- If you have connected your device to a display via the HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

## Connect the Vision AI Dev Kit hardware to your Azure IoT Hub

1. Use your computer's web browser to visit [http://setupaicamera.ms](http://setupaicamera.ms){:target="_blank"}.
  * If you do not see the below screen, verify your computer is connected to the Dev Kit hardware's access point.

    ![Vision AI Developer Kit starting screen]({{ '/assets/images/visual-ai-getting-started-screen.png' | relative_url }})

2. Tap **Next** to open the SSH configuration screen.
    ![Vision AI Developer Kit SSH config screen]({{ '/assets/images/SSH_setup.png' | relative_url }})

3. Tap **Next** to open the Wi-Fi configuration screen.  
    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Wi-Fi_settings.png' | relative_url }})

4. Select the Wi-Fi network your camera will connect to from the drop down box, then enter the Wi-Fi passphrase. You will see a confirmation screen when the camera successfully connects to your selected Wi-Fi network.

    * The Wi-Fi passphrase cannot have spaces (even at the end of the passphrase string), or the camera will be unable to connect to the Wi-Fi network. 

5. Tap **Next** to open the **Connect to Microsoft Azure** screen.

![Vision AI Developer Kit Connect to Azure screen]({{ '/assets/images/Connect_to_Azure.png' | relative_url }})

6. Enter the IoT Edge connection string created for your IoT Edge device previously. You will see the below **connecting** screen, followed by the **connected** screen (also below).

![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connecting.png' | relative_url }})

![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connected.png' | relative_url }})
