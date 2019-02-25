---
title: "Deploy a Model using Visual Studio Code"
permalink: /docs/Deploy_Model_VS_Code/
excerpt: "Using Visual Studio Code deployment to deploy models to the Vision AI DevKit hardware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-25
---
This page will help you deploy the pre-built vision model to your device using **Visual Studio (VS) Code**.


## What you will do
* Configure a VS Code dev environment
* Deploy the pre-built sample model container image through VS Code

## What you will need
* Latest version of Visual Studio (VS) Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"}
* Python 3.6 by Anaconda [(Download Here)](https://www.anaconda.com/download/){:target="_blank"}
* Vision Dev Kit sample model [(Download Here)]()
* USB-C cable to connect Dev Kit hardware to your PC.
* HDMI cable to connect Dev Kit hardware to a monitor.
* Active Wi-Fi access point with Internet connectivity.
* Latest Vision Dev Kit hardware firmware installed.

## Setup and Configure Visual Studio (VS) Code for container deployment to the Vision AI Dev Kit
1. If not already available, install VS Code using the link above.
2. If not already avialable, install Python 3.6 by Anaconda (using default options) using the link above.

   * Once installed, open the **Anaconda Prompt** from *Start Menu\Programs\Anaconda3 (64-bit)*
   * Create a Python 3.6 runtime environment using the command:  *conda create -n py36 python=3.6 anaconda* (Press y when it asks Proceed ([y]/n)?)
   * Activate the environment using the command:   *conda activate py36* or selecting *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (py36)*

3. Open VS Code and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**

4. Install the **Azure ML SDK** and required packages. (If you choose to use the sample code as-is, skip to: *Deploy a Model Container Image to the Vision AI Dev Kit hardware in Visual Studio Code*)

    Note: When installing the Azure Machine Learning SDK or related Python packages, there are some Python packages which depend on specific versions of other Python packages. If these (dependency) Python packages versions are too high, the installation will fail. To work around this issue, you will need to create a *requirements.txt* file in the VisionAIDevKit root folder (ex. c:\visionaidevkit\requirements.txt) which has stricter versions defined.

    Recommended content:
    > azure-cli-core==2.0.55
    > azure-mgmt-containerregistry==2.6.0
    > azure-mgmt-resource==2.0.0
    > azureml-core==1.0.8
    > azureml-contrib-iot==1.0.8
    > msgpack==0.6.1
    > PyYAML==4.2b1
    > pyqt5==5.9.2
    > wheel==0.30.0
    > easydict==1.9
    > tensorflow==1.12.0

