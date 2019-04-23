---
title: "Hands on Lab - Using the Vision AI DevKit with the VisionSample model"
permalink: /docs/Tutorial-HOL_Using_the_VisionSample/
excerpt: "How to quickly setup the Vision AI DevKit and see objects recognized."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-22
---

## What you will do

- Setup Azure IoT resources to manage the Vision AI DevKit.
- Setup the Vision AI DevKit to connect to Wi-Fi and register as an IoT Edge Device connected to an IoT Hub.
- Deploy the VisionSample model to the device.
- Build a test Vision AI model to detect a simulated analog temperature guage state (Green/Yellow/Red).

## What you will need

- Active Azure subscription (Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F.)
- Vision AI DevKit hardware
- Monitor supporting HDMI input and an HDMI cable (Do not use any cable adapters.)
- Azure Command-Line Interface (CLI) installation

## Setup the Vision AI DevKit

### Setup Azure IoT resources

To setup your Vision AI DevKit as an Azure IoT Edge device, you will create an IoT Hub register and remotely manage your DevKit as an Edge device. All required resources are free. Here are the steps to set this up quickly:

- [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)

- Login to your Azure subscription with Azure CLI:

    ```cmd
    az login
    ```

- Verify the correct subscription is being used (if not use `azure account set --subscription`):

    ```cmd
    az account list --output table
    ```

- [Install Azure CLI IoT extension](https://github.com/Azure/azure-iot-cli-extension):

    ```cmd
    az extension add --name azure-cli-iot-ext
    ```

- Create a resource group to manage all your Azure resources for this project:

    ```cmd
    az group create --name AiDevKitResources --location westus2
    ```

- Create a free IoT Hub:

    ```cmd
    az iot hub create --resource-group AiDevKitResources --name myIoTHub --sku F1
    ```

- Register your Vision AI DevKit in IoT Hub.

    ```cmd
    az iot hub device-identity create --hub-name myIoTHub --device-id myAiDevKitDevice --edge-enabled
    ```

Copy the connection string given back after this last command. You will use this string in the next step.

### Connect your Vision AI DevKit

Follow [these instructions]({{ '/docs/Run_OOBE/#connect-the-vision-ai-dev-kit-hardware-to-your-azure-iot-hub' | relative_url }}) to set up your device to Wifi and register it as an IoT Edge device connected to your IoT Hub.

### Deploy the sample vision AI model

To deploy an sample AI model, we will use the 'AI Vision Dev Kit Get Started Module' from the IoT Edge marketplace.

> [!NOTE] This module is currently hidden in the marketplace thus is only visible with the link below.

- Go to [this link](https://ms.portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=AIDevKitPreview#blade/Microsoft_Azure_Marketplace/GalleryResultsListBlade/selectedSubMenuItemId/%7B%22menuItemId%22%3A%22gallery%2FInternetOfThings_MP%2FIoTEdgeModules%22%2C%22resourceGroupId%22%3A%22%22%2C%22resourceGroupLocation%22%3A%22%22%2C%22dontDiscardJourney%22%3Afalse%2C%22launchingContext%22%3A%7B%22galleryItemId%22%3A%22IoTEdgeModules%22%2C%22source%22%3A%5B%22GalleryFeaturedMenuItemPart%22%5D%2C%22menuItemId%22%3A%22InternetOfThings_MP%22%2C%22subMenuItemId%22%3A%22IoTEdgeModules%22%7D%7D), which will require you to sign-in to the Azure portal. In the list of IoT Edge Modules, scroll down to find the 'AI Vision Dev Kit Get Started Module' (you may need to click the 'Load more' button at the bottom). Click the icon, then  click on `Create`.

> [!Note] A direct link will be given to customers once the module is published publicly.

- Choose your subscription, your IoT Hub named `myIoTHub`, find your device named `myAiDevKitDevice` and click on `Next`.

> [!Note] Module URI needs to be updated today to use a test version.

To edit the module URI, click on `Configure` and update the URI to be `ebertrams/visionsamplemodule:1.0.13_SSD-arm32v7`.

> [!Note] This step won't be required by customers once released.

- Confirm the deployment by clicking on `Next` twice then `Submit`.

After a few minutes (once the module has downloaded to your DevKit), you should see objects being detected by the camera when viewing the output from your DevKit on an HDMI connected monitor!

## Build a custom AI model

You will build a custom AI model to detect when an analog temperature gauge is getting into the warning or danger zone. We will use this website [Simulated Analog Guage](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html) to simulate our analog temperature gauge and will use [Custom Vision](https://www.customvision.ai/) to build a custom model.

### Setup up a new Custom Vision project

- Login to the Azure Custom Vision Service at [https://www.customvision.ai](https://www.customvision.ai).

- Create a new project, use these recommended settings:

  - Project Type - [Classification]
  - Classification Type - [Multiclass (Single tag per image)]
  - Domain - [General(compact)]
  - ** Basic Platforms + Vision AI DevKit

- To use Custom Vision Service, you will need to create Custom Vision training and prediction Azure resources.

    ```cmd
    az cognitiveservices account create -n myCustomVision -g AiDevKitResources --kind CustomVision --sku F0 -l westus2 --yes
    ```

### Upload and tag your training data

Some training images have already been collected for you based on the simulated analog temperature gauge.

- Download the training images from [TrainingData.zip](https://github.com/ebertrams/ai-dev-kit-hands-on-lab-2019/blob/master/TrainingData/TrainingData.zip).
- Uncompress the downloaded .zip file.
- Upload the images to custom vision per color (Green/Yellow/Red), tagging each image with the appropriate color (Green/Yellow/Red) during upload.

### Train and export your custom model

To train it with your new training data, go to your Custom Vision project and click on `Train`.

To export it, select tab `Performances` and `Export` button. Choose the `Vision AI DevKit` option to download your new custom model and finally uncompress them.

## Deploy your custom model to your device

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the Get Started module to use this model instead of the default one. We will use a cloud blob store to store the model but a public OneDrive link woudl work just as well.

### Uploading new custom model files

- Create a storage account:

    ```cmd
    az storage account create --name aidevkitstorage --resource-group AiDevKitResources --location westus --sku Standard_LRS --kind StorageV2
    ```

- Login to the [Azure portal](http://portal.azure.com) and go to your new storage resource.
- From the `overview` tab, click on `Blobs` service.
- `Add a new container` and select `Upload`.
- `Upload` the three files you got from the custom vision service.
- Copy the three URLs of these files.

### Updating the configuration of the Get Started module to use your new custom model

- Login to the [Azure portal](http://portal.azure.com) and go to your ioT Hub resource.
- Click on `IoT Edge` tab and then on your camera device named `myAiDevKitDevice`.
- Click on the `SamplemoduleMobilenetforAIVisionDevkit` module name and click on `Module Identity Twin`.
- Update the three desired properties (model, label, vam config) to map to your new URLs and hit `Save`.

After a few minutes, your device should now be running your custom model!

### Test your new model

- Go to [Simulated Analog Gauge](https://htmlpreview.github.io/?https://github.com/ebertrams/simulated-gauge/blob/master/SimulatedAnalogGauge.html) to view the simulated an analog gauge
- Verify that the camera sees the simulated guage and correctly classify the gauge's output as green / yellow / red from your DevKit's connected monitor.

## Clean up

To delete all the Azure resources that you've been using in this tutorial:

```cmd
az group delete --name AiDevKitResources
```

## Learn more

To learn more, visit [VisionAIDevKit.com](https://visionaidevkit.com).
