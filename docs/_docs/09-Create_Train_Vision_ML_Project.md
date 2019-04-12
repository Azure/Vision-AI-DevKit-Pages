---
title: "Create and deploy a vision AI model with CustomVision.AI"
permalink: /docs/Create_Train_Vision_ML_Project/
excerpt: "Guide to creating, training and deploying a Vision ML Project for the Vision AI DevKit using Azure Custome Vision Service (customvision.ai)."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-26
---
## What you will do
* Create a vision classifier model using the [Azure Custom Vision Service](https://customvision.ai) portal, create a container and deploy it to the device

## What you will need for training the model
* A valid Azure subscription. [Create an account for free.](https://azure.microsoft.com/free/)
* A set of images for use in training your classifier.

## What you will need for containerizing and deployment
* For deployment using VS Code you'll need a verified VS Code environment. The instructions are available [Deploy model: VS Code](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Deploy_Model_VS_Code/) page. If you are only going to use VS Code for containerizing the model, you don't need Anaconda/Python. However, they will be needed for many other activities like building a business logic module that takes actions based on what camera sees.
* You will also needed [Docker](https://www.docker.com/get-started) for containerizing the image using your local resources and Docker extension for VS Code. Docker installation and login are also instructed later in the instructions. Don't sign in Docker Desktop after Docker is installed.

## Setup your vision classifier
1. Using a browser, login to the Azure Custom Vision Service (Preview) at [https://www.customvision.ai.](https://www.customvision.ai)

2. Follow these instructions for [How to build a classifier with Custom Vision](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier), using the following information for the Vision AI Dev Kit hardware.

    - When creating a new project, use these recommended settings:
         - **Project Type** - [Classification]
         - **Classification Type** -  [Multiclass (Single tag per image)]
         - **Domain** - [General(compact)]
         - ** Basic images + Vision AI Dev Kit

3. Note that to use Custom Vision Service, you will need to create [Custom Vision Training and Prediction resources](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=microsoft_azure_cognitiveservices_customvision#create/Microsoft.CognitiveServicesCustomVision) (it is also instructed in 2. step below) in the in the Azure portal. This will create both a Training and Prediction resource.

## Export the trained vision model for the Vision AI DevKit

1. Download the trained models using the **Export** button in the  **Performance** tab of the customvision.ai portal.
![Image of the Export button in customvision.ai portal]({{ '/assets/images/Export_Vision_Model.png' | relative_url }})

2. Select Vision AI Dev Kit platform
![Custom Vision AI export]({{ '/assets/images/customvisionai_export.JPG' | relative_url }})

3. Export will provide you with model.dlc and labels.txt files that are needed in the next phase.

4. Congratulations! The first vision model is trained and downloaded

## Containerize and deploy you model

1. For containerizing and deploying your model using VS Code please follow the instructions in [vision-ai-developer-kit GitHub](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample/CreateAndDeployEdgeContainer) /sample-solutions/VisionSample/CreateAndDeployEdgeContainer.

These instructions will guide you through the process of containerizing the image using the resources in your local computer.

2. You can also move the model files to the Jupyter Notebook directory and follow the Notebook instructions to continue.
