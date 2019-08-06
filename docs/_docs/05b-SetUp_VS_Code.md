---
title: "Setup Visual Studio Code environment for Vision ML"
permalink: /docs/SetUp_VS_Code/
excerpt: "Visual Studio Code setup instructions for Windows, Linux and MacOS"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-07-03
---

## What you will do

* Install a Visual Studio (VS) Code dev environment for Windows, Linux or MacOS
* Setup and Configure Visual Studio (VS) Code for container deployment
* Clone Vision AI Dev Kit GitHub repository using VS Code sample

## What you will need

* VS Code
* Python 3.7 by Anaconda
* Azure Machine Learning, Azure IoT Hub Toolkit and Azure Iot Edge extensions for VS Code
* Azure user account with configured Azure IoT Hub

## Windows users

### Setup and Configure Visual Studio (VS) Code for container deployment

1. If not already available, install VS Code [(Download)](https://code.visualstudio.com/){:target="_blank"} and Python 3.7 by Anaconda (using default options). [(Download)](https://www.anaconda.com/download){:target="_blank"}

2. Once installed, open the **Anaconda Prompt** from *Start Menu\Programs\Anaconda3 (64-bit)*

3. Open VS Code. Click the Extensions icon in the Activity Bar (left side) and install Vision AI Dev Kit extension. It bundles together several other needed extensions:
    ![VS Cpde extensions]({{ '/assets/images/VSC_Deploy_extension.png' | relative_url }})

   * For more information on installing extensions in VS Code, see [Managing Extensions in Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-gallery){:target="_blank"}

4. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py){:target="_blank"} and required packages.

    * Note: When installing the Azure Machine Learning SDK or related Python packages, there are some Python packages which depend on specific versions of other Python packages. If these (dependency) Python packages versions are too high, the installation will fail. To work around this issue, there is a *requirements.txt* in GitHub under [VisionSample\MachineLearning\scripts](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/samples/research/VisionSample/MachineLearning/scripts){:target="_blank"} folder that can be used to specify correct versions. Please copy the file in the VisionAIDevKit root folder (ex. c:\visionaidevkit\requirements.txt) which has stricter versions defined. Below is the content of the file if you prefer creating it locally.

    Recommended requirements.txt contents:

    ```terminal
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

5. Use the **Anaconda Prompt (base)** as an administrator, then execute the following command lines:

    ```cmd
    pip install --upgrade -r requirements.txt
    ```

6. Restart Visual Studio Code in the Python 3.7 runtime environment, by executing the following command in an **Anaconda Prompt (base)** window:

    ```cmd
    code
    ```

      This will enable VS code to inherit the environment variables of the **Python 3.7** runtime environment.
7. Open the *command palette* in VS Code *(Ctrl-Shift-P)*, then enter

    ```cmd
    Python: Select Interpreter
    ```

    to select your Python interpreter (*Python 3.7*)
8. In the VS Code *command pallette*, enter

    ```cmd
    Azure: Sign In
    ```

    to sign in to your Azure account and select your subscription.

9. Create a new workspace in VS Code as described in [Get started with Azure Machine Learning for Visual Studio Code](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-vscode-tools){:target="_blank"}. You can also use 00-aml-configuration.py script described in the next section to create a new workspace.

## Linux and MacOS users

Linux/iOS - these instructions are in draft form and are still being improved

For Linux these have been tested for Ubuntu or Ubuntu VM version 18.04.

### Install and configure required tools

   1. Install the build tools.

      ```cmd
      sudo apt-get install build-essential checkinstall
      sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev
         \ libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
      sudo apt-get install libffi-dev
      ```

   2. Download Python 3.7.2.

      ```cmd
      cd /usr/src
      sudo wget https://www.python.org/ftp/python/3.7.2/Python-3.7.2.tgz
      ```

   3. Extract tgz

      ```cmd
      sudo tar xzf Python-3.7.2.tgz
      ```

   4. Compile.

      ```cmd
      cd Python-3.7.2
      sudo ./configure --enable-optimizations
      sudo make altinstall
      ```

   5. Add alias into ~/.bashrc

      ```cmd
      alias python='/usr/local/bin/python3.7m'
      ```

   6. Install pip:

       ```cmd
       curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
       sudo python get-pip.py
       sudo pip install --upgrade pip
       ```

### Setup and Configure Visual Studio (VS) Code for container deployment

1. Install VS Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"}

2. Open VS Code. Click the Extensions icon in the Activity Bar (left side) and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**
      * For more information on installing extensions in VS Code, see [Managing Extensions in Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-gallery){:target="_blank"}

3. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py){:target="_blank"} and required packages.

### Clone GitHub

1.	Open command palette ("View" -> "Command palette")
   - Select "Azure IoT Edge Show Sample Gallery"
   - Click Vision AI Developer Kit -> Open Sample
   - Select local folder to use to store the sample solution

 ![Open sample]({{ '/assets/images/VSC_Deploy_Open_Sample.png' | relative_url }})

 ![GitHub view in VS Code]({{ '/assets/images/VSC_Deploy_GitHub_view.png' | relative_url }})