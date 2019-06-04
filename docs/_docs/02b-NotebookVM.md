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

- Open the Notebook VM
![Create new Notebook VM]({{ '/assets/images/NVM_open_notebook.PNG' | relative_url }})
- Open "Terminal"
![Create new Notebook VM]({{ '/assets/images/NVM_open_terminal.PNG' | relative_url }})
- Note that if you use Edge as your browser the terminal many not open directly. In that case you can access it from "Running" tab.

![Create new Notebook VM]({{ '/assets/images/NVM_edge.PNG' | relative_url }})

`git clone --recursive https://github.com/microsoft/vision-ai-developer-kit`


