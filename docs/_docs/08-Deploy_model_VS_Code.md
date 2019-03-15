---
title: "Deploy model: VS Code"
permalink: /docs/Deploy_Model_VS_Code/
excerpt: "Using Visual Studio Code deployment to deploy models to the Vision AI DevKit hardware."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-03-15
---
The easiest way to deploy Vision AI models to the Vision AI DevKit is through the use of **Visual Studio (VS) Code**.

## What you will do
* Configure a VS Code dev environment
* Deploy the pre-built sample model container image through VS Code

## What you will need
* Latest version of Visual Studio (VS) Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"}
* Python 3.6 by Anaconda [(Download Here)](https://www.anaconda.com/download/){:target="_blank"}
* Vision Dev Kit sample model - [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample).
* Latest Azure Machine Learning SDK for Python [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py)
* Azure IoT Hub and Azure IoT Edge device configured for your Vision AI DevKit hardware [(Instructions)]({{ '/docs/Setup_Azure_resources/' | relative_url}})
* USB-C cable to connect Dev Kit hardware to your PC.
* HDMI cable to connect Dev Kit hardware to a monitor.
* Active Wi-Fi access point with Internet connectivity.
* Latest Vision Dev Kit hardware firmware installed.

## Setup and Configure Visual Studio (VS) Code for container deployment to the Vision AI Dev Kit
1. If not already available, install VS Code [(Download Here)](https://code.visualstudio.com/){:target="_blank"} and Python 3.6 by Anaconda (using default options). [(Download here)](https://www.anaconda.com/download){:target="_blank"}

    * Select the check-box to 'Add Anaconda to the system PATH environment variables' in the *Advanced Installation Options* (as shown below) during the Anaconda install.  
        ![Screen shot of Anaconda installation dialog box to add Anaconda to the system PATH variables]({{ '/assets/images/Anaconda_path_set_screenshot.png' | relative_url }})

    * Once installed, open the **Anaconda Prompt** from *Start Menu\Programs\Anaconda3 (64-bit)*
    * Create a Python 3.6 runtime environment using the command:
     ```
     conda create -n py36 python=3.6 anaconda
     ```
    * Press 'y' when asked '*Proceed (y/n)?*'
    * Activate the environment using *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (py36)* or the command line:
     ```
     conda activate py36
     ```  
2. Open VS Code. Click the Extensions icon in the Activity Bar (left side) and install the following extensions:
    * **Azure Machine Learning** (this will automatically add **Azure Account** and **Microsoft Python** extensions)
    * **Azure IoT Hub Toolkit**
    * **Azure IoT Edge**
    * **Docker extension**
      * For more information on installing extensions in VS Code, see [Managing Extensions in Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-gallery)
3. Install the **Azure ML SDK** [(Instructions)](https://docs.microsoft.com/en-us/python/api/overview/azure/ml/install?view=azure-ml-py) and required packages. If you choose to use the sample code as-is, skip to: [*Deploy a Model Container Image to the Vision AI Dev Kit hardware in Visual Studio Code*]( {{'/docs/Deploy_Model_VS_Code/#deploy-a-model-container-image-to-a-vision-ai-dev-kit-device-in-visual-studio-code' | relative_url}} )

    * Note: When installing the Azure Machine Learning SDK or related Python packages, there are some Python packages which depend on specific versions of other Python packages. If these (dependency) Python packages versions are too high, the installation will fail. To work around this issue, you will need to create a *requirements.txt* file in the VisionAIDevKit root folder (ex. c:\visionaidevkit\requirements.txt) which has stricter versions defined.

    Recommended requirements.txt contents:
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

4. Open the **Anaconda Prompt (py36)** as an administrator (right-click *Start Menu\Programs\Anaconda3 (64-bit)\Anaconda Prompt (py36)*, choose *run as administrator*), then execute the following command lines:
      ```
      pip install --ignore-installed PyYAML==4.2b1 
      pip install --upgrade -r requirements.txt
      ```
5. Restart Visual Studio Code in the Python 3.6 runtime environment, by executing the following command in an **Anaconda Prompt (py36)** window:
    ```
    code
    ```
      This will enable VS code to inherit the environment variables of the **Python 3.6** runtime environment.
6. Open the *command palette* in VS Code *(Ctrl-Shift-P)*, then enter 
    ```
    Python: Select Interpreter
    ```
    to select your Python interpreter (*Python 3.6*)
7. In the VS Code *command pallette*, enter 
    ```
    Azure: Sign In
    ```
    to sign in to your Azure account and select your subscription.

8. Create a new workspace in VS Code as described in [Get started with Azure Machine Learning for Visual Studio Code](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-vscode-tools). You can also use 00-aml-configuration.py script described in the next section to create a new workspace.

## Deploy a Model Container Image to a Vision AI Dev Kit device in Visual Studio Code

1. Download or Clone the latest Visual Studio Code sample from the [GitHub repository](https://github.com/Microsoft/vision-ai-developer-kit/tree/master/sample-solutions/VisionSample).
2. Launch Visual Studio Code, and select [File > Open Folder…] command to open the “VisionSample” directory as the workspace root.
3. Use the [Python: Select Interpreter] command in the command palette box or click the current “Python interpreter” option on the bottom line to set "python.pythonPath" in .vscode\settings.json.
![Setting the pythonPath screen shot]({{ '/assets/images/VSC_Deploy_Python_Path.png' | relative_url }}) 
4. Open “00-aml-configuration.py” under “VisionSample\MachineLearning\scripts” folder and replace the following 3 default settings with your Azure Machine Learning Service Workspace settings:
![Setting the pythonPath screen shot]({{ '/assets/images/VSC_Deploy_mod_00-aml-configuration.py_screenshot.png' | relative_url }})
5. Click the [Run Cell] or [Run All Cells] link on the top line of the cell. A new workspace will be created, if one does not already exist, along with a “config.json” file under the “VisionSample\aml_config” folder.  
![Modify config.json screen shot]({{ '/assets/images/VSC_Deploy_config-json_screenshot.png' | relative_url }}) 
6. Open “01-convert-model-containerize.py” under the “VisionSample\MachineLearning\scripts” folder and click the [Run Cell] or [Run All Cells] link to: register the model, convert the model, create a container image, and write settings related to the container image to the “.env” file under the “VisionSample\EdgeSolution” folder.
  * Note: This .py script will import *current_config.py* under the *VisionSample\MachineLearning\scripts\model_configs* folder to process the model specified in *current_config.py*.  The script can be reused to process a different model by changing *current_config.py’s* content. The initial content in *current_config.py* is for the pre-trained model *imagenet_2_frozen.pb* located in the *VisionSample\MachineLearning\models\mobilenet-imagenet\orig* folder.
![Initial contents of current_config.json screen shot]({{ '/assets/images/VSC_Deploy_current-config-py_Initial_content_screenshot.png' | relative_url }})
7. Right click the *deployment.template.json* file under the *VisionSample\EdgeSolution* folder and select **Generate IoT Edge Deployment Manifest** to create a new *deployment.json* file under *VisionSample\EdgeSolution\config* folder.  
![Open deployment.template.json screen shot]({{ '/assets/images/VSC_Deploy_open_deployment-template-json_screenshot.png' | relative_url }}) 
8. Click the [Explorer] icon, then click […] in the **AZURE IOT HUB DEVICES** section on the right side. Click **Select IoT Hub** to select your Azure IoT Hub.
9. Expand the **AZURE IOT HUB DEVICES** section. Right-click your IoT Edge device, then select **Create Development for Single Device**. Click the *deployment.json* file under the *VisionSample\EdgeSolution\config* folder, then click the **Select Edge Deployment Manifest** button to deploy the container image to the IoT Edge device (your Vision AI DevKit hardware).
![Open deployment.template.json from VSC Screenshot]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot.png' | relative_url }})  
 ![Open deployment.template.json from VSC Screenshot #2]({{ '/assets/images/VSC_Deploy_Select-Edge-Deployment-Manifest_screenshot2.png' | relative_url }})
10.	Configure the device as an IoT Edge device using the connection string for your Vision AI DevKit, obtained earlier.
11.	Monitor the deployment status for the AI Vision Kit device by the command lines
```
adb shell docker ps
adb shell docker logs edgeAgent
```
![Use ADB to monitor deployment status Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_monitor_deployment_screenshot.png' | relative_url }})
12.	Check object detection results using the command line
```
adb shell iotedge logs <module name>
```
(e.g. “iotedge logs VisionSampleImagenet”.)
Mobilenet-imagenet model can detect the 1000 object classes listed in the  *VisionSample\MachineLearning\models\mobilenet-imagenet\orig\output_labels.txt*.

    ![Use ADB to module impage outputs Screenshot]({{ '/assets/images/VSC_Deploy_Using_ADB_to_check_detection_results_screenshot.png' | relative_url }})

If the Vision AI DevKit camera is connected to an  external screen through HDMI, you should be able to see bounding boxes with text indictating detection, as below.
![Image of a display showing recognition box with text]({{ '/assets/images/VSC_Deploy_object_detection_screenshot.png' | relative_url }})

In VS Code, select **AZURE IOT HUB DEVICES > … > Select IoT Hub** and then **AZURE IOT HUB DEVICES > … > Start Monitoring D2C Message** command to monitor the messages sent from the AI Vision DevKit to your Azure IoT Hub.
    ![Screenshot of message monitoring output]({{ '/assets/images/VSC-Deploy-Monitor-messages.png' | relative_url }})

## Retraining the machine learning model
1. Open *02-mobilenet-transfer-learning-cloud.py* and click **Run Cell** or **Run All Cells** to train a new mobilenet model in the cloud using *soda_cans* data under the *VisionSample\MachineLearning\data\soda_cans* folder.
2. After **Run All Cells** execution has completed, it will write a *va-snpe-engine-library_config.json* config file to the new model folder, the write the model config file to *VisionSample\MachineLearning\scripts\model_configs* and overwrite *current_config.py*.
3. Repeat steps 6 and 7 in the previous section to open and execute *01-convert-model-containerize.py*, using the newly generated *deployment.json* to deploy the new model image *retrained_graph.pb* under the *VisionSample\MachineLearning\models\mobilenet-retrain-cloud\outputs* folder.
