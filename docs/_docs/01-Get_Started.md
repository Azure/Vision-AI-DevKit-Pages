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
To get you started on your journey with vision AI, using the **Vision AI DevKit**, this guide will take you through setting up your Azure account to seeing video output from the camera of recognized objects. We will use the VisionSample model for this process.

  ![High level steps to take for the initial Vision AI Dev Kit setup]({{ '/assets/images/GetStarted.PNG' | relative_url }})

## What you will do

- Setup Azure IoT resources to manage the Vision AI DevKit.
- Setup the Vision AI DevKit to connect to Wi-Fi and register as an IoT Edge Device connected to an IoT Hub.
- Deploy the VisionSample model to the device.

## What you will need

- Active Azure subscription (Create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F.){:target="_blank"}
- Vision AI DevKit hardware
- Monitor supporting HDMI input and an HDMI cable (Do not use any cable adapters), or an [RTSP supporting video player application]({{ '/docs/RTSP_stream/' | relative_url }})
- Azure Command-Line Interface (CLI) installation
- Ubuntu for Windows [Windows Store link](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6?activetab=pivot:overviewtab){:target="_blank"}

## Setup Azure IoT resources

To setup your Vision AI DevKit as an Azure IoT Edge device, you will create an IoT Hub to register and remotely manage your DevKit as an Edge device. All required resources are free.

### Install Azure Command Line Interface (CLI) tools

- [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest){:target="_blank"}.

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
    azure account set --subscription <SubscriptionId>
    ```

- [Install Azure CLI IoT extension](https://github.com/Azure/azure-iot-cli-extension){:target="_blank"}:

    ```cmd
    az extension add --name azure-cli-iot-ext
    ```

### Create Azure IoT resources

- Create a resource group to manage all your Azure resources for this project:

    ```cmd
    az group create --name AiDevKitResources --location westus2
    ```

- Create a free F1 IoT Hub (Note: replace {myIoTHub} with a unique name):

    ```cmd
    az iot hub create --resource-group AiDevKitResources --name {myIoTHub} --sku F1
    ```

Note: If your receive an error because there is already a free hub in use on your subscription, change the SKU to S1. You may also see an error that the IoT Hub name is not available. IoT Hub names must be globally unique. Please try another name.

- Register your Vision AI DevKit in IoT Hub.

    ```cmd
    az iot hub device-identity create --hub-name {myIoTHub} --device-id myAiDevKitDevice --edge-enabled
    ```

- Retrieve the connection string for your device, which links your physical device with its identity in IoT Hub. Copy the the `connectionString` value. You will use this value when connecting your Vision AI DevKit.

    ```cmd
    az iot hub device-identity show-connection-string --device-id myAiDevKitDevice --hub-name {myIoTHub}
    ```

## Setup your Vision AI DevKit

Follow [these instructions]({{ '/docs/Run_OOBE/#connect-the-vision-ai-dev-kit-hardware-to-your-azure-iot-hub' | relative_url }}){:target="_blank"} to set up your device for Wifi and register it as an IoT Edge device connected to your IoT Hub.

## Deploy the sample vision AI model

To deploy an sample AI model, we will use the 'AI Vision Dev Kit Get Started Module' from the IoT Edge marketplace.

> [!NOTE] This module is currently hidden in the marketplace thus is only visible with the link below.

- Go to [this link](https://ms.portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=AIDevKitPreview#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/AI%20vision%20dev%20kit/resetMenuId/){:target="_blank"}, which will require you to sign-in to the Azure portal. In the list of IoT Edge Modules, scroll down to find the 'AI Vision Dev Kit Get Started Module (preview)' (you may need to click the 'Load more' button at the bottom). Click the icon, then  click on `Create`.

> [!Note] A direct link will be given to customers once the module is published publicly.

- Choose your subscription, your IoT Hub named `myIoTHub`, find your device named `myAiDevKitDevice` and click on `Next`.

> [!Note] Module URI needs to be updated today to use a test version.

To edit the module URI, click on `Configure` and update the URI to be `ebertrams/visionsamplemodule:1.0.16_SSD-arm32v7`.

The new version of the get started module (v1.0.16 or higher) requires new settings in the createOptions. Please replace its createOptions by the following and hit `Save`:

```terminal
    {
      "HostConfig": {
        "Binds": [
          "/data/misc/camera:/app/vam_model_folder",
           "/run/systemd:/run/systemd"
        ],
        "NetworkMode": "host"
      },
      "NetworkingConfig": {
        "EndpointsConfig": {
          "host": {}
        }
      }
    }
```

> [!Note] This step won't be required by customers once released.

- Confirm the deployment by clicking on `Next` twice then `Submit`.

[!NOTE]
> On the latest firmware, a regression has been introduced. To work around it, you need to click on `Configure advanced Edge runtime settings` and replace the createOptions of the edgeHub with the following:
>
```terminal
 {
   "User": "root",
   "HostConfig": {
     "PortBindings": {}
   }
 }
```

> [!NOTE]
> Some reliability issues have been found with the current version of the edgeHub. To fix them, click on `Configure advanced Edge runtime settings` replace the edgeHub URI from `mcr.microsoft.com/azureiotedge-hub:1.0.7-rc2` with `mcr.microsoft.com/azureiotedge-hub:1.0.7-rc2` and the edgeAgent URI from `mcr.microsoft.com/azureiotedge-agent:1.0.7-rc2` with `mcr.microsoft.com/azureiotedge-agent:1.0.7-rc2`. This will be fixed automatically with 1.0.7 release.

After a few minutes (once the module has downloaded to your DevKit), you should see objects being detected by the camera when viewing the output from your DevKit on an HDMI connected monitor! You can optionally use a video player app supporting the RTSP protocol, such as VLC Player, to view the video output from your camera. See the topic [**View RTSP video stream**]({{ '/docs/RTSP_stream/' | relative_url }}) for details
