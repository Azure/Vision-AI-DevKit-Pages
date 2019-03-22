---
title: Push DLC model quickly to the device"
permalink: /docs/PushMeBat/
excerpt: "Guide to quickly push DLC model directly to device without contanerizing it first"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
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

    6.	Copy and paste the following into the Container Create Options field: 

    {
    "HostConfig": {
    "Binds": [
    "/data/misc/camera:/app/vam_model_folder"
    ],
    "NetworkMode": "host"
    },
    "NetworkingConfig": {
    "EndpointsConfig": {
    "host": {}
    }
    },
    "Cmd": [
    "-p False"
    ]
    }
 
    7.	Then click Save

    8.	Click Next

    9.	Specify Routes (optional) - click Next

    10.	Review Deployment and click Submit
    
3.	Download the model folder and pushme.bat file here: https://microsoftapc.sharepoint.com/teams/Selfhost-VisionAIDevKit/Shared%20Documents/General/Tools/pushmodeltoCamera.zip
4.	Make sure you have your "model" folder created and containing the following three file types (following are basic example names):

    1.	Label.txt file
    2.	Model.dlc file
    3.	Config.json file

5.	Make sure you also have the pushme.bat file in the same parent folder as the model folder noted above.

6.	Open a Command Prompt as "Run as Administrator"

7.	Access the model folder with the command cd <pushmodeltoCamera folder path>

8.	Use command pushme.bat to apply the model and reboot the device.

9.	After a few minutes, check the docker containers are running with adb shell and docker ps commands.

10.	If no docker containers are running, restart IoT Edge with the command systemctl restart iotedge

11.	Then check again if the docker containers are running with adb shell and docker ps

12.	If the docker containers are still not running, try using the command adb reboot

