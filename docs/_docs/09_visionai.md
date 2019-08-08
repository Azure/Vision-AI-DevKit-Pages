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

Vision AI Dev Kit and related Microsoft services enable you to take your first steps with machine learning and provide also solutions for experienced professionals. The camera has a DSP (Digital Signal Processor) specifically designed for fast inferencing. In normal use it will run the image classification model while other IoT Edge modules run on CPU. Vision AI Dev Kit supports multiple neural networks and run times. See the full list of [supported framework]({{ '/docs/frameworks' | relative_url }}).

There are multiple ways to develop a custom machine learning model and deploy it the device. Azure IoT Hub provides an ease of use UI for deploying a model to run in the camera in seconds.

### Use an existing model

See more information regarding [Vision AI model]({{ '/docs/model' | relative_url }}) that runs on a camera. Vision AI Dev Kit [GitHub](https://github.com/Microsoft/vision-ai-developer-kit){:target="_blank"} contains samples and scripts for converting an existing model to a supported file format.

### Custom Vision - Get started with machine learning

[Custom Vision](https://www.customvision.ai/) portal provides an easy start for your machine learning journey. It can also export the AI model in a format that runs directly in Vision AI Dev Kit. 

Read more about Custom Vision from [Microsoft docs pages](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/home).

### Azure Machine Learning

[Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml) offers comprehensive means for building AI models. Vision AI Dev Kit [GitHub](https://github.com/Microsoft/vision-ai-developer-kit){:target="_blank"} contains samples and scripts for using Azure Machine learning by using Jupyter Notebooks or VS Code as a user interface.

