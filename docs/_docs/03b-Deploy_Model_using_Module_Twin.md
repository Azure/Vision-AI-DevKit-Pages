---
title: "Send a new Custom Vision model to a deployed Custom Vision configured module"
permalink: /docs/Deploy_Model_using_Module_Twin/
excerpt: "How to deploy a new Custom Vision model to a device with an existing Custom Vision configure module using the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-05-02
---

## What you will do

* Modify module twin settings for an existing Custom Module deployed to the DevKit

## What you will need

* Vision AI DevKit with a pre-existing module containing a Custom Vision created module
  * This can be the AIVisionDevKitGetStartedModule from the tutorial or another module developed with the Azure Custom Vision service
* New vision AI module exported from the [Azure Custom Vision](https://customvision.ai){:target="_blank"} service
* Azure Storage acccount

## Deploy your custom model to your device

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the Get Started module to use this model instead of the default one. We will use a cloud blob store to store the model but a public OneDrive link would work just as well.

### Uploading new custom model files

* Login to the [Azure portal](http://portal.azure.com){:target="_blank"} go to *Storage accounts*, then select (or create) the storage resource for your module.
* From the `overview` tab, click on `Blobs` service.
* Add a new container, setting the `Public access level` to  `Container (anonymous read access for containers and blobs)`.

* Click on the container you created, then click `Upload`.
* Select the three files exported from the Custom Vision service and click 'Upload'.
* Copy the three URLs for each of these files.

### Updating the configuration of the Get Started module to use your new custom model

* Click *Dashboard* on the Azure portal side menu, then click on your  ioT Hub resource.
* Click on `IoT Edge`, under *Automatic Device Management* and then on your camera device name.
* Click on the IoT Edge Custom Module (such as `AIVisionDevkitGetStartedModule`) and click on `Module Identity Twin`.
* Update the three properties (ModelUrl, LabelUrl, and ConfigUrl) with the URL you copied during the file upload earlier, then click `Save`.

```terminal
{
    "properties.desired":{
        "ModelUrl":"https://../MyModelFile.dlc",
        "LabelURL":"https://../MyLabels.txt",
        "ConfigUrl":"https://:../MyConfig.json",
    }
}
```

After a few minutes, your device should now be running your new custom model.

### Test your new model

* Verify that the camera output from your DevKit's connected monitor or using a video player supporting RTSP [(View RTSP Stream)]({{ '/docs/RTSP_stream/' | relative_url }}).