---
title: "Setup VS Code environment"
permalink: /docs/SetUp_VS_Code/
excerpt: "Visual Studio Code setup instructions for Windows, Linux and MacOS"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---

* Instructions for Windows, Linux and MacOS users

## What you will do
* Configure a VS Code dev environment

## What you will need
* Latest version of Visual Studio (VS) Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"}
* Python 3.7 by Anaconda [(Download Here)](https://www.anaconda.com/download/){:target="_blank"}
* Latest Azure Machine Learning SDK for Python [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py)
* Azure subscription with configured Azure IoT Hub

## Windows users

### Setup and Configure Visual Studio (VS) Code for container deployment to the Vision AI Dev Kit
1. If not already available, install VS Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"} and Python 3.7 by Anaconda (using default options). [(Download here)](https://www.anaconda.com/download){:target="_blank"}

  

    * Once installed, open the **Anaconda Prompt** from *Start Menu\Programs\Anaconda3 (64-bit)*
    
2. Open VS Code. Click the Extensions icon in the Activity Bar (left side) and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**
      * For more information on installing extensions in VS Code, see [Managing Extensions in Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-gallery)
3. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py) and required packages.

    * Note: When installing the Azure Machine Learning SDK or related Python packages, there are some Python packages which depend on specific versions of other Python packages. If these (dependency) Python packages versions are too high, the installation will fail. To work around this issue, there is a *requirements.txt* in GitHub under [VisionSample\MachineLearning\scripts](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample/MachineLearning/scripts) folder that can be used to specify correct versions. Please copy the file in the VisionAIDevKit root folder (ex. c:\visionaidevkit\requirements.txt) which has stricter versions defined. Below is the content of the file if you prefer creating it locally.

    Recommended requirements.txt contents:
    ```
      azure-cli-core==2.0.60
      azure-mgmt-containerregistry==2.7.0
      azure-mgmt-resource==2.1.0
      azureml-contrib-iot==1.0.18
      azureml-core==1.0.18
      easydict==1.9
      numpy==1.16
      tensorflow==1.13.1
      wheel==0.30.0
     ```

4. Open the **Anaconda Prompt (base)** as an administrator (right-click *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (base)*, choose *run as administrator*), then execute the following command lines:
      ```
      pip install --upgrade -r requirements.txt
      ```
5. Restart Visual Studio Code in the Python 3.7 runtime environment, by executing the following command in an **Anaconda Prompt (base)** window:
    ```
    code
    ```
      This will enable VS code to inherit the environment variables of the **Python 3.7** runtime environment.
6. Open the *command palette* in VS Code *(Ctrl-Shift-P)*, then enter 
    ```
    Python: Select Interpreter
    ```
    to select your Python interpreter (*Python 3.7*)
7. In the VS Code *command pallette*, enter 
    ```
    Azure: Sign In
    ```
    to sign in to your Azure account and select your subscription.

8. Create a new workspace in VS Code as described in [Get started with Azure Machine Learning for Visual Studio Code](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-vscode-tools). You can also use 00-aml-configuration.py script described in the next section to create a new workspace.

## Linux and MacOS users

Linux/iOS - Note these insturctions are draft and are still being improved

For Linux these have been tested for Ubuntu or Ubuntu VM version 18.04.

### Setup and Configure Visual Studio (VS) Code for container deployment to the Vision AI Dev Kit
1. If not already available, install VS Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"} and Python 3.7 by Anaconda (using default options). [(Download here)](https://www.anaconda.com/download){:target="_blank"}

    * Select the check-box to 'Add Anaconda to the system PATH environment variables' in the *Advanced Installation Options* (as shown below) during the Anaconda install.  
        ![Screen shot of Anaconda installation dialog box to add Anaconda to the system PATH variables]({{ '/assets/images/Anaconda_path_set_screenshot.png' | relative_url }})

    * Once installed, open the **Anaconda Prompt**
    
2. Open VS Code. Click the Extensions icon in the Activity Bar (left side) and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**
      * For more information on installing extensions in VS Code, see [Managing Extensions in Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-gallery)
      
3. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py) and required packages. 

### Install and configure development software.
   1. Install the build tools.

      ```terminal
      sudo apt-get install build-essential checkinstall
      sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev
         \ libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
      sudo apt-get install libffi-dev
      ```

   2. Download Python 3.7.2.

      ```terminal
      cd /usr/src
      sudo wget https://www.python.org/ftp/python/3.7.2/Python-3.7.2.tgz
      ```

   3. Extract tgz: `sudo tar xzf Python-3.7.2.tgz`
   
   4. Compile.

      ```terminal
      cd Python-3.7.2
      sudo ./configure --enable-optimizations
      sudo make altinstall
      ```

   5. Add alias into ~/.bashrc: `alias python='/usr/local/bin/python3.7m'`
   
   6. Install pip:

       ```terminal
       curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
       sudo python get-pip.py
       sudo pip install --upgrade pip
       ```

