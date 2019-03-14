---
title: "Model Create/Train: CustomVision.AI"
permalink: /docs/Create_Train_Vision_ML_Project/
excerpt: "Guide to manually creating and training a Vision ML Project for the Vision AI DevKit using Azure services"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-13
---
## What you will do
* Create a vision classifier model using the Azure Custom Vision (Preview) portal.

## What you will need
* A valid Azure subscription. [Create an account for free.}(https://azure.microsoft.com/free/)
* A set of images for use in training your classifier.
* Specific login credentials to download Vision AI DevKit compatible models. 

## Setup your vision classifier
1. Using a browser, login to the Azure Custom Vision Service (Preview) at [https://www.customvision.ai.](https://www.customvision.ai)
    - (Note: You will need to use a specific username/password at this time. This is a temporary measure for downloading a model in the format needed by the Vision AI Dev Kit. An upcoming release of customvision.ai will provide this support to all users. Please review the Teams Wiki for access details.)

2. Follow these instructions for [How to build a classifier with Custom Vision](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier), with the following modifications for the Vision AI Dev Kit hardware.

    - When creating a new project, use these recommended settings:
         - **Project Type** - [Classification]
         - **Classification Type** -  [Multiclass (Single tag per image)]
         - **Domain** - [General(compact)] 

## Export the trained vision model for the Vision AI DevKit

1. Download the trained models using the **Export** button in the  **Performance** tab of the customvision.ai portal.
![Image of the Export button in customvision.ai portal]({{ '/assets/images/Export_Vision_Model.png' | relative_url }})

2. Export with platform selected

3. Congratulations! The first vision model is trained and downloaded
(You can move the model files to the Jupyter Notebook directory and follow the Notebook instructions to continue).
