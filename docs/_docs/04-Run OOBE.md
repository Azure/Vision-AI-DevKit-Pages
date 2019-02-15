---
title: "Run OOBE"
permalink: /docs/Run_OOBE/
excerpt: "Run OOBE (Ouf-Of-Box-Experience) - Connect device to WiFi and IoT Hub"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-11
---
## Connect your PC to the Visual AI DevKit Wi-Fi access point
When you first power up the Visual AI DevKit hardware, or connect it to a charger, you will see three Red LED lights. The LED will start flashing within 10 seconds of power up to indicate that the device is ready to accept a Wi-Fi connection.

1. From your PC, look for a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D).
2. Connect to the MSIOT_xxxxxx Wi-Fi access point.
	* Check the label at the bottom of the device whether there is a default passphrase. If there is no label, see the Troubleshooting Section.

### Notes
- If your device LEDs are not flashing RED, review the Troubleshooting section below.
- If you have connected your device to a display via the HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

## Connect the Vision AI Dev Kit to your Azure IoT Hub
* Use a browser to visit [http://setupaicamera.ms](http://setupaicamera.ms).
	* If you do not see the below screen, verify that your computer is connected to the reference hardware's access point. 

![Vision AI Developer Kit starting screen]({{ '/assets/images/visual-ai-getting-started-screen.png' | relative_url }})

* Tap **Next** to open the SSH configuration screen.

![Vision AI Developer Kit SSH config screen]({{ '/assets/images/SSH_setup.png' | relative_url }})

* Tap **Next** to open the Wi-Fi configuration screen.

![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Wi-Fi_settings.png' | relative_url }})

Select the Wi-Fi network your camera will connect to from the drop down, then enter the access password.

### Notes
- The Wi-Fi access password cannot have spaces, or the camera will be unable to connect to the Wi-Fi network. You will see a confirmation screen when the camera successfully connects to your selected Wi-Fi network.

* Tap **Next**  to open the 'Connect to Microsoft Azure' screen.

![Vision AI Developer Kit Connect to Azure screen]({{ '/assets/images/Connect_to_Azure.png' | relative_url }})

* Insert the IoT Edge connection string created for your IoT Edge device previously. You will see the below 'connecting' screen, followed by the 'connected' screen (also below).

![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connecting.png' | relative_url }})

![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connected.png' | relative_url }})