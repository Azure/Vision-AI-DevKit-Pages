[//]: # (This is an include file of the OOBE proecess)

### Connect your PC to the camera's Wi-Fi access point

- Within 10 seconds of first power up, you should see three flashing RED LED lights. This indicates the device is in Wi-Fi access point mode. If your device is not flashing RED, press the power button for 5 seconds to turn on the DevKit hardware access point.

{% include_relative Device_LEDs.md %}

- From your PC, connect to a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi MAC address, e.g. MSIOT_BD097D).

#### Notes

- The label at the bottom of the device will have the default Wi-Fi access point password. If there is no label, see [Troubleshooting Wi-Fi Issues]({{ '/docs/Wi-Fi_issues/' | relative_url }}).
- If you have connected your device to a display via the HDMI port, the display will show a gray pattern. You will not see any text or images on your display until the IoT Edge runtime has been deployed to the device.

### Configure the camera for your Wi-Fi network

1. Use your computer's web browser to visit [http://setupaicamera.ms](http://setupaicamera.ms){:target="_blank"}. If you do not see the below screen, verify your computer is connected to the Dev Kit hardware's access point.

    ![Vision AI Developer Kit starting screen]({{ '/assets/images/vision-ai-getting-started-screen.png' | relative_url }})

2. Tapping **Next** will open the SSH configuration screen, where you can create a new Wi-Fi access point passphrase for the camera, if desired. All settings can be left at their defaults.

    ![Vision AI Developer Kit SSH config screen]({{ '/assets/images/SSH_setup.png' | relative_url }})

3. Tapping **Next** will open the Wi-Fi settings page, where you will connect your Vision AI DevKit to the Wi-Fi network it will use during normal operation.

    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Wi-Fi_settings.png' | relative_url }})
    - Select the Wi-Fi network your camera will connect to from the drop down box, then enter the Wi-Fi passphrase. You will see a confirmation screen when the camera successfully connects to your selected Wi-Fi network.
    - The Wi-Fi passphrase cannot have spaces (even at the end of the passphrase string), or the camera will be unable to connect to the Wi-Fi network.

4. Tapping **Next** will take you to the **connecting** and **connected** screens.

    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connecting.png' | relative_url }})

    ![Vision AI Developer Kit Wi-Fi Settings screen]({{ '/assets/images/Connected.png' | relative_url }})

### Configure your camera to connect to Azure as an IoT Edge device

Tapping **Next** starts the process of creating the necessary Azure resources, then connecting the camera to these resources.

1. You will see the following screen. You should copy the device code for use in the next step.

    ![Result screen presenting your unique device code for connection to Azure IoT]({{ '/assets/images/Device_String.png' | relative_url }})

    Note: If you already have an Azure IoT Edge device connection string associated with the Vision AI Dev Kit, click the `Already have a connection string?' link and enter that connection string. However, in order to get the full first use experience, the existing connection string must have been used with Vision AI Dev Kit device arlier. A different IoT Edge connection string will not load the default vision sample module to the device.

2. Tap **Next** and insert the device code you received in the previous screen.

    ![Dialog box for inserting the unique device code into]({{ '/assets/images/Enter_Code.png' | relative_url }})

3. You should reach the following screen when your code is accepted. (Press 'OK' to close the pop-up message, if seen.)

    ![Screen confirming connection to Azure, then allowing selection of your Azure account]({{ '/assets/images/Connected_to_Azure.png' | relative_url }})

    - Use the `Switch directory` link to choose the GUID of your Azure account.
    - Use the `Select your IoT Hub` link to choose an existing IoT Hub, or create a new one.

4. Click **Next**, then input a name for your DevKit camera in this screen.

    ![Dialog box for inputing a name for the DevKit camera]({{ '/assets/images/Name_the_Camera.png' | relative_url }})

    - Click **Next** and you should see the following screen:

        ![Screen showing the camera downloading the Azure IoT Edge runtime]({{ '/assets/images/Downloading_Runtime.png' | relative_url }})
    - You will see the following screen showing your DevKit camera is ready to recognize objects.
    
        ![Screen confirming camera is setup and providing the RTSP string for viewing camera output over the wire]({{ '/assets/images/Camera_Setup_Complete.png' | relative_url }})
