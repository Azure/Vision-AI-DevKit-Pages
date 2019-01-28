---
---
![](media/image1.jpeg){width="6.5in"
height="2.8125in"}![](media/image2.png){width="2.0104166666666665in"
height="3.0625in"}

Welcome to the Vision AI Development Kit! This document has instructions
for setting up the kit.

Summary of the Setup Steps for your Vision AI Development Kit
=============================================================

1.  Configure your IoT Hub and IoT Edge Device

2.  Configure Your Development Kit to Connect to The Camera AP

3.  Vision AI Dev Kit Configuration

![](media/image3.png){width="4.091666666666667in" height="2.16875in"}

Picture of The Vision AI Dev Kit and Button Functions

Step 1) Configure Your IoT Hub and IoT Edge Device
==================================================

Now is the time to charge the Vision AI Dev Kit by plugging it into a 2A
charger for 10 minutes. After charging is completed connect the provided
USB cable to your Windows 10 computer with Internet Connectivity to
automatically load drivers. Please have a HDMI cable and monitor ready
to display output after completing all three setup steps.

You will need an Azure IoT Edge connection string to connect your camera
to Microsoft Azure. Follow the steps on this
[page](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal)
to create your IoT Hub and add an IoT Edge device. If you don't already
have a Azure account you can register for a trial account
[here](https://azure.microsoft.com/en-us/offers/ms-azr-0044p/).

A.  When creating your **IoT Edge** device in the [Azure
    portal](https://portal.azure.com) avoid using a device that you have
    used before. Do not reuse the connection string on multiple devices.
    IoT Hub Region may be anywhere The IoT Hub is available except East
    US and West Europe

    ![](media/image4.png){width="5.0079997812773405in"
    height="1.6423611111111112in"}

B.  Copy the Connection string (primary key) to a text file. This is the
    unique identifier for the device. You will need this string later in
    the setup to configure the camera.

Step 2) Configure Your Development Kit to Connect to The Camera AP

When you first power up the device or connect to a charger you will see
three Red LED lights. The LED will start flashing within 10 seconds of
power up. This indicates that the device is ready to go through the WiFi
setup. See the Troubleshooting Section for a complete description of the
different states the LEDs may be in. If you have a display connected to
the device you will see a Gray pattern. You will not see any other text
until after you deploy your IoT Edge runtime to the device.

**WiFi Setup**
==============

A.  Make sure your Vision AI Dev Kit Camera is powered on. (Press the
    power button once.)

B.  From your PC, look for WiFi network with SSID **MSIOT\_xxxxxx**
    (xxxxxx is the last 6 characters of your WiFi mac address, for e.g.
    MSIOT\_BD097D)

C.  Connect to MSIOT\_xxxxxx WiFi access point from your PC.

    a.  Check the label at the bottom of the device whether there is a
        default passphrase. If there is not a label on the bottom of the
        device see the Troubleshooting Section.

D.  Using a browser enter this URL
    [http://setupaicamera.ms](http://setupaicamera.ms/) to connect to
    the device's setup screen  

Step 3) Vision AI Dev Kit Configuration
=======================================

![](media/image5.png){width="2.4025973315835523in"
height="1.383850612423447in"}

![](media/image6.png){width="1.894377734033246in"
height="2.571428258967629in"}

![](media/image7.png){width="1.6038965441819772in"
height="1.1626027996500437in"}

![](media/image8.png){width="1.374915791776028in"
height="0.831169072615923in"}

![](media/image9.png){width="2.1187860892388453in"
height="1.240259186351706in"}

You may now connect a HDMI Cable and Monitor to display output from the
Vision AI Dev Kit.

Firmware Update Instructions and Troubleshooting

When a firmware update for the Vision AI Dev Kit is needed these steps
may be utilized. Microsoft does not recommend frequent updates for minor
release changes unless you are instructed to do so.

Tools required before starting:

-   **ADB (Andriod Debug Bridge) and Fastboot**: Download the
    command-line tools (URL
    [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip),
    [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)
    or
    [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip).)

-   **7-Zip**: Download the 7-Zip file archiver. (URL
    [here](https://www.7-zip.org/))

-   **Use an existing Azure Account or create a free account on this
    URL**: <https://azure.microsoft.com/en-us/free/>

Instructions to Deploy your IoT Edge module are on this URL:

<https://docs.microsoft.com/en-us/azure/iot-edge/quickstart>

-   Altek firmware may be downloaded from this FTP site:
    ftp://ftp.altek.com.tw

**Useful ADB commands to run when the device is connected to Development system (PC) using the supplied USB cable**
===================================================================================================================

1.  Check the battery level

    **adb shell cat /sys/class/power\_supply/battery/capacity**

2.  Check to see if device is connected to PC

    **adb devices**

3.  Check firmware version

    **adb shell cat /etc/version**

4.  Type adb alone to display all available commands

Rebooting the device

Tips: There are multiple methods to reboot the device.

1.  Pin hole on the right. With a single click it will reboot the
    device.

2.  Power button on the back. With a single click it will reboot the
    device.

3.  Using command adb reboot.

4.  Go to adb shell, and then use command reboot.

5.  If none of above steps work long press the power button on the back
    for more than 12 seconds. This will shut down the device. Then
    reboot the device with another long press power button for more than
    12 seconds.

**Updating The Firmware**
=========================

Downloading and Extracting the latest Device Firmware 
======================================================

1.  Get the latest firmware/image released by Altek

2.  Download and extract the .TGZ file with 7zip. After extraction you
    will see a tar file. Next extract again. You will see more than 120
    files located in a folder, for example in folder such as
    *v0.2600\_Perf.*

Flashing the device with the latest firmware 
=============================================

FASTBOOT is now included in the platform tools

1.  Make sure that your platform tools directory is included in your
    path environment variable. From a CMD window, a simple *set
    path=%path%;F:\\AI-CAM\\platform-tools\_r28.0.1-windows\\platform-tools*
    (replace with the right path) would do.

2.  Extract the firmware file with 7zip (as before, first TGZ, then TAR)
    if you haven't.

3.  Copy
    [FastBootUpgrad.bat](https://microsoftapc.sharepoint.com/teams/Selfhost-VisionAIDevKit/Shared%20Documents/General/Altek%20FW%20Image/FastbootUpgrade.bat)
    into the directory you extracted the firmware to.

4.  From a CMD window run *adb devices* to check if the camera is
    attached/recognized

5.  Run FastBootUpgrad.bat

6.  Follow the instructions given, the camera will update and reboot
    when done.

7.  If you are stuck at the message \<waiting for device\>, please
    reboot it and run FastBootUpgrad.bat again. If you keep hitting the
    same message, please charge the device for 10+minutes to make sure
    that the battery is charged.

8.  In your CMD prompt type:

    *adb shell cat /etc/version*

    *v0.2600\_Perf ( confirm that you see the latest version)*

**Troubleshooting**

#### HDMI

1.  HDMI: use a direct HDMI connection to the display. Using converters,
    e.g. DP port, will usually not work.

2.  Stability: the neural processing engine (or other parts of the
    stack) require a reboot occasionally. *adb reboot* will help to
    reset all sub systems.

3.  Incorrect labels: the labels presented on the HDMI output are
    incorrect. The display process picks the label of the last object
    that was detected and presents it to the UI. This is not an
    inferencing bug. *logcat \| grep SNPE* will show you the inferenced
    objects.

4.  Offline mode: iotedged fails to start after reboot if it cannot find
    WiFi.

Display The WiFi Password

These cameras all have a unique WPA Wifi pasword that should be include
on a sticker. If there is no sticker use ADB tools: Run *adb shell cat
/data/misc/wifi/hostapd\_virtual.conf*

 The output will be similar to the text below. The Password is
highlighted and it will be different for your camera. 

> *ctrl\_interface=/var/run/hostapd*
>
> *interface=softap0*
>
> *\#driver=nl80211*
>
> *\#ieee80211d=1*
>
> *ieee80211n=1*
>
> *hw\_mode=g*
>
> *country\_code=US*
>
> *ssid=MSIoT\_E72FA8*
>
> *macaddr\_acl=0*
>
> *channel=0*
>
> *wpa=2*
>
> *wpa\_passphrase=NhEtVE3D *
>
> *wpa\_key\_mgmt=WPA-PSK*
>
> *\#wpa\_pairwise=CCMP*
>
> *rsn\_pairwise=TKIP CCMP*
>
> *ht\_capab=HT20 SHORT-GI-20*
>
> *wmm\_enabled=1*
>
> *ignore\_broadcast\_ssid=0*

 Display The MAC Address

> Get the MAC address of the camera.\
> Using adb \"*adb shell ifconfig wlan0*\"\
> Look for \"HWaddr\".\
> You will see something like 00:0A:G5:5B:20:9E\
> This is the MAC address of the device.

Recover Devices with Failed Flash
=================================

Flashing devices is very reliable. Here are the recovery steps to get
the device back to a working state should the flash fail.

Re-flash using Fastboot (if it is possible to enter fastboot mode)
Fastboot is part of the platform tools.

>   \$ adb reboot bootloader
>
>   \$ fastboot devices
>
>   \$ fastboot flash abl abl.elf
>
>   \$ fastboot flash boot qcs605-boot.img
>
>   \$ fastboot flash system qcs605-sysfs.ext4
>
>   \$ fastboot flash userdata qcs605-usrfs.ext4
>
>   \$ fastboot flash persist qcs605-persist.ext4
>
>   \$ fastboot flash cache qcs605-cache.ext4
>
>   \$ fastboot flash systemrw qcs605-systemrw.ext4
>
>   \$ fastboot reboot

*Additional Commands*

In The CMD prompt type the following commands to check docker container
status

-   *adb shell*, use

-   *docker ps* or *watch docker ps*

If **edgeAgent** is still being downloaded, you will see it empty. To
check if it's in progress, you can use *watch ifconfig wlan0* and see if
the RX bytes are increasing.

If **edgeAgent** is downloaded, you will see it running here. Once you
see edgeAgent is downloaded, you can type *docker logs -f edgeAgent* to
see its progress. Now the device is ready to deploy a module from IoT
Hub.

You can use *docker logs -f edgeAgent* to see the logs and progress of
the Edge Agent.

After you see "Start module \<your module name\>" message then you can
use docker logs -f \<your module name\>

Get IP address of the device using *adb shell ifconfig wlan0*

Running inferencing on CPU (this will give better accuracy as DSP does
not work very well due to quanitization)

1.  Change your va-snpe-engine-library\_config.json by setting below 2
    fields to 0

    1.  \"NetworkIO\":0

    2.  \"Runtime\":0

  ----------------------- ------------- ------------- ------------- ----------------------------------------------------------------------------------
  **Device state**        **LED1**      **LED2**      **LED3**      **Description**
  Setup                   Blink Red     Blink Red     Blink Red     Device in OOBE state. Ready for WiFi Setup.
  Connected to WiFi       Blink Green   Blink Green   Blink Green   WiFi connected to internet access/not connected to IoT Hub
  SoftAP Mode             Blink Amber   Blink Amber   Blink Amber   WiFi in AP mode. Reconfigure WiFi connection.
  IoT Hub Connected       Green         Green         Green         Connected to IoT Hub, downloading manifest/modules, executing modules
  Disconnected            Amber         Amber         Amber         Device is setup but not connected to WiFi. Modules running in Disconnected mode.
  Reboot                  Red                                       Device is rebooting
  Factory Reset           Red           Red           Red           Device is restoring factory settings
  Charging/Connected                                                 
  Charging/Disconnected                                              
  ----------------------- ------------- ------------- ------------- ----------------------------------------------------------------------------------
