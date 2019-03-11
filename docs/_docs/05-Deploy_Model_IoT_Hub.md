---
title: "Deploy a Model from IoT Hub"
permalink: /docs/Deploy_Model_IoT_Hub/
excerpt: "How to deploy a pre-built vision model to the Vision AI DevKit through the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-07
---

This page will help you deploy a pre-build vision model to your device through the Azure portal.


## What you will do
* Deploy a pre-built sample module through the Azure portal

## What you will need
* An [IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal){:target="_blank"} configured in your Azure Subscription
* Vision AI Dev Kit camera hardware configured as an [IoT Edge device](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device-portal){:target="_blank"}, with the IoT Edge runtime installed
* HDMI cable
* Monitor with an HDMI input connector

## Select your Vision AI DevKit camera in the Azure portal
1. Sign in to the [Azure portal](https://portal.azure.com/){:target="_blank"} and navigate to your IoT hub.
2. Select **IoT Edge** from the menu.
3. Click on the ID of the target camera hardware from the list of devices.
4. Select **Set Modules**.

![Azure portal 'Set Modules']({{ '/assets/images/Set_Modules.png' | relative_url }})

Note:  If the **Set Modules** option is not available, ensure that you are selecting the IoT Edge item from the list below **Automatic Device Management**.  The **Set Modules** option is not available via the **IoT devices** link under the **Explorers** heading

## Configure a deployment manifest
A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins. For more information about how deployment manifests work and how to create them, see [Understand how IoT Edge modules can be used, configured, and reused](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition){:target="_blank"}.

The Azure portal has a wizard that walks you through creating the deployment manifest, instead of building the JSON document manually. It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.

## Add modules
1. In the **Deployment modules** section of the page, select **Add**.
2. Select the **IoT Edge Module**. ![Azure portal 'Add Modules']({{ '/assets/images/Add_Modules.png' | relative_url }})
3. Provide a name for the module, then specify the container image. To deploy the pre-configured sample, use the following:

	* **Name** - VisionSample
	* **Image URI** - mcr.microsoft.com/aivision/visionsamplemodule:1.0.4_SSD_linklocal-arm32v7
	* **Container Create Options** - `{ <br>
  "HostConfig": { <br>
    "Binds": [ <br>
      "/data/misc/camera:/app/vam_model_folder" <br>
    ], <br>
    "NetworkMode": "host" <br>
  }, <br>
  "NetworkingConfig": { <br>
    "EndpointsConfig": { <br>
      "host": {} <br>
    } <br>
  } <br>
} <br> 
` 
	* **Restart Policy** - Always
	* **Desired Status** - running

    For more information about container create options, restart policy, and desired status see [EdgeAgent desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-edgeagent-edgehub#edgeagent-desired-properties). For more information about the module twin see [Define or update desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition#define-or-update-desired-properties).

4. Select **Save**
5. Select **Configure advanced Edge Runtime settings** 
6. Add the following line to the existing **Create Options** section
  ```
  "User": "root",
  ```
 ![Create Options addition]({{ '/assets/images/Create_Options_Addition.png' | relative_url }})
7. Select **Save**, then select **Next**

## Specify routes
By default the wizard gives you a route called route and defined as FROM /* INTO $upstream, which means that any messages output by any modules are sent to your IoT hub.

Add or update the routes with information from Declare routes, then select **Next** to continue to the review section. For the sample module, no changes are required.

## Review deployment
The review section shows you the JSON deployment manifest that was created based on your selections in the previous two sections. Note that there are two modules declared that you didn't add: **$edgeAgent** and **$edgeHub**. These two modules make up the [IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime){:target="_blank"} and are required defaults in every deployment.

Review your deployment information, then select **Submit**.

 ![Verify that all modules are reported by the device]({{ '/assets/images/VisionSample_IoTHub.png' | relative_url }})

## Verify output on the monitor
Connect the HDMI cable to the camera hardware and your monitor. A few minutes after submitting your deployment, you should start to see video on the monitor with bounding boxes drawing around objects the camera can see and evaluate.
