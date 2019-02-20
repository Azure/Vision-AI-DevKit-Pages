---
title: "Get started"
permalink: /docs/01-Get_Started/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-11
---
For first-time users of the **Vision AI DevKit**, this page will help you get your device ready for use.

![Get Started]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## What you will do
* Configure an **Azure IoT Hub**
* Configure your PC to connect to the Vision AI Development Kit’s Wi-Fi access point
* Connect your Vision AI Dev Kit camera to your Azure IoT Hub

## What you will need
* Vision AI Dev Kit camera hardware
* IoT Edge Device connection String
* An active Azure subscription. [Activate a free Microsoft Azure account.](https://azure.microsoft.com/en-us/free/){:target="_blank"}.

## Prepare your hardware
The Vision AI Dev Kit hardware **must be charged for at least 10 minutes** (using a 2A charger) before starting the configuration process.

## Obtain an Azure IoT Edge connection string
You will need an Azure IoT Edge connection string to connect your camera to Microsoft Azure. The connection string is created when you create an IoT Hub and register your Vision AI DevKit hardware as the configured IoT Edge device.

1. [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"}
2. [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}

### Notes
- When creating your IoT Edge device in the Azure portal, avoid using a device you may have used previously.
- Do not reuse a connection string for multiple devices.
- You may use any IoT Hub Region which is available in the Azure portal.

## Connect your PC to the Visual AI DevKit Wi-Fi access point
When you first power up the Visual AI DevKit hardware, or connect it to a charger, you will see three Red LED lights. The LED will start flashing within 10 seconds of power up to indicate that the device is ready to accept a Wi-Fi connection.

1. From your PC, look for a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D).
2. Connect to the MSIOT_xxxxxx Wi-Fi access point.
	* Check the label at the bottom of the device whether there is a default passphrase. If there is no label, see the Troubleshooting Section.

### Notes
- If your device LEDs are not flashing RED, review the Troubleshooting section below.
- If you have connected your device to a display via the HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

## Connect the Vision AI Dev Kit to your Azure IoT Hub
* Use a browser to visit [http://setupaicamera.ms](http://setupaicamera.ms){:target="_blank"}.
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
