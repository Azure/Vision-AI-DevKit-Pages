---
title: "MLADS 2019 - train your AI model for Vision AI Dev Kit"
permalink: /docs/mlads/
excerpt: "Bush bash lab instructions for running the OOBE and creating a customvision.ai model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-06-06
---

## Welcome to MLADS - train you model for Vision AI Dev Kit

- Setup a Vision AI Dev Kit
- Train a model using Customvision.ai and deploy the model to the device
- Train a model using Azure Notebooks and Azure Machine Learning service

## Pre-requisites

- Active Azure subscription
- Azure Machine Learning Workspace

## Additional Azure resources
- During this lab you will create:
  - IoT Hub and Edge Device to control the network traffic between your device and cloud
  - Cognitive services resources needed for customvision.ai
  - Azure Storage for deploying your customvision.ai model to the camera using module twin update
  
  If you already have some or all of these resources you can use existing ones. Otherwise the resources will be created during the lab

### Setup the camera

1. Connect your laptop to the camera allocated to you. The camera has a fresh firmware and should be blinking three red lights. That means it's running it's own access point and you can connect to it with your laptop and setup the device. You will find the access point name from the bottom of the camera. It will be in format of MSIOT_xxxxxx (xxxxxx is the last 6 characters of the device’s Wi-Fi mac address, e.g. MSIOT_BD097D). **Note** there are 30 of these devices running the access point at the same time, finding the correct one can be challenging.
2. If you have an existing IoT Hub and IoT Device defined access Azure portal and get a connection string for the IoT device.
3. Once connected to the camera (unless done automatically) please open your browser and access [setupaicamera.ms](https://setupaicamera.ms){:target="_blank"}
4. During the OOBE (Out-Of-Box Experience) Please connect the camera to **MSFTGUEST** Wifi. No password required.

**Note:** after the setup you will be able to stream the picture from the camera either to a browser or VLC / Open VC player. In order for that to work your laptop needs to be connected to the same network than the camera (MSFTGUEST) 

### Train an example model using CustomVision.ai

You will build a custom AI model to detect when someone is wearing a hard hat. You will use the [Azure Custom Vision service](https://customvision.ai){:target="_blank"} to build the model.

### Setup up a new Custom Vision project
- Login to Azure Custom Vision Service at [https://customvision.ai](https://customvision.ai){:target="_blank"}.

- Create a new project, us\ing these recommended settings:
    - Give it a name like `Simulated HardHat Detector`
    - Project Type - [Classification]
    - Use the existing resource group
    - Classification Type - [Multiclass (Single tag per image)]
    - Domain - [General(compact)] **NOTE: Ensure you do not select the `General` option**
    - Export Capabilites - Vision AI Dev Kit

### Upload and tag your training data
Some training images have already been collected for you for the hard hat use case.

- Download the .zip file containing the sample images from: <a href="https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL" target="blank">https://1drv.ms/u/s!AkzLzaBpSgoMo9hXX4NPjd8QrfhQLA?e=M3ehCL</a>
- Uncompress the zip file to a local directory
- Upload images to custom vision in batches, one batch per tag (images containing *HardHat* in the name, then *NoHardHat*), adding the appropriate tag during upload.

### Train and export your custom model

To train your model using the uploaded training images, go to your Custom Vision project and click on `Train`.

To export your model, select the `Performances` tab, then click the `Export` button. Choose the `Vision AI Dev Kit` option to download your model.

### Deploy your custom model to your camera

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the VisionSample module to use this new model. We will use a cloud blob store to store the model, but any publically accessible file storage system will work.

### Upload your trained model files

We'll start by creating a new storage account and then upload your model to it.

- Login to <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a>.
- Search for `Storage` and select `Storage accounts`.
- Use your existing Azure subscription and resource group.
- Create a new storage account with a unique name (NOTE: upper case characters are not allowed).
- Select the `West-US 2` region.
- Click on `Review+Create` (other default options should be correct).
- Wait until until provisioning is complete and navigate to your new storage account.
- From the `overview` tab, click on `Blobs`.
- Click `Add a new container`, give it a name like `hardhatmodel` and make sure to select `Container (anonymous read access for containers and blobs)` for the `Public access level`.
- Click on the container just created, then click  the `Upload` button and select the zip file you downloaded from the Azure Custom Vision service.
- Copy the URL of the uploaded file for later use.

### Update the configuration of the VisionSample module to use your custom model

- Login to <a href="http://portal.azure.com" target="blank">http://portal.azure.com</a> and go to the IoT Hub resource you created earlier.
- Click the `IoT Edge` tab, then click on IoT edge  device named `visionkit`.
- Click on the `AIVisionDevKitGetStartedModule`  name, then click `Module Identity Twin`.
- Update the zip file with the URL you saved earlier to *"ModelZipUrl": ""*, then click `Save`.

After a few minutes, your device should now be running your custom model!

### Test your new model

- Put on a hard hat on and smile at the camera!
- Verify the camera correctly classifies you as wearing a hard hat.

## Train and deploy a model using Azure Notebooks and Azure Machine Learning

* Train a model using Azure Machine Learning and Azure Notebooks.
* In this notebook you will:
  * Spin up a VM to your machine learning workspace
  * Upload data to train the model
  * Convert the model to a format that runs in Vision AI Dev Kit
  * Create a container
  * Create a new deployment.json that specifies the new module for the deployment
  * Deploy the module to Vision AI Dev Kit

### Pre-requisites

* Vision AI DevKit camera
* Azure Machine Learning workspace

### Clone example GitHub

* Log in to an existing [Azure Notebook](https://notebooks.azure.com/tedway/projects/vision-ai-dev-kit ){:target="_blank"} and clone it
* ![Clone GitHub]({{ '/assets/images/ANB_github_clone.PNG' | relative_url }})

### Prep your environment

* Change the aml_config/config.json file to match the subscription details for your Azure ML Workspace
* In case you want to use your own data go to the data folder and create a folder with your data, e.g. my_data. 
  * In the my_data folder, copy your data. Each folder name is the label of the images in that folder.  For example, the soda_cans folder looks like this:  
    * soda_cans 
    * coke 
    * ice 
    * pepsi 

* IMPORTANT: You MUST upload more than 35 images per folder so there’s enough data for training. 

### Run the notebook

* Open the 02-mobilenet-transfer-learning-final.ipynb notebook 

* Set the Kernel to Python 3.6

![Set kernel]({{ '/assets/images/NVM_set_kernel.PNG' | relative_url }})

* Run the notebook by running each cell individually

![Run notebook]({{ '/assets/images/ANB_run.PNG' | relative_url }})

* In case you don't want to run a cell you can change it to markdown

![Markdown cell]({{ '/assets/images/ANB_markdown.PNG' | relative_url }})

*Note* some cells contains two options, so please make sure that the option you don't use is set as markdown.

### Configure your IoT Hub details

* Change the cell content to reflect your IoT Hub. Please note that you can use format:
  * Iot_hub_name="youriothub"

![IotHub Details]({{ '/assets/images/ANB_iothub.PNG' | relative_url }})
