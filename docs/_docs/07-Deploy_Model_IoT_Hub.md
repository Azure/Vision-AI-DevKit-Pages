---
title: "Deploy a Vision AI model with Azure IoT Hub"
permalink: /docs/Deploy_Model_IoT_Hub/
excerpt: "How to deploy a pre-built vision model to the Vision AI DevKit through the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

## What you will do

* Deploy a pre-built sample model container image to the Vision AI DevKit hardware using Azure IoT Hub

## What you will need

* Configured Azure Iot Hub with the Vision AI DevKit registered as an IoT Edge device ([Instructions](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Setup_Azure_resources/){:target="_blank"})
* Vision Dev Kit sample model - [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample).
* (optional) Monitor and HDMI cable

## Select your Vision AI DevKit hardware in the Azure portal
1. Download or Clone the latest Vision AI DevKit repository from [GitHub](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample).
2. Sign in to the [Azure portal](https://portal.azure.com/){:target="_blank"} and navigate to your IoT hub.
3. Select **IoT Edge** from the menu.
4. Click on the ID of the target camera hardware from the list of devices.
5. Select **Set Modules**.

![Azure portal 'Set Modules']({{ '/assets/images/Set_Modules.png' | relative_url }})

  - If the **Set Modules** option is not available, ensure that you are selecting the IoT Edge item from the list below **Automatic Device Management**.  The **Set Modules** option is not available via the **IoT devices** link under the **Explorers** heading

## Configure a deployment manifest
A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins. For more information on deployment manifests, see [Understand how IoT Edge modules can be used, configured, and reused](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition){:target="_blank"}.

The Azure portal uses a wizard to walk you through creating the deployment manifest. It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.

### Add modules
1. In the **Deployment modules** section of the page, select **Add**.
2. Select the **IoT Edge Module**. ![Azure portal 'Add Modules']({{ '/assets/images/Add_Modules.png' | relative_url }})
3. Provide a name for the module, then specify the container image. To deploy the pre-configured sample, use the following values:

```
  Name - VisionSample
  Image URI - mcr.microsoft.com/aivision/visionsamplemodule:1.0.4_SSD_linklocal-arm32v7
  Container Create Options - 
      {
        "HostConfig": {
          "Binds": [
            "/data/misc/camera:/app/vam_model_folder"
          ],
          "NetworkMode": "host"
        },
        "NetworkingConfig": {
          "EndpointsConfig": {
            "host": {}
          }
        }
      }
  Restart Policy - Always
  Desired Status - running
```

For more information about *Container Create Options*, *Restart Policy*, and *Desired Status* see [EdgeAgent desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-edgeagent-edgehub#edgeagent-desired-properties). For more information about *Module Twin* see [Define or update desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition#define-or-update-desired-properties).

4. Select **Save**
5. Select **Configure advanced Edge Runtime settings** 
6. Add the following line to the existing **Create Options** section
  ```
  "User": "root",
  ```
 ![Create Options addition]({{ '/assets/images/Create_Options_Addition.png' | relative_url }})
7. Select **Save**, then select **Next**

### Specify routes

By default the wizard gives you a route called *route*, defined as FROM /* INTO $upstream, which means that any messages output by any module will be sent to your IoT hub.

While the sample module requires no changes, you can add or update the routes with information from Declare routes, then select **Next** to continue to the review section.

### Review deployment

The review section shows you the JSON deployment manifest created based on your selections in the previous two sections.

* Note: There are two modules declared that you didn't add, **$edgeAgent** and **$edgeHub**. These modules represent the [IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime){:target="_blank"} and are required for every deployment.

 ![Verify that all modules are reported by the device]({{ '/assets/images/VisionSample_IoTHub1.png' | relative_url }})

Review your deployment information, then select **Submit**.

## Verify output on the monitor
Connect the HDMI cable to the Vision AI DevKit hardware and your monitor. A few minutes after submitting your deployment, you should start to see video on the monitor with bounding boxes drawing around objects the camera can see and evaluate.
