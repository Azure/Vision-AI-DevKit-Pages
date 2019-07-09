---
title: "Use pictures taken by the Vision AI Dev Kit to train your model"
permalink: /docs/train/
excerpt: "Use pictures taken by the Vision AI Dev Kit to train your model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-06-12
---

## What you will do

- Use Vision AI Dev Kit to take pictures you will later use to train your Vision AI model

## What you will need

- Cloned or downloaded version of [https://github.com/Microsoft/vision-ai-developer-kit](https://github.com/Microsoft/vision-ai-developer-kit){:target="_blank"}
- Python installation (instructions instructing the usage with Anaconda prompt installed as a part of [VS Code setup instructions]({{ '/docs/SetUp_VS_Code/' | relative_url}}){:target="_blank"})
- Camera and your device running in same WiFi network?
- IP address of your device. You can find it by using platform tools and typing in a command "adb shell ifconfig wlan0"

## Take pictures with the camera

- Open command prompt that allows you to run python scripts. When using Windows command prompt add python to the path using a following command

     set path=%path%;[path to your python folder]

- Go to the directory in your device where you have the contents of vision-ai-developer-kit GitHub. 
- Go to folder vision-ai-developer-kit/samples/research/ai-vision-devkit-get-started-legacy/modules/VisionSampleModule/python_iotcc_sdk/sdk/

Run command:

     
     python .\capture_and_train.py --ip {IP address of your device} -t {object of interest} -p False -n {number of pictures}
     

For example:

     
     python .\capture_and_train.py --ip 10.10.10.10 -t Apple -p False -n 10
     

where:
- **IP Address** is the IP address of your device
- **Object of interest** is the object you are taking pictures from like "Apple". The script will create a folder with the same name to the directory where the script is located and store the picture to the folder
- **Number of pictures** defines how many pictures the camera takes. The time between pictures is roughly 1 seconds

Note: it may be that taking pictures with the camera causes the VisionAIDevKitGetStartedModule not to function properly afterwards and the device needs to be rebooted in order to get the module to inference normally.





