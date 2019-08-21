---
title: "Vision AI"
permalink: /docs/visionai/
excerpt: "Vision AI"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-08
---

## Vision AI and machine learning

Vision AI is specialized machine learning for images and video that allows you to transform camera input into labels and objects that you can use in your applications and busineses logic. The Vision AI DevKit brings together the hardware and services to enable you to get started with vision and machine learning. If you're already an experienced data scientist, the kit also integrates with familiar tools and services. 

The camera itself is specifically designed with inferencing performance in mind, and enables your image classification model to run hardware-accelerated on the Qualcomm Neural Processing Engine. This frees up the CPU on the device to allow you to run other IoT Edge modules, like the IoT Hub to manage your solution, analytics, or your own business logic for your solution.  The DevKit supports a number of neural network formats and frameworks so that you can create custom models that work for your solution.  For the current list of supported options, see [supported framework]({{ '/docs/frameworks' | relative_url }}).

You can develop your custom machine learning model using any of the integrated Azure services that we support and deploy it to the camera using Azure IoT Hub. A sample object detection model is deployed to the device with Azure IoT Hub when you first setup the device to allow you to start learning right out of the box.

### Use an existing model

See more information regarding [Vision AI model]({{ '/docs/model' | relative_url }}) that runs on a camera. Vision AI Dev Kit [GitHub](https://github.com/Microsoft/vision-ai-developer-kit){:target="_blank"} contains samples and scripts for converting an existing model to a supported file format.

### Custom Vision - Get started with machine learning

Custom Vision lets you create an image classification model with your own images with an easy to use web interface. See the Custom Vision [tutorial](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Tutorial-HOL_Using_the_VisionSample/) that walks through creating and deploying your own model to the camera. For more information, the [Custom Vision](https://www.customvision.ai/) portal provides an easy start for your machine learning journey. It can also export the AI model in a format that runs directly in Vision AI Dev Kit. 

Read more about Custom Vision from [Microsoft docs pages](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/home).

### Azure Machine Learning

For data scientists and Python developers, the Vision AI DevKit integrates with Azure ML and allows you to create your own models and leverage a familiar development environment. [Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml) offers comprehensive tools for building AI models. Vision AI Dev Kit [GitHub](https://github.com/Microsoft/vision-ai-developer-kit){:target="_blank"} contains samples and scripts for using Azure Machine learning by using Jupyter Notebooks or VS Code as a user interface.

