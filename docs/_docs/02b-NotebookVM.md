---
title: "Training model using Azure Machine Learning and Jupyter Notebook VM"
permalink: /docs/notebookvm/
excerpt: "Training model using Azure Machine Learning and Jupyter Notebook VM"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-06-03
---

## What you will do

- Create a Notebook VM to your Azure Machine Learning Workspace 
- Train a model using Azure Machine Learning and Notebook VM. Deploy the model to your Vision AI Dev Kit device

### Pre-requisites

- Vision AI DevKit camera
- Azure Machine Learning workspace

### Create Notebook VM

- Log in to [Azure Portal](https://ms.portal.azure.com){:target="_blank"} and access Azure Machine Learning workspace
- Create a new Notebook VM
- ![Create new Notebook VM]({{ '/assets/images/NVM_create_new.PNG' | relative_url }})

### Clone example notebooks from GitHub

-	Add an access token to your GitHub account (if not exist yet). This is needed for being able to [clone a private GitHub](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line){:target="_blank"}. In this case the password when cloning a GitHub is your token.
- Open the Notebook VM
![Create new Notebook VM]({{ '/assets/images/NVM_open_notebook.PNG' | relative_url }})
- Open "Terminal"
![Create new Notebook VM]({{ '/assets/images/NVM_open_terminal.PNG' | relative_url }})
- Note that if you use Edge as your browser the terminal many not open directly. In that case you can access it from "Running" tab.

![Create new Notebook VM]({{ '/assets/images/NVM_edge.PNG' | relative_url }})

`git clone --recursive https://github.com/microsoft/vision-ai-developer-kit`

### Prep your environment

* Change the aml_config/config.json file to match the subscription details for your Azure ML Workspace
* In case you want to use your own data go to the data folder and create a folder with your data, e.g. my_data. 
  * In the my_data folder, copy your data.  Each folder name is the label of the images in that folder.  For example, the soda_cans folder looks like this:  
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

### Configure your IoT Hub details

* Change the cell content to reflect your IoT Hub. Please note that you can use format:
  * Iot_hub_name="youriothub"

![IotHub Details]({{ '/assets/images/ANB_iothub.PNG' | relative_url }})
