---
layout: splash
permalink: /
title: A Smart Camera for the Intelligent Edge
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/node-graphic.png
  image: /assets/images/camera-render-transparent-small.png
  alt: "Picture of the Vision AI DevKit camera hardware"
  actions:
#    - label: "Order <i class='fas fa-chevron-right'></i>"
#      url: "https://www.arrow.com/en/products/eic-ms-vision-500/einfochips-limited"
    - label: "Coming Soon"
excerpt: >
  Jumpstart your Azure vision machine learning journey
VAIDK_More:
  - title: "Start fast"
    excerpt: |
      [Get up and running in minutes](https://aka.ms/VAIDKGetStarted-Landing/), regardless of your current skill level with vision machine learning. Connect your camera to Azure IoT Hub that controls the network traffic between the device and the cloud, and see the camera in action by running a default Vision AI module that recognizes 183 different objects.
      # Build fast
      * New to Vision ML? Start building a vision model by uploading and tagging pictures, letting [Azure Custom Vision Service](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Tutorial-HOL_Using_the_VisionSample/){:target="_blank"} do the heavy lifting.
      * Experienced with vision ML? Use [Jupyter notebooks](https://azure.github.io/Vision-AI-DevKit-Pages/docs/jupyter/){:target="_blank"} and [Visual Studio Code](https://azure.github.io/Vision-AI-DevKit-Pages/docs/SetUp_VS_Code/) to create and train custom vision models using Azure Machine Learning (AML). AML services enable you to prepare data and train models. You can then convert the trained model to the custom DLC format and package it into an IoT Edge module to deploy to the Vision AI Dev Kit.
            
  - title: "Deploy fast"
    excerpt: |
      [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/) can push your containerized vision ML models and other modules to the Vision AI DevKit with ease, whether the camera is on your desk or in another country.   

      # Join the Community
      Get help and help others with vision ML projects by joining our [Tech Community](https://aka.ms/VAIDK-IoTTechCommunity){:target="_blank"} and [Gitter](https://aka.ms/VAIDKGitter-Landing/){:target="_blank"}.
      # Build the intelligent edge
      As an [Intelligent Edge device](https://azure.microsoft.com/en-us/overview/future-of-cloud/){:target="_blank"}, the Vision AI DevKit does inferences and runs containerized Azure services locally in the device. Moving these workloads to the edge of the network means vision ML inferencing work requires less cloud interaction while also enabling quick reaction to local events, allowing operation during extended offline periods.
     
advantages:
  - video_path: https://easstandardhosting123.blob.core.windows.net/asset-0a1504fe-8b97-4e8f-a312-2a5eef36c891/Vision_AI_101418.mp4?sv=2015-07-08&sr=c&si=1da79a8d-775c-4a56-af1a-173c36a1823b&sig=W7ACJX%2F0FrlqxYg7TlPfjojO3Ajf%2FiHy7eW4%2FfgK%2BAk%3D&st=2018-10-25T01%3A49%3A06Z&se=2118-10-25T01%3A49%3A06Z
    video_poster: /assets/images/Video_poster.png

  - title: "<img src='assets/images/msft-logo-gray.svg' alt='Microsoft' style='max-width: 160px'>"
    excerpt: >
        An Azure IoT starter kit, the Vision AI DevKit can be used with models built and trained using the [Azure Machine Learning service](https://azure.microsoft.com/en-us/services/machine-learning-service/){:target="_blank"} and [CustomVision.ai](https://customvision.ai){:target="_blank"}. <br><br><br>

        <img src='assets/images/qualcomm-logo-blue.png' alt='Qualcomm' style='max-width: 125px'><br><br>

        The Vision AI DevKit features the [Qualcomm Visual Intelligence Platform](https://www.qualcomm.com/news/onq/2018/05/07/qualcomm-vision-intelligence-platform-microsoft-azure-bring-edge-ai-solution){:target="_blank"} for hardware acceleration of AI models to deliver superior inferencing performance.<br><br><br>

tech_specs:
  - title: "<img src='assets/images/Peabody_spec_image.png' alt='Vision AI DevKit device image'>"

  - title: "<img src='assets/images/Peabody_spec_image2.png' alt='Vision AI DevKit specs'>"

---

<div class="feature__outer_wrapper">
{% include feature_row id="VAIDK_More" type="dual" %}
</div>

<div class="feature__outer_wrapper">
{% include feature_row id="advantages" type="dual" %}
</div>

<h2 style="text-align: center">Technical Specifications</h2>

<div class="feature__outer_wrapper">
{% include feature_row id="tech_specs" type="dual" %}
</div>
