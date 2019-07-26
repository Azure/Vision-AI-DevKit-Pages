---
title: "Airlfit 2019 - Train an AI model for the Vision AI DevKit"
permalink: /docs/airlift/
excerpt: "Setup the camera; Create a customvision.ai model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-06-10
---

## Welcome to Airlift - train an AI model for use with the Vision AI DevKit

### What you will do

- Setup a Vision AI DevKit camera
- Train a model using Customvision.ai and deploy the model to the camera
- Create an Azure IoT Hub with an IoT Edge device for controlling network traffic between the camera and the cloud

### What you will need

- Active Azure subscription

## Setup the Vision AI DevKit camera

1. The Vision AI DevKit camera you were provided should be displaying three blinking red LEDs on the front of the camera, indicating the camera is running in Wi-Fi APN mode.
2. Connect your laptop to the camera's Wi-Fi APN. The APN for your device can be found on a sticker on the bottom of the camera. The name will be in the format 'MSIOT_xxxxxx' (xxxxxx is the last 6 characters of the device’s Wi-Fi mac address, e.g. MSIOT_BD097D). **Note:** since there are multiple of these devices running in the lab, ensure you select the correct one.
3. An existing IoT Hub can be used. Please create in any case a new IoT Edge device.
4. Once connected to the camera, use your browser to open [setupaicamera.ms](https://setupaicamera.ms){:target="_blank"}. Follow the instructions on the screen and complete the whole OOBE flow. Connecting device to internet is not enough, it has to be associated with IoT Hub as well.
5. Go carefully through the OOBE experience and set up the camera
6. During the setup process, connect the camera to **MSFTGUEST** Wifi. (No password is required).

**Note:** After camera setup is complete, you can stream the live camera video output using a browser window or and application such as VLC / Open VC player. Your laptop will need to be connected to the same Wi-Fi network (MSFTGUEST) as the camera to display the video stream.

## Train an AI model using CustomVision.ai

You will build a custom AI model to detect when someone is wearing a hard hat, using the [Azure Custom Vision service](https://customvision.ai){:target="_blank"}.

### Setup up a new Custom Vision project

- Login to Azure Custom Vision service at [https://customvision.ai](https://customvision.ai){:target="_blank"}.

### Image classification vs. object detection

There are two ways to train your model - image classification and object detection.

*Image classification:* analyses the whole frame as a picture and doesn't draw bounding boxes. Can only identify one object per frame. Easy to train
*Object detection:* Can identify multiple objects per image and draws bounding boxes around them. Takes a little bit more time to train as the training requires identifying the object per uploaded image.

#### Create new project

- Create a new project, using these recommended settings:
  - Give it a name like `Simulated HardHat Detector`
  - Project Type - select between [Classification] and [ObjectDetection]
  - Use the existing resource group
  - Classification Type - [Multiclass (Single tag per image)]
  - Domain - [General(compact)] **NOTE: Ensure you do not select the `General` option**
  - Export Capabilites - Vision AI Dev Kit

### Upload and tag your training data
Some training images have already been collected for you for the hard hat use case.

- Download the .zip file containing the sample images from: <a href="https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL" target="blank">https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL</a>
- Uncompress the zip file to a local directory
- Upload images to custom vision in batches, 
  - For image classification model one batch per tag (images containing *HardHat* in the name, then *NoHardHat*), adding the appropriate tag during upload.
  - For object detection model each picture needs to be tagged separately. They can all be uploaded to customvision.ai at the same time.

### Train your custom model

To train your model using the uploaded training images, go to your Custom Vision project and click on `Train`.

To export your model, select the `Performances` tab, then click the `Export` button. Choose the `Vision AI Dev Kit` option to download your model. Instead of download press the right button of your mouse in order to see options. Select `Copy link`. It is a link that points to a zip file of your model. 

This is the fastest way to deploy the model to your camera in lab environment. Please note that this link will expire and instructions for using for example Azure blob storage to store the model can be found from the left side menu under *Tutorials* -> *Create and deploy a vision AI model*

 ![Clone GitHub]({{ '/assets/images/cvai_link.PNG' | relative_url }})

### Update the configuration of the VisionSample module to use your custom model

- Login to <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a> and go to the IoT Hub resource you created earlier.
- Click the `IoT Edge` tab, then click on IoT edge  device named `visionkit`.
- Click on the `AIVisionDevKitGetStartedModule`  name, then click `Module Identity Twin`.
- Update the zip file with the URL you saved earlier to *"ModelZipUrl": ""*, then click `Save`.

After a few seconds, your device should now be running your custom model! If it doesn't try editing the module twin again and save (press for example space and backspace and save)

### Test your new model

- Put on a hard hat on and smile at the camera!
- Verify the camera correctly classifies you as wearing a hard hat.

