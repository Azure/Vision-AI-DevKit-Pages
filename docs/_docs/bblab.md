---
title: "May 2019 Bug bash lab"
permalink: /docs/bblab/
excerpt: "Bush bash lab instructions for running the OOBE and creating a customvision.ai model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-05-24
---

## What you will do

- Set up a Vision AI DevKit camera and needed Azure services
- Train a model using [Azure Custom Vision service](https://customvision.ai){:target="_blank"}, then deploy the model to the Vision AI DevKit

## Pre-requisites

- Vision AI DevKit camera, connected to power via USB
- Active Azure subscription

### Connect your PC to the camera's Wi-Fi access point

- Your Vision AI DevKit camera is in a state where it has been freshly updated with the latest firmware. You should see the three fron LEDs flashing red, indicating the device is running in Wi-Fi APN mode, waiting for your PC to connect.
- From your PC, connect to the Wi-Fi network named MSIOT_xxxxxx. The name for your camera (and any required password) should be found on a sticker attached to the camera. (Note: xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D).
- The initial user experience (OOBE) will guide you through the process of creating Azure resources, configuring your device to use them. You will use Azure IoT Hub to control network traffic between the device and the Azure resources. During OOBE you'll create the IoT Hub with an IoT Edge device which represents your camera.
- OOBE also deploys a default VisionSample model to the camera, which can recognize multiple objects.

## Build a custom AI model

You will build a custom AI model to detect when someone is wearing an hard hat. (You should have a hard hat on your desk to use for model validation.) You will use the [Azure Custom Vision service](https://customvision.ai){:target="_blank"} to build the model.

### Setup up a new Custom Vision project
- Login to Azure Custom Vision Service at [https://customvision.ai](https://customvision.ai){:target="_blank"}.

- Create a new project, us\ing these recommended settings:
    - Give it a name like `Simulated HardHat Detector`
    - Project Type - [Classification]
    - Use the existing resource group
    - Classification Type - [Multiclass (Single tag per image)]
    - Domain - [General(compact)] **NOTE: Ensure you do not select the `General` option**
    - Export Capabilites - Vision AI Dev Kit

### Upload and tag your training data
Some training images have already been collected for you for the hard hat use case.

- Download the .zip file containing the sample images from: <a href="https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL" target="blank">https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL</a>
- Uncompress the zip file to a local directory
- Upload images to custom vision in batches, one batch per tag (images containing *HardHat* in the name, then *NoHardHat*), adding the appropriate tag during upload.

### Train and export your custom model

To train your model using the uploaded training images, go to your Custom Vision project and click on `Train`.

To export your model, select the `Performances` tab, then click the `Export` button. Choose the `Vision AI Dev Kit` option to download your model, then  uncompress the files to a local directory.

### Deploy your custom model to your camera

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the VisionSample module to use this new model. We will use a cloud blob store to store the model, but any publically accessible file storage system will work.

#### Upload your trained model files

We'll start by creating a new storage account and then upload your model to it.

- Login to <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a>.
- Search for `Storage` and select `Storage accounts`.
- Use your existing Azure subscription and resource group.
- Create a new storage account with a unique name (NOTE: upper case characters are not allowed).
- Select the `West-US 2` region.
- Click on `Review+Create` (other default options should be correct).
- Wait until until provisioning is complete and navigate to your new storage account.
- From the `overview` tab, click on `Blobs`.
- Click `Add a new container`, give it a name like `hardhatmodel` and make sure to select `Container (anonymous read access for containers and blobs)` for the `Public access level`.
- Click on the container just created, then click  the `Upload` button and select the files you downloaded from the Azure Custom Vision service.
- Copy the three URLs of the uploaded files for later use.

#### Update the configuration of the VisionSample module to use your custom model

- Login to <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a> and go to the IoT Hub resource you created earlier.
- Click the `IoT Edge` tab, then click on IoT edge  device named `visionkit`.
- Click on the `AIVisionDevKitGetStartedModule`  name, then click `Module Identity Twin`.
- Update the three desired properties (model, label, vam config) with the URLs you saved earlier, then click `Save`.

After a few minutes, your device should now be running your custom model!

### Test your new model

- Put your hard hat on and smile at the camera!
- Verify the camera correctly classifies you as wearing a hard hat.

## Going further
As a next step, you could re-use the same training images but build an object detection model instead of an image classifier. To do this, please go to this <a href="https://iris-demo1.azurewebsites.net/projects" target="blank">demo environment of the Azure Custom Vision service</a> and use the labeling tool.

To learn more about the Vision AI DevKit, visit <a href="https://visionaidevkit.com/" target="blank">https://visionaidevkit.com</a> 

## Clean up
Before leaving, please:

Thank you!
