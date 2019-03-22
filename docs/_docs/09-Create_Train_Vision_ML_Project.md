---
title: "Model Create/Train: CustomVision.AI"
permalink: /docs/Create_Train_Vision_ML_Project/
excerpt: "Guide to manually creating and training a Vision ML Project for the Vision AI DevKit using Azure services"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---
## What you will do
* Create a vision classifier model using the Azure Custom Vision (Preview) portal, create a container and deploy it to the device

## What you will need for training the model
* A valid Azure subscription. [Create an account for free.](https://azure.microsoft.com/free/)
* A set of images for use in training your classifier.

## What you will for containerizing and deployment
* For deployment using VS Code you'll need a verified VS Code environment. The instructions are available [Deploy model: VS Code](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Deploy_Model_VS_Code/) page.

## Setup your vision classifier
1. Using a browser, login to the Azure Custom Vision Service (Preview) at [https://www.customvision.ai.](https://www.customvision.ai)
    - (Note: Please review the Teams Wiki for pre-GA access details.)

2. Follow these instructions for [How to build a classifier with Custom Vision](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier), using the following information for the Vision AI Dev Kit hardware.

    - When creating a new project, use these recommended settings:
         - **Project Type** - [Classification]
         - **Classification Type** -  [Multiclass (Single tag per image)]
         - **Domain** - [General(compact)] 

## Export the trained vision model for the Vision AI DevKit

1. Download the trained models using the **Export** button in the  **Performance** tab of the customvision.ai portal.
![Image of the Export button in customvision.ai portal]({{ '/assets/images/Export_Vision_Model.png' | relative_url }})

2. Select Vision AI Dev Kit platform

3. Export will provide you with model.dlc and labels.txt files that are needed in the next phase.

4. Congratulations! The first vision model is trained and downloaded

## Containerize and deploy you model

1. For containerizing and deploying you model using VS Code please follow the instructions in [vision-ai-developer-kit GitHub](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample/BasicEdgeSolution) /sample-solutions/VisionSample/BasicEdgeSolution.

2. You can also move the model files to the Jupyter Notebook directory and follow the Notebook instructions to continue.
