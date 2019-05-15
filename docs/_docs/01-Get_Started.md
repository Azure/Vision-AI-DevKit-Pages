---
title: "Quick Start"
permalink: /docs/Get_Started/
excerpt: "How to quickly install and set up your development environment to use the Vision AI DevKit."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-29
---
This guide will start you on your vision AI journey with the **Vision AI DevKit**. this guide will take you through setting up your Microsoft Azure account to seeing video output from the camera of recognized objects. We will use the VisionSample model for this process.

  ![Flow chart of the steps taken for the first use of the Vision AI Dev Kit, covered in the 'What you will do' section of this document]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## What you will do

- Create necessary Azure IoT resources (Resource Group, IoT Hub, IoT Edge device).
- Connect the Vision AI DevKit camera to Wi-Fi
- Connect the Vision AI DevKit camera to a created IoT Edge Device.
- Deploy the VisionSample model to the device.
- See video output from the camera to a connected monitor or connected video streaming client.

## What you will need

- Active Azure subscription (Create a [free account](https://aka.ms/azureaccount/){:target="_blank"})
- Vision AI DevKit camera hardware
- Monitor supporting HDMI input with an HDMI cable (do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}

## Azure account and resources

### Connect to an Azure account

The Vision AI DevKit is configured to work with Microsoft Azure IoT resources. To get started, you will need an existing (or new) Azure subscription account. If you do not have an Azure account, a free account can be created by visiting this link: [https://azure.microsoft.com/free](https://aka.ms/azureaccount/){:target="_blank"}

### Setup Azure IoT resources

Your Vision AI DevKit will need to be connected to an Azure IoT Edge device within an Azure IoT Hub, which will allow you to remotely manage the Vision AI DevKit. We will use the Azure Command Line Interfact (CLI) to complete these setup tasks.

#### Install Azure Command Line Interface (CLI) tools

- [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest){:target="_blank"}.

- [Install Azure CLI IoT extension](https://github.com/Azure/azure-iot-cli-extension){:target="_blank"}:

    ```cmd
    az extension add --name azure-cli-iot-ext
    ```

- Login to your Azure subscription with Azure CLI:

    ```cmd
    az login
    ```

- Verify the correct subscription is being used:

    ```cmd
    az account list --output table
    ```

    If the incorrect subscription is being used, use the following command to change to the correct one:

    ```cmd
    az account set --subscription <SubscriptionId>
    ```

#### Create Azure IoT resources

- Create a resource group to manage the Azure resources for this project:

    ```cmd
    az group create --name AiDevKitResources --location westus2
    ```

- Create a free F1 IoT Hub (Note: replace {myIoTHub} with a unique name):

    ```cmd
    az iot hub create --resource-group AiDevKitResources --name {myIoTHub} --sku F1
    ```

  This process can take 3 - 5 minutes.

Note: If your receive an error because there is already a free hub in use on your subscription, change the --sku value to S1. You may see an error that the IoT Hub name is not available. IoT Hub names must be globally unique. Please try another name.

- Register your Vision AI DevKit as an IoT Edge device in the IoT Hub you created.

    ```cmd
    az iot hub device-identity create --hub-name {myIoTHub} --device-id myAiDevKitDevice --edge-enabled
    ```

- Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub. Copy the the `connectionString` value. You will use this value when connecting your Vision AI DevKit.

    ```cmd
    az iot hub device-identity show-connection-string --device-id myAiDevKitDevice --hub-name {myIoTHub}
    ```

## Setup your device

Follow [these instructions]({{ '/docs/Run_OOBE/#connect-the-vision-ai-dev-kit-hardware-to-your-azure-iot-hub' | relative_url }}){:target="_blank"} to set up your device for Wifi and register it as an IoT Edge device connected to your IoT Hub.

## Deploy the sample vision AI model

We will use the 'AI Vision Dev Kit Get Started Module' from the IoT Edge Marketplace for this example deployment of a vision AI model.

- Go to [this link](https://ms.portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=AIDevKitPreview#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/AI%20vision%20dev%20kit/resetMenuId/){:target="_blank"}, which will require you to sign-in to the Azure portal. You should see 'AI Vision Dev Kit Get Started Module'. Click on the name, then click the `Create` button.

- Choose your subscription and the IoT Hub you created previously (these fields may already be filled with the correct information)
- Click 'Find device', the click on the name of the device you created, `myAiDevKitDevice` in the 'Select IoT Edge Device' panel that appears.
- Click `Select`, then click `Create`.

In your IoT Hub, click on `IoT Edge`, under *Automatic Device Managment*. Click on the Device ID for your device, the click on the `Set Modules` menu item. Click on `Configure advanced Edge Runtime settings`.

Under 'Advanced Edge Settings - Edge Hub', add the environment variable `OptimizeForPerformance`, set to `False`.

Click the `Save` button.

- Confirm the deployment by clicking on `Next` twice then `Submit`.

After a few minutes (once the module has downloaded to your DevKit), you should see objects being detected by the camera when viewing the output from your DevKit on an HDMI connected monitor! (Note: the 417 Runtime Response should be replaced with 'OK' once the module has downloaded.)

You can optionally use a video player app supporting the RTSP protocol, such as VLC Player, to view the video output from your camera. See the topic [**View RTSP video stream**]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"} for details
