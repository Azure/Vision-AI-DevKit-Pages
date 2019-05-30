---
title: "Tutorial: Create and deploy a custom vision AI module using Azure Custom Vision service and Azure IoT Edge"
permalink: /docs/Tutorial-HOL_Using_the_VisionSample/
excerpt: "How to create and deploy a custom vision AI module to the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-29
---

## What you will do

- Build a vision AI model for detecting the state (Green/Yellow/Red) of a simulated analog temperature gauge using the Azure Custom Vision service.
- Deploy the vision AI module to the Vision AI DevKit camera using Azure IoT Edge.

## What you will need

- Active Azure subscription (Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F.){:target="_blank"})
- Configured Vision AI DevKit camera [(Instructions)]({{ '/docs/Get_Started/' |relative_url }}){:target="_blank"}
- Monitor supporting HDMI input and an HDMI cable (do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}

## Create a vision AI model with Azure Custom Vision service

In this tutorial, you will build a vision AI model to detect when an analog temperature gauge is getting into the warning or danger zone. We will use this website [Simulated Analog Guage](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html){:target="_blank"} to simulate our analog temperature gauge and will use the [Azure Custom Vision](https://www.customvision.ai/){:target="_blank"} service to build the model.

### Setup a new Azure Custom Vision project

- Login to the Azure Custom Vision Service at [https://www.customvision.ai](https://www.customvision.ai){:target="_blank"}.

- Create a new project, using these recommended settings:

  - Training and prediction resources
    - SKU - F0

  - Name - `Simulated Temperature Gauge`
    - Project Type - [Classification]
    - Resource Group `AiDevKitResources-CustomVision`
    - Classification Type - [Multiclass (Single tag per image)]
    - Domain - [General(compact)]  **NOTE: Ensure you do not select the `General` option**
    - Export Capabilities - Vision AI Dev Kit

### Upload and tag your training data

- Download the training images - [TrainingData.zip]({{ '/Needed/TrainingData.zip' | relative_url }}).
- Uncompress the downloaded .zip file to a directory on your system.
- Upload the images to custom vision in sets, grouped by color (ex. all files with Green in the name, then Yellow in the name, then Red), tagging each image set with the appropriate color (Green, Yellow, or Red) at upload.

### Train and export your custom model

- Go to your Custom Vision project and click on `Train`.
- Select the `Performances` tab and then click the `Export` button.
- Choose the `Vision AI DevKit` option to download your new custom model, then uncompress the files to a folder on your system.

## Deploy your custom model to your device

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the `AI Vision Dev Kit Get Started Module (preview)`, (used in the Quick Start) to use the model you just trained. We will place the model files in a cloud blob store. A public OneDrive link would work as well.

### Upload new model files to Azure Blob Store

- Login to the [Azure portal](http://portal.azure.com){:target="_blank"} and create a new storage resource.
  - Use a unique name (less than 24 characters in length, using all lower case letters)
  - SKU = Standard_LRS
  - Kind = Storage V2

- From the `overview` tab, click on `Blobs` service.
- Click `Add a new container`, using a name such as `model001`, selecting `Container (anonymous read access for containers and blobs)` for the `Public access level`.

- Click on the container you created, then click `Upload`.
- Select the three files downloaded from the Custom Vision service and click `Upload`.
- Copy the three URLs for each of these files for later use.

### Modify the configuration of the `Get Started` module

- Login to the [Azure portal](http://portal.azure.com){:target="_blank"} and go to your ioT Hub resource.
- Click the `IoT Edge` tab and then click on your device named `myAiDevKitDevice`.
- Click on the `AIVisionDevkitGetStartedModule` module name and click on `Module Identity Twin`.
- Update the properties `ModelUrl`, `LabelUrl` and `ConfigURL` to the URLs you just received and click `Save`.

```terminal
{
    "properties.desired":{
        "ModelUrl":"URL",
        "LabelURL":"URL",
        "ConfigUrl":"URL",
        "FreqToSendMsg":12,
        "ObjectOfInterest":"ALL"
    }
}
```

After a few minutes, your device should be running your custom model.

### Test your new model

- Go to [Simulated Analog Gauge](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html){:target="_blank"} using your computer browser.
- Point the DevKit camera at the gauge on your monitor and verify the camera sees the simulated gauge and correctly classifies the gauge's output as green / yellow / red by viewing the output on your DevKit's connected monitor or by using a video player supporting an RTSP source. [(View RTSP Stream)]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}

## Clean up

To delete the Azure resources that you've been using in this tutorial, execute the following commands:

```cmd
az group delete --name AiDevKitResources
az group delete --name AIDevKitResources-CustomVision
```

## Learn more

To learn more, return to [Vision AI DevKit - Get Started](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Get_Started/).
