---
title: "Deploy a new Vision AI model to an already existing module"
permalink: /docs/Deploy_Model_using_Module_Twin/
excerpt: "How to deploy a new Custom Vision model to a device with an existing Custom Vision configure module using the Azure portal."
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-07-30
---

## What you will do

* Modify module twin settings for an existing Vision AI model deployed to the DevKit

## What you will need

* Vision AI DevKit with a pre-existing default AIVisionDevKitGetStartedModule module
* A new Vision AI model in a zip file including the model (.dlc file or equivalent, labels.txt and VAM config)

## Deploy your custom model to your device

To deploy your custom model, we will first store your model in a publicly accessible location and then update the configuration of the Get Started module to use this model instead of the default one. We will use a cloud blob store to store the model but a public OneDrive link would work just as well.

### Uploading new custom model files

* Login to the [Azure portal](http://portal.azure.com){:target="_blank"} go to *Storage accounts*, then select (or create) the storage resource for your module.
* From the `overview` tab, click on `Blobs` service.
* Add a new container, setting the `Public access level` to  `Container (anonymous read access for containers and blobs)`.

* Click on the container you created, then click `Upload`.
* Select the zip files exported from the Custom Vision service and click 'Upload'.
* Copy the URL for the uploaded zip file.

### Updating the configuration of the Get Started module to use your new custom model

* Click *Dashboard* on the Azure portal side menu, then click on your  ioT Hub resource.
* Click on `IoT Edge`, under *Automatic Device Management* and then on your camera device name.
* Click on the IoT Edge Custom Module (such as `AIVisionDevkitGetStartedModule`) and click on `Module Identity Twin`.
* Update the property `ModelZipUrl` with the URL to the zip file on your blob storage, then click `Save`.

```terminal
{
    "properties.desired":{
        "ModelZipUrl":"https://../MyModel.zip",
    }
}
```

After a few seconds, your device should now be running your new custom model.

### Test your new model

* Verify that the camera output from your DevKit's connected monitor or using a video player supporting RTSP [(View RTSP Stream)]({{ '/docs/RTSP_stream/' | relative_url }}).
* If the module twin update doesn't seem to work try making an artificial change to the module twin properties (like hitting a space and backspace) and save again.
* In case you are iterating multiple times improving the same model and not sure if the model has been updated one way to check it is to use platform tools (ADB) and check from the camera's file structure time stamps when the model has been applied the last time:

```terminal
adb shell ls -ls /data/misc/camera
```
