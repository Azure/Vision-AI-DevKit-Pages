---
title: "Deploy a vision AI container module using Azure IoT Hub"
permalink: /docs/Deploy_Model_IoT_Hub/
excerpt: "How to deploy a pre-built vision module to the Vision AI DevKit camera using the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

## What you will do

* Deploy a pre-built sample container module to the Vision AI DevKit camera using Azure IoT Hub

## What you will need

* Configured Azure Iot Hub with the Vision AI DevKit registered as an IoT Edge device ([Instructions](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Setup_Azure_resources/){:target="_blank"})
* (optional) Monitor and HDMI cable

## Select your Vision AI DevKit hardware in the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com/){:target="_blank"} and navigate to your IoT hub.
2. Select **IoT Edge** from the menu.
3. Click on the ID of the target camera hardware from the list of devices.
4. Select **Set Modules**.

![Azure portal 'Set Modules']({{ '/assets/images/Set_Modules.png' | relative_url }})

  Note: If the **Set Modules** option is not available, ensure that you are selecting the IoT Edge item from the list below **Automatic Device Management**.  The **Set Modules** option is not available via the **IoT devices** link under the **Explorers** heading

## Configure a deployment manifest

A deployment manifest is a JSON document that describes which modules to deploy, how data flows between the modules, and desired properties of the module twins. For more information on deployment manifests, see [Understand how IoT Edge modules can be used, configured, and reused](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition){:target="_blank"}.

The Azure portal uses a wizard to walk you through creating the deployment manifest. It has three steps: **Add modules**, **Specify routes**, and **Review deployment**.

### Add modules

1. In the **Deployment modules** section of the page, select **Add**.
2. Select the **IoT Edge Module**. ![Azure portal 'Add Modules']({{ '/assets/images/Add_Modules.png' | relative_url }})
3. Provide a name for the module, then specify the container image. To deploy the pre-configured sample, use the following values:

```terminal
      Name - VisionSample
      Image URI - mcr.microsoft.com/aivision/visionsamplemodule:latest
      Container create options –
      {
        "HostConfig": {
          "NetworkMode": "host",
          "Binds": [
            "/data/misc/camera:/app/vam_model_folder",
            "/run/systemd:/run/systemd"
            ]
        },
        "NetworkingConfig": {
          "EndpointsConfig": {
            "host": {}
          }
        }
       }
    ```

Optional: Deploy the Webstream module if you want to view the video output in a browser. To deploy the Webstream module, use the following values and replace the IP address with the IP address of your device:

```terminal
     Name – WebStreamModule
     Image URI - mcr.microsoft.com/aivision/visionsamplemodule:webstream_0.0.13-arm32v7
     Environment variables –
        RTSP_IP <IP_address_of_camera>
        RTSP_PORT 8900
        RTSP_PATH live

     Container create options –
     {
      "ExposedPorts": {
      "3000/tcp": {},
      "3002/tcp": {}
     },
      "HostConfig": {
        "NetworkMode": "host",
        "PortBindings": {
        "3000/tcp": [
          {
            "HostPort": "3000"
          }
        ],
        "3002/tcp": [
          {
            "HostPort": "3002"
          }
        ]
      }
      },
        "NetworkingConfig": {
          "EndpointsConfig": {
            "host": {}
          }
        }
```

- For more information about *Container Create Options*, *Restart Policy*, and *Desired Status* see [EdgeAgent desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-edgeagent-edgehub#edgeagent-desired-properties){:target="_blank"}.
- For more information about *Module Twin* see [Define or update desired properties](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition#define-or-update-desired-properties){:target="_blank"}.

4. Select **Save**
5. Select **Configure advanced Edge Runtime settings**
  - Under `Edge Agent`, use `Image -mcr.microsoft.com/azureiotedge-agent:1.0.7.1`
6. Select **Save**, then select **Next**

### Specify routes

By default the wizard gives you a route called *route*, defined as FROM /* INTO $upstream, which means that any messages output by any module will be sent to your IoT hub.

While the sample module requires no changes, you can add or update the routes with information from Declare routes, then select **Next** to continue to the review section.

### Review deployment

The review section shows you the JSON deployment manifest created based on your selections in the previous two sections.

* Note: There are two modules declared that you didn't add, **$edgeAgent** and **$edgeHub**. These modules represent the [IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime){:target="_blank"} and are required for every deployment.

 ![Verify that all modules are reported by the device]({{ '/assets/images/VisionSample_IoTHub1.png' | relative_url }})

Review your deployment information, then select **Submit**.

## Verify DevKit camera output

After a few minutes (once the module has downloaded to your DevKit camera), you should see objects detected by the camera showing on a monitor connected to the HDMI port on the DevKit camera. (Note: if you see a 417 Runtime Response, it should be replaced with ‘OK’ once the module has downloaded.)

You can optionally use a video player app supporting the RTSP protocol, such as VLC Player, to view the video output from your camera. See [View RTSP video stream]({{ '/docs/RTSP_stream/' | relative_url}}){:target="_blank"} for more information.
