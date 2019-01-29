---
title: "Get started"
permalink: /docs/get-started/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-01-28
---
For first-time users of the Vision AI DevKit, this page will help you get your device ready for use.

{% include toc icon="columns" %}

## What you will learn
* Configure an Azure IoT Hub
* Configure an IoT Edge Device connection string
* Configure your development system to connect to the Vision AI Development Kit’s WiFi access point
* Deploy a pre-built sample module through the Azure portal

## What you will need
* Vision AI Dev Kit hardware
* HDMI cable
* Monitor with an HDMI input connector
* An active Azure subscription. [Activate a free Microsoft Azure account with 12 months of free services.](https://azure.microsoft.com/en-us/free/).
* A configured Azure IoT Hub

## Prepare your hardware
The Vision AI Dev Kit hardware must be charged for at least 10 minutes (using a 2A charger) before starting the configuration process.

## Obtaining an Azure IoT Edge connection string
You will need an Azure IoT Edge connection string to connect your camera to Microsoft Azure.  The connection string will be created after you create and IoT Hub and register your Vision AI DevKit as a configured IoT Edge device.

1. [Create an IoT hub using the Azure portal](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal)
2. [Register a new Azure IoT Edge device from the Azure portal](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal)

### Notes
1. When creating your IoT Edge device in the Azure portal, avoid using a device you may have used previously.
2. Do not reuse a connection string for multiple devices.
3. You may use any IoT Hub Region which is available in the Azure portal.

## Connect your PC to the Visual AI DevKit Wi-Fi access point
When you first power up the Visual AI DevKit hardware, or connect it to a charger, you will see three Red LED lights. The LED will start flashing within 10 seconds of power up to indicate that the device is ready to accept a Wi-Fi connection.
	Note 1: If your device LEDs are not flashing RED, review the Troubleshooting section below.
	Note 2: If you have connected your device to an HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

1. From your PC, look for a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the devices WiFi mac address, e.g. MSIOT_BD097D).
2. Connect to the MSIOT_xxxxxx Wi-Fi access point.
	* Check the label at the bottom of the device whether there is a default passphrase. If there is no label, see the Troubleshooting Section.

## Connect the Vision AI Dev Kit to your Azure IoT Hub
1. Use a browser to visit [http://setupaicamera.ms](http://setupaicamera.ms).
	* If you do not see the below screen, verify that your computer is connected to the reference hardware's access point. 

![Vision AI Developer Kit starting screen]({{"/docs/assets/images/visual-ai-getting-started-screen.png" | relative_url }})
