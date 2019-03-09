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
* Vision Dev Kit sample model - [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/sample-solution-1).
* Latest Azure Machine Learning SDK for Python [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py)
* USB-C cable to connect Dev Kit hardware to your PC.
* HDMI cable to connect Dev Kit hardware to a monitor.
* Active Wi-Fi access point with Internet connectivity.
* Latest Vision Dev Kit hardware firmware installed.

## Setup and Configure Visual Studio (VS) Code for container deployment to the Vision AI Dev Kit
1. If not already available, download and install VS Code. [(Download Here)](https://code.visualstudio.com/){:target="_blank"}
2. If not already available, install Python 3.6 by Anaconda (using default otpions). [(Download here)](https://www.anaconda.com/download){:target="_blank"}
2. If not already available, install Python 3.6 by Anaconda (using default options). [(Download Here)](https://www.anaconda.com/download/){:target="_blank"}

    * Note: You must select the check-box to 'Add Anaconda to the system PATH environment variables' (as shown below) during the Anaconda install.

        ![Screen shot of Anaconda installation dialog box to add Anaconda to the system PATH variables]({{ '/assets/images/Anaconda_path_set_screenshot.png' | relative_url }})
   * Once installed, open the **Anaconda Prompt** from *Start Menu\Programs\Anaconda3 (64-bit)*
   * Create a Python 3.6 runtime environment using the command:
   ```
   conda create -n py36 python=3.6 anaconda
   ```
      (Press y when it asks Proceed (y/n)?)
   * Activate the environment using the command:
   ```
   conda activate py36
   ```
      or selecting *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (py36)*
3. Open VS Code and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**
  ![Screen shot of VSCode Extension installation dialog]({{ '/assets/images/VSCode_Extension_Install.png' | relative_url }})
4. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py) and required packages. (If you choose to use the sample code as-is, skip to: [*Deploy a Model Container Image to the Vision AI Dev Kit hardware in Visual Studio Code*]( {{'/docs/Deploy_Model_VS_Code/#deploy-a-model-container-image-to-a-vision-ai-dev-kit-device-in-visual-studio-code' | relative_url}} ))
    Note: When installing the Azure Machine Learning SDK or related Python packages, there are some Python packages which depend on specific versions of other Python packages. If these (dependency) Python packages versions are too high, the installation will fail. To work around this issue, you will need to create a *requirements.txt* file in the VisionAIDevKit root folder (ex. c:\visionaidevkit\requirements.txt) which has stricter versions defined.

    Recommended contents:
    ```
      azure-cli-core==2.0.55
      azure-mgmt-containerregistry==2.6.0
      azure-mgmt-resource==2.0.0
      azureml-core==1.0.8
      azureml-contrib-iot==1.0.8
      msgpack==0.6.1
      PyYAML==4.2b1
      pyqt5==5.9.2
      wheel==0.30.0
      easydict==1.9
      tensorflow==1.12.0
      ```
5. Open the **Anaconda Prompt (py36)** as an administrator (right-click *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (py36)*, then choose *run as administrator*) then execute the following command:
      ```
      pip install --ignore-installed PyYAML==4.2b1 
      pip install --upgrade -r requirements.txt
      ```
6. Restart Visual Studio Code in the Python 3.6 runtime environment, by executing the following command in an **Anaconda Prompt (py36)** window:
    ```
    code
    ```
      This will enable VS code to inherit the environment variables of the **Python 3.6** runtime environment.
7. Open the *command palette* in VS Code *(Ctrl-Shift-P)*, then enter 
    ```
    Python: Select Interpreter
    ```
    to select your Python interpreter (*Python 3.6*)
8. In the VS Code *command pallette*, enter 
    ```
    Azure: Sign In
    ```
    to sign in to your Azure account and select your subscription.
9. Create a new IoT Hub with an IoT Edge device using the instructions found in [Setup Azure resources]({{ '/docs/Setup_Azure_Resources' | relative_url }}).
  Note: If you have an exisitng IoT Hub and Edge device(s) already created for your Vision AI DevKit hardware, you can reuse them instead of creating new ones.
10. Create a new workspace in VS Code as described in [Get started with Azure Machine Learning for Visual Studio Code](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-vscode-tools). You can also use 00-aml-configuration.py script described in the next section to create a new workspace.

## Deploy a Model Container Image to a Vision AI Dev Kit device in Visual Studio Code
1. Download or Clone the latest Visual Studio Code sample from the [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/sample-solution-1).
2.	Launch Visual Studio Code, and select [File > Open Folder…] command to open the “sample-solution-1” directory as workspace root.
3.	Use the [Python: Select Interpreter] command in the command palette box or click the current “Python interpreter” option on the bottom line to set "python.pythonPath" in .vscode\settings.json.
![Setting the pythonPath screen shot]({{ '/assets/images/VSC_Deploy_Python_Path.png' | relative_url }}) 
4.	Install Azure ML SDK and required packages (Skip this step if you already did step 4 of previous section)
  * Close VS Code and launch VS Code again by “Run as administrator”.
  * Select [Terminal > New Terminal] command to open a terminal window, change directory to “sample-solution-1\MachineLearning\scripts”, and execute the following commands to install required Python packages: 
    ```
    pip install msgpack==0.6.1 
    pip install --ignore-installed PyYAML==4.2b1 
    pip install --upgrade -r requirements.txt 
    ```
Note: The above installation steps works for the latest Azure Machine Learning SDK version v1.0.8 and install Python 3.6.5 by Anaconda with Python version 3.6.5 link. If the version of AML SDK, Python, or other packages will be changed in the future, you might have to install or upgrade packages manually.
5.	Open “00-aml-configuration.py” under “sample-solution-1\MachineLearning\scripts” folder and replace the following 3 fake settings to your Azure Machine Learning Service Workspace settings:
![Setting the pythonPath screen shot]({{ '/assets/images/VSC_Deploy_mod_00-aml-configuration.py_screenshot.png' | relative_url }})
6.	Click [Run Cell] or [Run All Cells] link on the top line of the cell.  It will create a new workspace if it doesn’t exist and write a “config.json” file under “sample-solution-1\aml_config” folder.
![Modify config.json screen shot]({{ '/assets/images/VSC_Deploy_config-json_screenshot.png' | relative_url }}) 
7.	Open “01-convert-model-containerize.py” under “sample-solution-1\MachineLearning\scripts” folder and click [Run Cell] or [Run All Cells] link to register model, convert model, create container image, and write settings related to the container image to “.env” file under “sample-solution-1\EdgeSolution” folder.
Note: This .py script will import “current_config.py” under “sample-solution-1\MachineLearning\scripts\model_configs” folder to process the model specified in “current_config.py”.  So, it can be reused to process different model by changing current_config.py’s content.  The initial content in current_config.py is for the pre-trained model “imagenet_2_frozen.pb” under “sample-solution-1\MachineLearning\models\mobilenet-imagenet\orig” folder.
![Initial contents of current_config.json screen shot]({{ '/assets/images/VSC_Deploy_current-config-py_Initial_content_screenshot.png' | relative_url }}) 
8.	Right click “deployment.template.json” file under “sample-solution-1\EdgeSolution” folder and select [Generate IoT Edge Deployment Manifest] command to create a new “deployment.json” file under “sample-solution-1\EdgeSolution\config” folder.
![Open deployment.template.json screen shot]({{ '/assets/images/VSC_Deploy_open_deployment-template-json_screenshot.png' | relative_url }}) 
9.	Click [Explorer] icon, click […] at [AZURE IOT HUB DEVICES] section right side, and select [Select IoT Hub] command to select an IoT Hub.
10.	 Expand [AZURE IOT HUB DEVICES] section, right-click an IoT edge device, select [Create Development for Single Device] command, select “deployment.json” file under “sample-solution-1\EdgeSolution\config” folder, and click [Select Edge Deployment Manifest] button to deploy the container image to the IoT edge device.
![Open deployment.template.json from VSC Screenshot]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot.png' | relative_url }})  
 ![Open deployment.template.json from VSC Screenshot #2]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot2.png' | relative_url }})
11.	Configure device as IoT Edge device using the connection string for Iot Edge device used in step 10 above to deployment the manifest. 
12.	Monitor the deployment status for the AI Vision Kit device by using platform tools commands: [adb shell], [docker ps] and [docker logs edgeAgent] commands.
![Use ADB to monitor deployment status Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_monitor_deployment_screenshot.png' | relative_url }})
13.	Check object detection results:
(mobilenet-imagenet model can detect 1000 object classes listed in the "sample-solution-1\MachineLearning\models\mobilenet-imagenet\orig\output_labels.txt")
  *	Use platform tools commands [adb shell > iotedge logs <module name>]  (e.g. “iotedge logs sample-solution-1Imagenet”) to check module image outputs.
![Use ADB to module impage outputs Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_check_detection_results_screenshot.png' | relative_url }})    

If the Vision AI DevKit camera is connected to an  external screen through HDMI, you should be able to see detection on screen as below.
![Image of a display showing recognition box with text]({{ '/assets/images/VSC_Deploy_object_detection_screenshot.png' | relative_url }})
 
•	Select [AZURE IOT HUB DEVICES > … > Select IoT Hub] command and [AZURE IOT HUB DEVICES > … > Start Monitoring D2C Message] command to monitor the messages sent from AI Vision Kit device to Azure IoT Hub:
 
## Retraining the Machine learning models
1.	Open “02-mobilenet-transfer-learning-cloud.py” and click [Run Cell] or [Run All Cells] link to retrain a new mobilenet model on cloud by “soda_cans” data under “sample-solution-1\MachineLearning\data\soda_cans” folder.
 
2.	After [Run All Cells] execution finished, it will write a “va-snpe-engine-library_config.json” config file to its new model folder, write its model config file to “sample-solution-1\MachineLearning\scripts\model_configs” and overwrite “current_config.py”.
 
3.	Repeat step 7 and 8 to open and execute “01-convert-model-containerize.py” and use the new generated “deployment.json” to deploy the new model image “retrained_graph.pb” under “sample-solution-1\MachineLearning\models\mobilenet-retrain-cloud\outputs” folder.
4.	Open “03-mobilenet-transfer-learning-local.py” and click [Run Cell] or [Run All Cells] link to retrain a new mobilenet model on a local machine by “soda_cans” data under “sample-solution-1\MachineLearning\data\soda_cans” folder.  It will write a “va-snpe-engine-library_config.json” config file to its new model folder, write its model config file to “sample-solution-1\MachineLearning\scripts\model_configs” and overwrite “current_config.py”.
 
5.	Repeat step 7 and 8 to open and execute “01-convert-model-containerize.py” and use the new generated “deployment.json” to deploy the new model image “retrained_graph_local.pb” under “sample-solution-1\MachineLearning\models\mobilenet-retrain-local” folder. 
