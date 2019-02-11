---
title: "Deploy a Model"
permalink: /docs/02-Deploy_Model/
excerpt: "How to deploy a pre-built vision model to the Vision AI DevKit through the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-11
---
This page will help you deploy a pre-build vision model to your device through the Azure portal.


## What you will do
* Deploy a pre-built sample module through the Azure portal

## What you will need
* An [IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal) configured in your Azure Subscription
* Vision AI Dev Kit camera hardware configured as an [IoT Edge device](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal), with the IoT Edge runtime installed
* HDMI cable
* Monitor with an HDMI input connector

## Select your Vision AI DevKit camera in the Azure portal
1. Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your IoT hub.
2. Select IoT Edge from the menu.
3. Click on the ID of the target camera hardware from the list of devices.
4. Select Set Modules.

![Azure portal 'Set Modules']({{ '/assets/images/Set_Modules.png' | relative_url }})

Note:  If the Set Modules option is not available, ensure that you are selecting the IoT Edge item from the list below Automatic Device Management.  The Set Module Option is not available via the IoT devices link under the Explorers heading

##Configure a deployment manifest
A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins. For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition).

The Azure portal has a wizard that walks you through creating the deployment manifest, instead of building the JSON document manually. It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.

##Add modules
1. In the **Deployment modules** section of the page, select **Add**.
2. Select the **IoT Edge Module**. ![Azure portal 'Add Modules']({{ '/assets/images/Add_Modules.png' | relative_url }})

3. 

