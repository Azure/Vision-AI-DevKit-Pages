---
title: "Bug bash lab"
permalink: /docs/bblab/
excerpt: "Bush bash lab instructions for running the OOBE and creating a customvision.ai model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-29
---

# AI dev kit Bug bash 2019

## What are you going to do

This bug bash lab consist of two phases
1. Setting up your device and needed Azure services
2. Training a model using customvision.ai and deploying it to the camera

### Hardware setup
Make sure that your AI vision dev kit is plugged to power via USB

### Get an Azure subscription
- Use your own Azure subscription for the lab. Microsoft employee specific instructions can be found from the lab invidation

### Connect your PC to the camera's Wi-Fi access point

- You device is in a state where is has a fresh firmware update to it. It should flash red lights indicating that it is running and access point you can connect you PC to.
- From your PC, connect to a Wi-Fi network named MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device's Wi-Fi mac address, e.g. MSIOT_BD097D). If there is a password listed in the device that is needed during OOBE
- OOBE guides you through the process of creating Azure resources and connecting your device to them. The device connects to Azure IoT Hub that controls the network traffic between the device and cloud. During OOBE you'll create IoT Hub and a IoT Edge device in a hub that represent the camera.
- OOBE also deployes a default VisionSample model to teh device that can recognize multiple objects.

## Build your own AI model
We'll build our own AI model to detect when someone is wearing an hard hat. You have an hard hat on your desk which well be used to validate your model built with <a href="https://www.customvision.ai/" target="blank">Custom Vision</a>.

### Setup up a new Custom Vision project
- Login to the Azure Custom Vision Service (Preview) at <a href="https://www.customvision.ai/" target="blank">https://www.customvision.ai/</a>.

- Create a new project, use these recommended settings:
    - Give it a name like `Simulated HardHat Detector`
    - Project Type - [Classification]
    - Use the existing resource group
    - Classification Type - [Multiclass (Single tag per image)]
    - Domain - [General(compact)]
    - Export Capabilites - Vision AI Dev Kit

### Upload and tag your training data
Some training images have already been collected for you for the hard hat use case.

Download them and upload them to your Custom Vision project:
- Downlaod the .zip file at this location: <a href="https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL" target="blank">https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL</a>
- Uncompress it
- Upload images to custom vision per tag (HardHat/NoHardHat) and tag them appropriately them during upload. Upload all pictures names similarly (like HardHat) at the same time.

### Train and export your custom model
To train it with your new training data, go to your Custom Vision project and click on `Train`.

To export it, select tab `Performances` and `Export` button. Choose the `Vision AI Dev Kit` option to download your new custom model and finally uncompress them.

### Deploy your custom model to your device
To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the Get Started module to use this model instead of the default one. We will use a cloud blob store to store the model but a public OneDrive link would work just as well.

#### Uploading new custom model files
We'll start by creating a new storage account and then upload your model to it.
- Login to the <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a>
- Search for `Storage` and select the `Storage accounts` service
- Use your existing subscription and resource group
- Give it a unique name, upper case characters are not allowed
- Select the West-US 2 region
- Click on `Review+Create` (other default options shoudl be correct)
- Wait until until provisioning is complete and navigate to yoru new storage account
- From the `overview` tab, click on `Blobs` service
- `Add a new container`, give it a name like `hardhatmodel` and make sure to select `Container (anonymous read access for containers and blobs)` for the `Public access level`
- Click on the container just created, Click on the `Upload` button and select your files from the custom vision service and `Upload`
- Copy the three URLs of these files by clicking on each of them and copying their URL to the clipboard

#### Updating the configuration of the Get Started module to use your new custom model

- Login to the <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a> and go to your ioT Hub resource
- Click on `IoT Edge` tab and then on your camera device named `visionkit`
- Click on the `AIVisionDevKitGetStartedModule` module name and click on `Module Identity Twin`
- Update the three desired properties (model, label, vam config) to map to your new URLs and hit `Save`

After a few minutes, your device should now be running your custom model!

### Test your new model
- Put your hard hat on and smile at the camera !
- Verify that the camera picks it up and correctly classify you as wearing the hard hat

## Going further
As a next step, you could re-use the same training images but build an object detection model instead of an image classifier. For that, please use this <a href="https://iris-demo1.azurewebsites.net/projects" target="blank">environment of custom vision</a> and use its labeling tool.

To learn more about this AI Dev Kit, visit <a href="https://azure.github.io/Vision-AI-DevKit-Pages/docs/Get_Started/" target="blank">https://azure.github.io/Vision-AI-DevKit-Pages/docs/Get_Started/</a> 


## Clean up
Before leaving, please:


Thank you!
