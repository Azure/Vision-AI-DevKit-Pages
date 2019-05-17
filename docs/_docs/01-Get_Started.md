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
This guide will start you on your vision AI journey with the **Vision AI DevKit**, taking you from setting up your Microsoft Azure account to seeing video output from the DevKit camera of recognized objects. We will use a VisionSample model for this process, which has been trained to recognize up to 183 different objects.

  ![Flow chart of the steps taken for the first use of the Vision AI Dev Kit, covered in the 'What you will do' section of this document]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## What you will do

- Create necessary Azure IoT resources (Resource Group, IoT Hub, IoT Edge device)
- Connect the Vision AI DevKit camera to Wi-Fi
- Connect the Vision AI DevKit camera to a created IoT Edge Device
- Deploy the containerized VisionSample model to the device
- See video output from the camera to a connected monitor or connected video streaming client

## What you will need

- Active Azure subscription
- Vision AI DevKit camera hardware
- Monitor supporting HDMI input with an HDMI cable (do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }}){:target="_blank"}

## Azure account and resources

### Connect to an Azure account

The Vision AI DevKit is configured to work with Microsoft Azure IoT resources. To get started, you will need a new or existing Azure subscription. You can create a free account by visiting this link: [https://azure.microsoft.com/free](https://aka.ms/azureaccount/){:target="_blank"}

### Setup Azure IoT resources

Your Vision AI DevKit camera will need to be configured as an Azure IoT Edge device within an Azure IoT Hub. This allows you to remotely manage the camera. We will use the Azure Command Line Interfact (CLI) to complete these setup tasks.

Note: Each of the command lines below should be executed in a command prompt dialog opened on your computer.

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

    If the wrong subscription was selected, use this command to change to the correct one:

    ```cmd
    az account set --subscription <SubscriptionId>
    ```

#### Create Azure IoT resources

- Create a resource group to manage the Azure resources for this project:

    ```cmd
    az group create --name AiDevKitResources --location westus2
    ```

- Create a free IoT Hub (Note: replace {myIoTHub} with a unique name):

    ```cmd
    az iot hub create --resource-group AiDevKitResources --name {myIoTHub} --sku F1
    ```

  This process can take 3 - 5 minutes.

  Notes:

    - If your receive an error because there is already a free hub in use on your subscription, change the --sku value to S1.
    - You may see an error that the IoT Hub name is not available. IoT Hub names must be globally unique. Please try another name.

- Register your Vision AI DevKit as an IoT Edge device in the IoT Hub you just created.

    ```cmd
    az iot hub device-identity create --hub-name {myIoTHub} --device-id myAiDevKitDevice --edge-enabled
    ```

- Retrieve the connection string for the IoT Edge device you created. This string will be used to link your physical DevKit camera with the Edge device identity in your IoT Hub.

    ```cmd
    az iot hub device-identity show-connection-string --device-id myAiDevKitDevice --hub-name {myIoTHub}
    ```

- Copy the the `connectionString` value returned. You will use this value when configuring your DevKit camera.

## Setup your DevKit camera

These steps will configure your DevKit camera for Wi-Fi and connect the the camera to the IoT Edge device you created earlier in Azure IoT Hub.

{% include_relative OOBE.md %}

## Deploy the sample vision AI model

We will use the 'AI Vision Dev Kit Get Started Module' from the IoT Edge Marketplace for this example deployment of a containerized vision AI model.

- Go to [this link](https://ms.portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=AIDevKitPreview#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/AI%20vision%20dev%20kit/resetMenuId/){:target="_blank"}, which will require you to sign-in to the Azure portal. You should see `AI Vision Dev Kit Get Started Module (preview)`. Click on the name, then click the `Create` button.
- Choose your subscription and the IoT Hub you created previously (these fields may already be filled with the correct information).
- Click `Find device`, then click on the name of the device you previously created, `myAiDevKitDevice` in the `Select IoT Edge Device` panel that appears.
- Click `Select`, then click `Create`.

In your IoT Hub, click on `IoT Edge`, under `Automatic Device Managment`. Click on the `Device ID` for your device, then click on the `Set Modules` menu item. Click on `Configure advanced Edge Runtime settings`.

Under `Advanced Edge Settings - Edge Hub`, add the environment variable `OptimizeForPerformance`, set to `False`.

Click the `Save` button.

- Confirm the deployment by clicking on `Next` twice then `Submit`.

## View DevKit camera output

After a few minutes (once the module has downloaded to your DevKit camera), you should see objects  detected by the camera showing on a monitor connected to the HDMI port on the DevKit camera. (Note: if you see a 417 Runtime Response, it should be replaced with 'OK' once the module has downloaded.)

You can optionally use a video player app supporting the RTSP protocol, such as VLC Player, to view the video output from your camera. See the topic [**View RTSP video stream**]({{ '/docs/RTSP_stream/#connect-to-the-video-stream' | relative_url }}){:target="_blank"} for details

## Next steps

In this quickstart, you configured the Vision AI DevKit camera to display output for objects recognized by the VisionSample model to a monitor or RTSP capable video player.

From here, your next step is to create and deployE a custom vision ML model using the Azure Custom Vision service.

[Create and deploy a vision ML model using the Azure Custom Vision service]({{ '/docs/Tutorial-HOL_Using_the_VisionSample/' | relative_url }}){:target="_blank"}
