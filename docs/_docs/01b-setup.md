---
title: "Module update and deployment"
permalink: /docs/setup/
excerpt: "Vision AI Dev Kit and Azure components"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-05-28
---

## Initial setup

After running through Get Started instructions and initial setup the camera has 4 modules (containers) running:
  - edgeAgent and edgeHub are two modules that make up the [IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime){:target="_blank"}
  - AIVisionDevKitGetStartedModule that is the default Vision AI model and recognizes 183 different objects
  - WebStreamModule that streams the picture from AIVisionDevKitGetStartedModule to a web browser

Visit [Azure portal](https://ms.portal.azure.com/#home){:target="_blank"} to see and manage your IoT Hub

![Initial setup]({{ '/assets/images/Initial_setup.PNG' | relative_url }})

## Module twin update

Deploying a new module using module twin update sets the AIVisionDevKitGetStartedModule to use the Vision AI model from external location. That location can be any location that is publicly accessible. Module twin is a representation of module's metadata in IoT Hub and changes to the metadata made in IoT Hub are applied to the module in IoT Edge device in seconds.

Note that this method requires AIVisionDevKitGetStartedModule to run in the device. This method only updates the Vision AI model, but the module itself. Updating AI model using module twin update is recommend when doing fast iteration with a Vision AI model using for example [customvision.ai](https://customvision.ai){:target="_blank"} for model training.

![Module twin update]({{ '/assets/images/module_twin_update.PNG' | relative_url }})

## Module deployment

Updating module configuration in the camera happens with deployment.json file that defines the set of modules and their characteristics per deployment. Modules are deployed from Azure Container Registry (ACR). The picture below is a simplified version of the deployment. Typically edgeAgent and edgeHub are deployed from Microsoft Container Registry (mcr) where are additional modules are often located in user's person ACR.

IoT Hub provides graphical UI for defining the deployment.json. Tutorials using VS Code and Jupyter Notebook also use this method to deploy the modules and utilize a template for deployment.json

More information about [module deployment](https://docs.microsoft.com/en-us/azure/iot-edge/module-composition){:target="_blank"}.

![Module deployment]({{ '/assets/images/module_deployment.PNG' | relative_url }})
