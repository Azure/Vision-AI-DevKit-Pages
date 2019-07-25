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
* Build and deploy a default AIVisionDevKitGetStartedModule or a module based on your own Vision AI model to the Visual AI DevKit hardware

## What you will need

* Visual Studio (VS) Code with required extentions [(Instructions)]({{ '/docs/SetUp_VS_Code/' | relative_url}}){:target="_blank"}
* Contents of the [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/){:target="_blank"} opened in VS Code
* Azure IoT Hub and Azure IoT Edge device configured for your Vision AI DevKit hardware [(Instructions)]({{ '/docs/Setup_Azure_resources/' | relative_url}}){:target="_blank"}. 
* Active Wi-Fi access point with Internet connectivity.
* [Azure Container Registry](https://ms.portal.azure.com/?flight=1#create/hub){:target="_blank"}
* ADB command line utility. ([instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})
* (optional) HDMI cable and monitor to view video from the Visual AI DevKit.

## How to identify that this tutorial has worked?

If you want to build default AIVisionDevKitGetStartedModule using VS Code we propose that you'll create a new IoT Edge device in IoT Hub, copy the connection string and re-run your OOBE using existing connection string. This way your are able to see the AIVisionDevKitGetStartedModule to get deployed. If you went through *Getting Started* guide your device is already running the default module and there is impact in the device when it gets deployed.

If you have your own model for example from customvision.ai you can run this tutorial with existing AIVisionDevKitGetStartedModule running on a device.


## Instructions in GitHub

* Please access GitHub for [Instructions](https://github.com/microsoft/vision-ai-developer-kit/blob/master/samples/official/ai-vision-devkit-get-started/readme.md){:target="_blank"}. The instructions are maintained in the GitHub as they use the GitHub assest and need to be kept in sync in case the content evolves.


