![](media/image1.jpeg){width="6.5in"
height="2.8125in"}![](media/image2.png){width="2.0104166666666665in"
height="3.0625in"}

  Date               Revisions
  ------------------ ----------------------------
  Oct 12^th^, 2018   First draft
  Oct 18^th^, 2018   Updated to release v0.1140
  Oct 30^th^, 2018   Updated to release v0.1530
  Nov 27^th^, 2018   Updated to release v0.2270
  Nov 30^th^, 2018   Updated to release v0.2340
  Dec 7^th^, 2018    Updated to release v0.2390

This is a step-by-step process to update the SW and configure the Vision
AI Dev Kit (codename Peabody). This document will cover instructions
from connecting hardware, setting up IoT Edge to configuring a basic
object detection AI model for viewing the results through HDMI display
and RTSP streaming.

Tools required before starting:
===============================

-   **ADB**: Download the ADB command-line tool for
    [Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip),
    [MAC](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)
    or
    [Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip).

-   **QFIL (part of QPST)**: QFIL is the application for Windows to
    install or flash stock firmware on devices using Qualcomm Chipset.
    Download from [Qualcomm
    CreatPoint](https://createpoint.qti.qualcomm.com/tools/#suite/285/27224)
    (available to existing licensees). (MSFT internal users use [this
    link](https://microsoftapc.sharepoint.com/teams/Selfhost-VisionAIDevKit/Shared%20Documents/General/Tools/qpst.win.2.7_installer_00480.14.zip).)

-   **7-Zip**: Download the 7-Zip file archiver. (from
    [here](https://www.7-zip.org/))

Validate PC is connecting to the device
=======================================

Connect the USB-type C cable from your windows PC to the camera.

Use command *adb devices* from your CMD prompt to see if the is
detected.

![](media/image3.png){width="2.220833333333333in"
height="0.6039446631671042in"}

*Tip: Long press the button behind Peabody device will trigger
hardware-reboot that may rescue you from being stuck.* *The* *long
pressing the white button at the back to reboot may not work
consistently because of ongoing SW changes. If your device has a hole on
the left side, press it and it will trigger power off. Then click on the
white button at the back again will make it power on again.*

Downloading and Extracting the latest Device Firmware 
======================================================

(jump to [Setup the IoT Hub and your IoTEdge
Device](#setup-the-iot-hub-and-your-iotedge-device) if device has the
latest firmware)

1.  Get the latest firmware/image released by Altek from this \* FTP
    site:

    (MSFT internal users use this
    [link](https://microsoftapc.sharepoint.com/:f:/t/Selfhost-VisionAIDevKit/EvyJ_qgT3oREqnjXTzhcjf4BfWjUDhMpZplsrcjvXjws2Q?e=KiXs5E).)

    In your browser or File Explorer: <ftp://ftp.altek.com.tw> (works
    well on Chrome; do not use Edge)

    username: Altek\_Microsoft

    Password: 4H\^J5i%&\^i

    As of Dec 7^th^, 2018, the latest firmware version is 0.2390. The
    PEABODY\_QCS603\_LE\_r29-v0.2390\_Perf.tgz file size for 0.2390
    should be 970,045,490 bytes -- confirm this.

    (Use **7-Zip** for the following three steps.)

2.  If you see it extracts another tar file, extract the tar file again
    and you will a folder containing 121 files

Flashing the device with the latest firmware 
=============================================

3.  Start QFIL that you download earlier. (MSFT internal users use [this
    link](https://microsoft.sharepoint.com/:u:/t/AzureMLbasedAICamera-Qualcomm/EWurO-L2ZIhKrXkc9RfOQJYBuP_G79fXGCAl1j9uMZfJtw?e=mGzUgN).)

4.  Enable **Reset After Download** per the screenshots below in
    *Configuration -\>Firehose programmer Setting*.

    ![](media/image4.png){width="3.7392279090113734in"
    height="2.8555555555555556in"}

5.  Open a cmd prompt in your PC.

6.  Type *adb reboot edl* to switch the device to flashing mode.

7.  Select QDLoader 9008 from Select Port in QFIL

    ![](media/image5.png){width="4.063144138232721in"
    height="2.3701662292213475in"}

8.  Make sure the detected device shows that following name, which
    implies that the device is ready for updating with new firmware.

    ![Machine generated alternative text:
    ](media/image6.png){width="5.90833552055993in"
    height="0.6654746281714785in"}

9.  Select the update files per the screenshots below.

-   Select *Browse* -\> *prog\_firehose\_ddr.elf*

    ![](media/image7.png){width="3.975236220472441in"
    height="1.4210629921259843in"}

-   Select *Load XML .... -\> rawprogram\_unsparse.xml*

    ![](media/image8.png){width="3.7100153105861766in"
    height="1.6163932633420823in"}

-   *patch0.xml*

    ![](media/image9.png){width="4.324011373578303in"
    height="1.271334208223972in"}

10. Then Click Download to start flashing. It will take within 2 minutes
    generally.

    ![Warning](media/image10.png){width="0.2in" height="0.2in"} Do not
    interrupt this step. Risk of permanently damaging the device.

11. Make sure the Status shows Download Succeed per screenshot
    below.![](media/image12.png){width="6.5in"
    height="1.3618055555555555in"}

12. In your CMD prompt type:

    *adb shell cat /etc/version*

    *v0.2390\_Perf ( confirm you see the latest version)*

Setup the IoT Hub and your IoTEdge Device
=========================================

Follow the steps on this
[page](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal)
to create your IoT Hub and add a IoT Edge device.

> **NOTE**: Offline mode
>
> You can setup your device to work in offline mode. Follow the steps on
> [[this]{.underline}](https://docs.microsoft.com/en-us/azure/iot-edge/offline-capabilities)
> page.

a)  IoT Hub Region must be any where IoT Hub is available, except East
    US and West Europe

b)  ~~Set environment variable **UpstreamProtocol** = **MQTT** for
    edgeHub and edgeAgent~~

<!-- -->

13. When creating your **IoTEdge** device in the [Azure
    portal](https://portal.azure.com), avoid using a device you have
    used before. Do not reuse the connection string on multiple devices.

    ![](media/image13.png){width="5.0079997812773405in"
    height="1.6423611111111112in"}

14. Copy the Connection string (primary key)

    This is the unique identifier for the device. You will need this
    string to configure your device.

Setup the default Object classification module
==============================================

### Deploy a prebuilt sample module through Azure portal

15. In the IoT edge device that you created earlier, click on Set
    modules, as shown in screenshot below.

    ![](media/image14.png){width="6.5in" height="1.9625in"}

16. In Deployment modules section, click on Add =\> IoT Edge Module.

    ![](media/image15.png){width="4.943201006124235in" height="3.775in"}

17. Put a name and the following details:

-   Image URI

mcr.microsoft.com/aivision/visionsamplemodule:**1.0.3\_demo\_objdetect-arm32v7**

-   codes snippet in Container Create Options. This is basically
    pointing the DLC files to a path that they are really located at.

    *{*

    *\"HostConfig\": {*

    *\"Binds\": \[*

    *\"/data/misc/camera:/app/vam\_model\_folder\"*

    *\],*

    *\"NetworkMode\": \"host\"*

    *},*

    *\"NetworkingConfig\": {*

    *\"EndpointsConfig\": {*

    *\"host\": {}*

    *}*

    *}*

    *}*

> ![](media/image16.png){width="4.635416666666667in"
> height="7.890071084864392in"}

18. Press Save.

19. Now it comes back to the *1 Add Modules (optional)* tab in *Set
    module* page.

20. Please click on *Configure advanced Edge Runtime settings* button at
    the bottom and add this line *\"User\": \"root\",* in Create
    Options.

    ![](media/image17.png){width="4.941767279090114in"
    height="1.6916666666666667in"}

    ![](media/image18.png){width="4.120535870516186in" height="3.55in"}

21. Press Save at the bottom.

22. Press Next under *Configure advanced Edge Runtime settings* button.

23. In *2 Specify Routes (optional),* remains unchanged and press Next.

24. In 3 Review Deployment, press Submit at the lower right corner.

25. Now you will see there are 3 modules here.

    ![](media/image19.png){width="5.90833552055993in"
    height="3.0166590113735783in"}

Configure your AI Camera Device
===============================

26. Make sure your AI Camera is powered on. (Press the power button
    once.)

![](media/image20.png){width="4.092160979877515in"
height="2.1688298337707788in"}

27. From your PC, look for WiFi network with SSID **MSIOT\_xxxxxx**
    (xxxxxx is the last 6 characters of your WiFi mac address, for e.g.
    MSIOT\_BD097D)

28. Connect to MSIOT\_xxxxxx WiFi access point from your PC.

29. The default passphrase is described as below

    \- check the label at the bottom of the device, there is default
    passphrase. If this doesn't exist,

    \- try 12345678 as default passphrase, if failed, check this:
    [Access Point WPA password on newer cameras - when 12345678 does not
    work\... in
    Wiki](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::c23825f0-6e7e-4ad6-af2e-64ecd324d775?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A2%2C%5C%22sectionId%5C%22%3A4%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A39ea7c4d806e461d8654bbd720b8332f%40thread.skype%22%7D&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47)

 

30. On connected to Wi-Fi, a default webpage will pop up to guide you
    through the OOBE steps. If it doesn't pop up automatically, please
    visit this url http://setupaicamera.ms.

31. Follow the instructions to fill in necessary information. The steps
    should be well-described.

    ![](media/image21.tmp){width="4.166666666666667in"
    height="3.0337423447069116in"}

32. For the last step connecting to Microsoft Azuer, depending on your
    WiFi connection speed, it will take a few minutes to pull edgeAgent
    from your Azure IoTEdge.

### THE END!

> Connect a display to the HDMI port (direct connection only, no
> converters please) to see the object classification model running on
> the camera.
>
> Some known issues listed [here](#known-issues).

\[debugging steps / tips & tricks\]
===================================

In CMD prompt type the following commands to check docker container
status

-   *adb shell*, use

-   *docker ps* or *watch docker ps*

If **edgeAgent** is still being downloaded, you will see it empty. To
check if it's in progress, you can use *watch ifconfig wlan0* and see if
the RX bytes is growing.

If **edgeAgent** is downloaded, you will see it running here. Once you
see edgeAgent is downloaded, you can type *docker logs -f edgeAgent* to
see its progress. Now the device is ready to deploy a module from IoT
Hub.

You can use *docker logs -f edgeAgent* to see the logs and progress of
the Edge Agent.

After you see "Start module \<your module name\>" message then you can
use docker logs -f \<your module name\>

Get IP address of the device using *adb shell ifconfig wlan0*

TROUBLESHOOTING::

a.  Running inferencing on CPU (this will give better accuracy as DSP
    doe snto work very well due to quanitization)

    1.  Change your va-snpe-engine-library\_config.json by setting below
        2 fields to 0

        1.  \"NetworkIO\":0

        2.  \"Runtime\":0

b.  How to run on camera that never connects to internet

    a.  Download this image on your pc from here

#### KNOWN ISSUES

1.  HDMI: use a direct HDMI connection to the display. Using converters,
    e.g. DP port, will usually not work.

2.  Stability: the neural processing engine (or other parts of the
    stack) will crash from time to time. *adb reboot* will help to reset
    all sub systems.

3.  Incorrect labels: the labels presented on the HDMI output are
    incorrect. The display process picks the label of the last object
    that was detected and presents it to the UI. This is not an
    inferencing bug. *logcat \| grep SNPE* will show you the inferenced
    objects.

4.  Offline mode: iotedged fails to start after reboot if it cannot find
    WiFi.
