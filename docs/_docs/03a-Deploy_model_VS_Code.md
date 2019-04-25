---
title: "Deploy a vision AI model with Visual Studio Code"
permalink: /docs/Deploy_model_VS_Code/
excerpt: "Using Visual Studio Code deployment to deploy models to the Vision AI DevKit hardware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-11
---

## What you will do

* Configure VS Code for model deployment
* Deploy a pre-built sample model container image to the Visual AI DevKit hardware

## What you will need

* Visual Studio (VS) Code with required extentions [(Instructions)]({{ '/docs/SetUp_VS_Code/' | relative_url}}){:target="_blank"}
* Vision Dev Kit sample model - [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample){:target="_blank"}.
* Azure IoT Hub and Azure IoT Edge device configured for your Vision AI DevKit hardware [(Instructions)]({{ '/docs/Setup_Azure_resources/' | relative_url}}){:target="_blank"}
* Active Wi-Fi access point with Internet connectivity.
* (optional) HDMI cable and monitor to view video from the Visual AI DevKit.

## Deploy the sample model container image to the Vision AI DevKit

1. Download or Clone the latest Vision AI DevKit repository from [GitHub](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample){:target="_blank"}.
2. Launch Visual Studio Code, and select [File > Open Folder…] command to open the “VisionSample” directory as the workspace root.
3. Right click the *deployment.template.json* file under the *VisionSample\DeployContainerFromAML* folder and select **Generate IoT Edge Deployment Manifest** to create a new *deployment.json* file under *VisionSample\DeployContainerFromAML\config* folder.  
![Open deployment.template.json screen shot]({{ '/assets/images/VSC_Deploy_open_deployment-template-json_screenshot.png' | relative_url }}) 
4. Click the [Explorer] icon, then click […] in the **AZURE IOT HUB DEVICES** section on the right side. Click **Select IoT Hub** to select your Azure IoT Hub.
5. Expand the **AZURE IOT HUB DEVICES** section. Right-click your IoT Edge device, then select **Create Deployment for Single Device**. Click the *deployment.json* file under the *VisionSample\DeployContainerFromAML\config* folder, then click the **Select Edge Deployment Manifest** button to deploy the container image to the IoT Edge device (your Vision AI DevKit hardware).
![Open deployment.template.json from VSC Screenshot]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot.png' | relative_url }})  
 ![Open deployment.template.json from VSC Screenshot #2]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot2.png' | relative_url }})
6.	Configure the device as an IoT Edge device using the connection string for your Vision AI DevKit, obtained earlier.
7.	Monitor the deployment status for the AI Vision Kit device by the command lines
    ```cmd
    adb shell docker ps
    adb shell docker logs edgeAgent
    ```
![Use ADB to monitor deployment status Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_monitor_deployment_screenshot.png' | relative_url }})
8.	Check object detection results using the command line

    ```cmd
    adb shell iotedge logs <module name>
    (e.g. “adb shell iotedge logs VisionSampleImagenet”)
    ```
Mobilenet-imagenet model can detect the 1000 object classes listed in the  *VisionSample\MachineLearning\models\mobilenet-imagenet\orig\output_labels.txt*.

    ![Use ADB to module impage outputs Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_check_detection_results_screenshot.png' | relative_url }})

In VS Code, select **AZURE IOT HUB DEVICES > … > Select IoT Hub** and then **AZURE IOT HUB DEVICES > … > Start Monitoring D2C Message** command to monitor the messages sent from the AI Vision DevKit to your Azure IoT Hub.
    ![Screenshot of message monitoring output]({{ '/assets/images/VSC-Deploy-Monitor-messages.png' | relative_url }})

### Verify output on the monitor
Connect the HDMI cable to the Vision AI DevKit hardware and your monitor. A few minutes after submitting your deployment, you should start to see video on the monitor with bounding boxes drawing around objects the camera can see and evaluate.

Note: You can also view the camera output using an RTSP compatible video player. See [View RTSP video stream]({{ '/docs/RTSP_stream/' | relative_url}}){:target="_blank"} for more information.
