---
title: "Tutorial: Create and deploy a custom vision AI module"
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

- Build a test vision AI model for detecting the state (Green/Yellow/Red) of a simulated analog temperature guage.

## What you will need

- Active Azure subscription (Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F.){:target="_blank"})
- Configured Vision AI DevKit hardware [(Instructions)]({{ '/docs/Get_Started/' |relative_url }}){:target="_blank"}
- Monitor supporting HDMI input and an HDMI cable (do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}
- Azure Command-Line Interface (CLI) installation [(Instructions)]({{ '/docs/Get_Started/#install-azure-command-line-interface-cli-tools' | relative_url }}){:target="_blank"}

## Create a custom AI model with Azure Custom Vision service

You will build a custom AI model to detect when an analog temperature gauge is getting into the warning or danger zone. We will use this website [Simulated Analog Guage](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html){:target="_blank"} to simulate our analog temperature gauge and will use [Custom Vision](https://www.customvision.ai/){:target="_blank"} to build a custom model.

### Setup up a new Custom Vision project

- Create Custom Vision training and prediction Azure resources.

    ```cmd
    az cognitiveservices account create -n myCustomVision -g AiDevKitResources --kind CustomVision --sku F0 -l westus2 --yes
    ```

- Login to the Azure Custom Vision Service at [https://www.customvision.ai](https://www.customvision.ai){:target="_blank"}.

- Create a new project, using these recommended settings:

  - Give it a name like `Simulated Temperature Gauge`
    - Project Type - [Classification]
    - Resource Group `AiDevKitResources-CustomVision`
    - Classification Type - [Multiclass (Single tag per image)]
    - Domain - [General(compact)]
    - ** Basic Platforms + Vision AI Dev Kit

### Upload and tag your training data

Some training images have already been collected for you based on the simulated analog temperature gauge.

- Download the training images from [TrainingData.zip]({{ '/Needed/TrainingData.zip' | relative_url }}).
- Uncompress the downloaded .zip file.
- Upload the images to custom vision in sets, per color (Green/Yellow/Red), tagging each image set with the appropriate color (Green/Yellow/Red) during upload.

### Train and export your custom model

To train your model with your new training data, go to your Custom Vision project and click on `Train`.

To export the model, select tab `Performances` and `Export` button. Choose the `Vision AI DevKit` option to download your new custom model and finally uncompress them.

## Deploy your custom model to your device

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the Get Started module to use this model instead of the default one. We will use a cloud blob store to store the model but a public OneDrive link would work just as well.

### Uploading new custom model files

- Create a storage account:

    ```cmd
    az storage account create --name {storageaccountname} --resource-group AiDevKitResources --location westus --sku Standard_LRS --kind StorageV2
    ```

    Note: Replace {storageaccountname} in the command-line with a unique name. The name can be no more than 24 characters long and must be in lower-case letters.

- Login to the [Azure portal](http://portal.azure.com){:target="_blank"} and go to your new storage resource.
- From the `overview` tab, click on `Blobs` service.
- `Add a new container`, with a name such as `model001`, selecting `Container (anonymous read access for containers and blobs)` for the `Public access level`.

- Click on the container you created, select `Upload`.
- Select the three files files downloaded from the Custom Vision service and click 'Upload'.
- Copy the three URLs for each of these files.

### Updating the configuration of the Get Started module to use your new custom model

- Login to the [Azure portal](http://portal.azure.com){:target="_blank"} and go to your ioT Hub resource.
- Click on `IoT Edge` tab and then on your camera device named `myAiDevKitDevice`.
- Click on the `SamplemoduleMobilenetforAIVisionDevkit` module name and click on `Module Identity Twin`.
- Update the three desired properties (model, label, vam config) to map to your new URLs and hit `Save`.

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

After a few minutes, your device should now be running your custom model.

### Test your new model

- Go to [Simulated Analog Gauge](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html){:target="_blank"} to view the simulated an analog gauge
- Verify that the camera sees the simulated gauge and correctly classifies the gauge's output as green / yellow / red from your DevKit's connected monitor or using a video player supporting RTSP [(View RTSP Stream)]({{ '/docs/RTSP_stream/' | relative_url }}).

## Clean up

To delete all the Azure resources that you've been using in this tutorial:

```cmd
az group delete --name AiDevKitResources
az group delete --name AIDevKitResources-CustomVision
```

## Learn more

To learn more, return to [Vision AI DevKit - Get Started](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Get_Started/).
