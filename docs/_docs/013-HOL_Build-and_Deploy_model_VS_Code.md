---
title: "Deploy a vision AI model with Visual Studio Code"
permalink: /docs/Deploy_model_VS_Code/
excerpt: "Using Visual Studio Code deployment to deploy models to the Vision AI DevKit hardware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-03
---

## What you will do

* Configure VS Code for model deployment
* Build and deploy a default AIVisionDevKitGetStartedModule or a module based on your own Vision AI model to the Visual AI DevKit hardware

## What you will need

* Visual Studio (VS) Code with required extentions [(Instructions)]({{ '/docs/SetUp_VS_Code/' | relative_url}}){:target="_blank"}
* Contents of the [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/){:target="_blank"} opened in VS Code
* Azure IoT Hub and Azure IoT Edge device configured for your Vision AI DevKit hardware [(Instructions)]({{ '/docs/Setup_Azure_resources/' | relative_url}}){:target="_blank"} 
* Active Wi-Fi access point with Internet connectivity.
* [Azure Container Registry](https://ms.portal.azure.com/?flight=1#create/hub){:target="_blank"}
* ADB command line utility ([Instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})
* (optional) HDMI cable and monitor to view video from the Visual AI DevKit

## How can you identify that this tutorial has worked?

If you want to build default AIVisionDevKitGetStartedModule using VS Code, we propose creating a new IoT Edge device in IoT Hub, copying the connection string and re-running your OOBE using the existing connection string. This way, you will be able to manually deploy AIVisionDevKitGetStartedModule. Using the *Getting Started* guide would launch your device with the default module already running, impacting its manual deployment.

If you have your own model for example from *customvision.ai*, you can run this tutorial with the existing AIVisionDevKitGetStartedModule running on a device.


## Instructions in GitHub

* Please access GitHub for [Instructions](https://github.com/microsoft/vision-ai-developer-kit/blob/master/samples/official/ai-vision-devkit-get-started/readme.md){:target="_blank"}. The instructions are maintained in the GitHub as assets for this tutorial are stored on GitHub and need to be kept in sync with any instructions as the content evolves.


