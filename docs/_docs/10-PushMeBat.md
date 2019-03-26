---
title: Push DLC model quickly to the device
permalink: /docs/PushMeBat/
excerpt: "Guide to quickly push DLC model directly to device without contanerizing it first"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-25
---
## What you will do
* Push DLC model directly to device without contanerizing it first

## What you need
* .dlc file and labels.txt file
* VAM configuration file
* You need to also have a module running in a device that uses .dlc file

1.	Make sure your device is connected to your PC via USB.

2.	To make sure you can manually push the model, adjust the parameters in IoTHub:
    1.	Click IoT Edge
    2.	Click your device.
    
    3.	Then select Set Modules

    4.	Select the Vision Sample module

    5.	Update the Image URL field with the following string: mcr.microsoft.com/aivision/visionsamplemodule:1.0.7_SSD-arm32v7

    ![IoT Edge device configuration, set modules]({{ '/assets/images/PushMe_EdgeModuleConf.JPG' | relative_url }})

    6.	Copy and paste the following into the Container Create Options field: 
    ```
        > {
        > "HostConfig": {
        > "Binds": [
        > "/data/misc/camera:/app/vam_model_folder"
        > ],
        > "NetworkMode": "host"
        > },
        > "NetworkingConfig": {
        > "EndpointsConfig": {
        > "host": {}
        > }
        > },
        > "Cmd": [
        > "-p False"
        > ]
        > }
    ```

    7.	Then click Save. “Cmd”: [ “-p False” ] prevents the VisionSample from being pushed from IoT Hub to the device. Without this configuration the model your are going to push to the device using ADB will be automatically overwritten from IoT Hub.

    8.	Click Next

    9.	Specify Routes (optional) - click Next

    10.	Review Deployment and click Submit
    
3.	Download the model folder and pushme.bat file [here](https://microsoftapc.sharepoint.com/teams/Selfhost-VisionAIDevKit/Shared%20Documents/General/Tools/pushmodeltoCamera.zip)
4.	Make sure you have your "model" folder created and containing the following three file types (following are basic example names):

    * Label.txt file
    * Model.dlc file
    * VAM Configuration file (va-snpe-engine-library_config.json)
    
    * Note: in order to test your own model quickly you'll need to replace these three files. The default VAM configuration file supports models created using customvision.ai. 

5.	Make sure you also have the pushme.bat file in the same parent folder as the model folder noted above,

6.	(In Windows) Open a Command Prompt and make sure that you have platform tools (ADB) in the path.

      For Windows, use the command line:
      ```
      set path=%path%;<platform tools path>
      ```

7.	Access the folder with pushme.bat and run it by typing pushme.bat to apply the model to your device. Reboot the device.

8.	After a few minutes, check the docker containers are running with adb shell and docker ps commands.

9.	If no docker containers are running, restart IoT Edge with the command systemctl restart iotedge

10.	Then check again if the docker containers are running with adb shell and docker ps

11.	If the docker containers are still not running, try using the command adb reboot

