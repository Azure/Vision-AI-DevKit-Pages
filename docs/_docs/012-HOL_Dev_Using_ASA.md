---
title: "Hands on Lab - Using Azure Stream Analytics (ASA) to create alerts"
permalink: /docs/Tutorial-HOL_Using_ASA_for_alerts/
excerpt: "How to use ASA and the Vision AI DevKit to create alerts."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-22
---
## Overview

Vision AI models object detection (such as finding a product missing on a retail shelf), can transform cameras into sensors. Combining Azure Stream Analytics and Azure IoT Edge, you can bring the necessary business logic to the camera itself. Processing telemetry streams at the edge can reduce the amount of data uploaded to the cloudand reduce the time it takes to react.

Like many sensors, the data generated can be noisy. To avoid false alerts, Azure Stream Analytics (ASA) at the edge can smooth out results, raising an alert only when required.

Azure Stream Analytics provides a richly structured query syntax for data analysis both in the cloud and on IoT Edge devices. For more information about Azure Stream Analytics on IoT Edge, see [Azure Stream Analytics documentation](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-edge){:target="_blank"}.

To do that, we will build and deploy an ASA module at the edge.

The type of telemetry data sent by Custom Vision models output a different format than in the above tutorial. So we will need to adjust the ASA query to account for that. Here is an example of an ASA query taking inputs from Custom Vision models and smoothing out results before raising an alert when a tag is consistently found after 1 full second: **ASA query code to be provided by ASA team**

## What you will do

* Create an Azure Stream Analytics job to process data on the edge.
* Connect the new Azure Stream Analytics job with other IoT Edge modules.
* Deploy the Azure Stream Analytics job to an IoT Edge device from the Azure portal.

  ![Diagram - Tutorial architecture, stage and deploy ASA job]({{ '/assets/images/asa-architecture.png' | relative_url }})

## What you will need

* Configured Vision AI DevKit
* Configured Azure IoT Hub

## Create an Azure Stream Analytics (ASA) job

In this section, you create an Azure Stream Analytics job to take data from your IoT hub, query the sent telemetry data from your device, and then forward the results to an Azure Blob storage container.

### Create a storage account

When you create an Azure Stream Analytics job to run on an IoT Edge device, it needs to be stored in a way that can be called from the device. You can use an existing Azure storage account, or create a new one now.

1. In the Azure portal, go to **Create a resource** > **Internet of Things** > **Stream Analytics Job**..

2. Provide the following values to create your storage account:

    | Field| Value |
    |-------|--------|
    |Name| Provide a unique name for your storage account.|
    |Location|Choose a location close to you.|
    |Subscription|Choose the same subscription as your IoT hub.|
    |Resource group|We recommend that you use the same resource group for all test resources you create during Vision AI DevKit quick starts and tutorials.|

3. Keep the default values for the other fields and select **Create**.

### Create a new job

1. In the Azure portal, go to **Create a resource** > **Internet of Things** > **Stream Analytics Job**.

1. Provide the following values to create your job:

   | Field | Value |
   | ----- | ----- |
   | Job name | Provide a name for your job. For example, **IoTEdgeJob** |
   | Subscription | Choose the same subscription as your IoT hub. |
   | Resource group | We recommend that you use the same resource group for all test resources you create during the Vision AI DevKit quick starts and tutorials.|
   | Location | Choose a location close to you. |
   | Hosting environment | Select **Edge**. |

1. Select **Create**.

### Configure your job

Once your Stream Analytics job is created in the Azure portal, you can configure it with an input, an output, and a query to run on the data that passes through.

Using the three elements of input, output, and query, this section creates a job that receives temperature data from the IoT Edge device. It analyzes that data in a rolling 30-second window. If the average temperature in that window goes over 70 degrees, then an alert is sent to the IoT Edge device. You'll specify exactly where the data comes from and goes in the next section when you deploy the job.  

1. Navigate to your Stream Analytics job in the Azure portal.

1. Under **Job Topology**, select **Inputs** then **Add stream input**.

   ![Azure Stream Analytics add input]({{ '/assets/images/asa_input.png' |relative_url }})

1. Choose **Edge Hub** from the drop-down list.

1. In the **New input** pane, enter **temperature** as the input alias.

1. Keep the default values for the other fields, and select **Save**.

1. Under **Job Topology**, open **Outputs** then select **Add**.

   ![Azure Stream Analytics add output]({{ '/assets/images/asa_output.png' | relative_url }})

1. Choose **Edge Hub** from the drop-down list.

1. In the **New output** pane, enter **alert** as the output alias.

1. Keep the default values for the other fields, and select **Save**.

1. Under **Job Topology**, select **Query**.

1. Replace the default text with the following query. The SQL code sends a reset command to the alert output if the average machine temperature in a 30-second window reaches 70 degrees. The reset command has been pre-programmed into the sensor as an action that can be taken.

    ```sql
    SELECT  
        'reset' AS command
    INTO
       alert
    FROM
       temperature TIMESTAMP BY timeCreated
    GROUP BY TumblingWindow(second,30)
    HAVING Avg(machine.temperature) > 70
    ```

1. Select **Save**.

### Configure IoT Edge settings

To prepare your Stream Analytics job to be deployed on an IoT Edge device, you need to associate the job with a container in a storage account. When you go to deploy your job, the job definition is exported to the storage container.

1. Under **Configure**, select **Storage account settings**.

1. Select **Add storage account**.

1. Select your **Storage account** from the drop-down menu.

1. For the **Container** field, select **Create new** and provide a name for the storage container.

1. Select **Save**.

## Deploy the job

You are now ready to deploy the Azure Stream Analytics job on your IoT Edge device.

In this section, you use the **Set Modules** wizard in the Azure portal to create a *deployment manifest*. A deployment manifest is a JSON file that describes all the modules that will be deployed to a device, the container registries that store the module images, how the modules should be managed, and how the modules can communicate with each other. Your IoT Edge device retrieves its deployment manifest from IoT Hub, then uses the information in it to deploy and configure all of its assigned modules.

For this tutorial, you deploy two modules. The first is **tempSensor**, which is a module that simulates a temperature and humidity sensor. The second is your Stream Analytics job. The sensor module provides the stream of data that your job query will analyze.

1. In the Azure portal, in your IoT hub, go to **IoT Edge**, and then open the details page for your IoT Edge device.

1. Select **Set modules**.  

1. If you previously deployed the tempSensor module on this device, it might autopopulate. If it does not, add the module with the following steps:

   1. Click **Add** and select **IoT Edge Module**.
   1. For the name, type **tempSensor**.
   1. For the image URI, enter **mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0**.
   1. Leave the other settings unchanged and select **Save**.

1. Add your Azure Stream Analytics Edge job with the following steps:

   1. Click **Add** and select **Azure Stream Analytics Module**.
   1. Select your subscription and the Azure Stream Analytics Edge job that you created.
   1. Select **Save**.

1. Once your Stream Analytics job is published to the storage container that you created, click on the module name to see how a Stream Analytics module is structured.

   The image URI points to a standard Azure Stream Analytics image. This is the same image used for every job that gets deployed to an IoT Edge device.

   The module twin is configured with a desired property called **ASAJobInfo**. The value of that property points to the job definition in your storage container. This property is how the Stream Analytics image is configured with your specific job information.

1. Close the module page.

1. Make a note of the name of your Stream Analytics module because you'll need it in the next step, then select **Next** to continue.

1. Replace the default value in **Routes** with the following code. Update all three instances of _{moduleName}_ with the name of your Azure Stream Analytics module.

    ```json
    {
        "routes": {
            "telemetryToCloud": "FROM /messages/modules/tempSensor/* INTO $upstream",
            "alertsToCloud": "FROM /messages/modules/{moduleName}/* INTO $upstream",
            "alertsToReset": "FROM /messages/modules/{moduleName}/* INTO BrokeredEndpoint(\"/modules/tempSensor/inputs/control\")",
            "telemetryToAsa": "FROM /messages/modules/tempSensor/* INTO BrokeredEndpoint(\"/modules/{moduleName}/inputs/temperature\")"
        }
    }
    ```

   The routes that you declare here define the flow of data through the IoT Edge device. The telemetry data from tempSensor are sent to IoT Hub and to the **temperature** input that was configured in the Stream Analytics job. The **alert** output messages are sent to IoT Hub and to the tempSensor module to trigger the reset command.

1. Select **Next**.

1. In the **Review Deployment** step, select **Submit**.

1. Return to the device details page, and then select **Refresh**.  

    You should see the new Stream Analytics module running, along with the IoT Edge agent module and the IoT Edge hub.

    ![tempSensor and ASA module reported by device]({{ '/assets/images/asa_module_output2.png' | relative_url }})

## View data

Now you can go to your IoT Edge device to check out the interaction between the Azure Stream Analytics module and the tempSensor module.

1. Check that all the modules are running in Docker:

   ```cmd/sh
   iotedge list  
   ```

   <!--
   ![Docker output](./media/tutorial-deploy-stream-analytics/docker_output.png)
   -->
1. View all system logs and metrics data. Use the Stream Analytics module name:

   ```cmd/sh
   iotedge logs -f {moduleName}  
   ```

You should be able to watch the machine's temperature gradually rise until it reaches 70 degrees for 30 seconds. Then the Stream Analytics module triggers a reset, and the machine temperature drops back to 21.

   ![Reset command output into module logs]({{ '/assets/images/asa_docker_log.png' | relative_url }})

## Clean up resources

You can keep the resources and configurations that you created and reuse them. You can also keep using the same IoT Edge device as a test device.

Otherwise, you can delete the local configurations and the Azure resources that you created in this article to avoid charges.

### Delete Azure resources

Deleting Azure resources and resource groups is irreversible. Make sure that you don't accidentally delete the wrong resource group or resources. If you created the IoT hub inside an existing resource group that has resources that you want to keep, delete only the IoT hub resource itself, instead of deleting the resource group.

To delete the resources:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Resource groups**.

2. Select the name of the resource group that contains your IoT Edge test resources.

3. Review the list of resources contained in your resource group. If you want to delete all of them, you can select **Delete resource group**. If you want to delete only some of them, you can click into each resource to delete them individually.

### Delete local resources

If you want to remove the IoT Edge runtime and related resources from your device, use the appropriate commands for your device operating system.

#### Windows

Uninstall the IoT Edge runtime.

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Uninstall-SecurityDaemon
   ```

When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device. View all containers.

   ```powershell
   docker ps -a
   ```

Delete the runtime containers that were created on your device.

   ```powershell
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```

Delete any additional containers that were listed in the `docker ps` output by referring to the container names.

#### Linux

Remove the IoT Edge runtime.

   ```bash
   sudo apt-get remove --purge iotedge
   ```

When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device. View all containers.

   ```bash
   sudo docker ps -a
   ```

Delete the runtime containers that were created on your device.

   ```bash
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```

Delete any additional containers that were listed in the `docker ps` output by referring to the container names.

Remove the container runtime.

   ```bash
   sudo apt-get remove --purge moby
   ```

## Next steps

In this tutorial, you configured an Azure Streaming Analytics job to analyze data from your IoT Edge device. You then loaded this Azure Stream Analytics module on your IoT Edge device to process and react to temperature increase locally, as well as sending the aggregated data stream to the cloud.
