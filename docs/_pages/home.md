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
    - label: "Order <i class='fas fa-chevron-right'></i>"
      url: "https://www.arrow.com/en/products/eic-ms-vision-500/einfochips-limited"
excerpt: >
  Jumpstart your Azure Vision Machine Learning Journey today
VAIDK_More:
  - title: "Start fast"
    excerpt: |
      Using the [tutorial project](https://aka.ms/VAIDKGetStarted-Landing/), the Vision AI DevKit can be up and running in minutes, regardless of your current skill level with Vision Machine Learning. Don't have a DevKit yet? Start building an [image classifier](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) with [Azure Custom Vision Service](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/home).
      # Build fast
      * Just getting started with Vision ML? [Azure Custom Vision Service](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier){:target="_blank"} can do the hard work to get your project up and running quickly with only a few labeled images to start off with.
      * Experienced with Vision ML? [Jupyter notebooks](https://jupyter.org/){:target="_blank"} or [Visual Studio Code](https://azure.github.io/Vision-AI-DevKit-Pages/docs/SetUp_VS_Code/) can be used to create, train and deploy your custom vision ML models.
      * Convert and deploy existing models from other formats to work with the Vision AI DevKit -
        * [MobileNet ImageNet](https://github.com/Microsoft/vision-ai-developer-kit/blob/master/machine-learning-reference/notebooks/01-convert-model-containerize.ipynb)
        * [Squeezenet Caffe](https://github.com/Microsoft/vision-ai-developer-kit/blob/master/machine-learning-reference/notebooks/03-squeezenet-custom-vision.ipynb)
        * Tensorflow

        Note: Some links require Vision AI DevKit GitHub repository access (currently in private preview.)

      # Deploy fast
      [Azure IoT Edge](https://docs.microsoft.com/en-us/azure/iot-edge/){:target="_blank"} can push your Vision ML models to the Vision AI DevKit with ease, whether the camera is on your desk or in another country, using [Visual Studio Code](https://azure.github.io/Vision-AI-DevKit-Pages/docs/Deploy_model_VS_Code/) or [Jupyter notebooks](https://github.com/Microsoft/vision-ai-developer-kit/blob/master/machine-learning-reference/notebooks/04-Deploy-Trained-Model.ipynb)         

  - title: "Prove your concept"
    excerpt: |
      With the Vision AI DevKit and Azure services, quickly take your project from concept to reality.

      # Intelligent Edge: Fast local processing, backed by the power of the cloud 
      As an [Intelligent Edge device](https://azure.microsoft.com/en-us/overview/future-of-cloud/){:target="_blank"}, the Vision AI DevKit runs your Vision ML models locally for fast image inference. You can add business logic to your concept, sending only the most important data to the cloud for more advanced processing and response.
     
more_info:
  - title: "<img src='assets/images/qualcomm-logo-blue.png' alt='Qualcomm' style='max-width: 200px'>"
    excerpt: >
        The Vision AI Dev Kit features the [Qualcomm Visual Intelligence Platform](https://www.qualcomm.com/news/onq/2018/05/07/qualcomm-vision-intelligence-platform-microsoft-azure-bring-edge-ai-solution){:target="_blank"} for hardware acceleration of AI models to deliver superior inferencing performance. Create new solutions for a variety of scenarios, such as industrial safety, retail, security, and more.
  - title: ""
    excerpt: |
     # Additional Resources
      * [DevKit announcement](https://azure.microsoft.com/en-us/blog/iot-swc-2018-iot-solutions-for-the-built-world/){:target="_blank"}
      * [Join the Internet of Things Microsoft Tech Community](https://aka.ms/VAIDK-IoTTechCommunity){:target="_blank"}

advantages:
  - excerpt: |
        <video id="azuremediaplayer" class="azuremediaplayer amp-default-skin amp-big-play-centered" tabindex="0"></video>
        <script>
            var myOptions = {
                "nativeControlsForTouch": false,
                controls: true,
                autoplay: false,
                width: "100%",
                height: "auto",
            }
            myPlayer = amp("azuremediaplayer", myOptions);
            myPlayer.src([
                {
                    "src": "https://easstandardhosting123.blob.core.windows.net/asset-0a1504fe-8b97-4e8f-a312-2a5eef36c891/Vision_AI_101418.mp4?sv=2015-07-08&sr=c&si=1da79a8d-775c-4a56-af1a-173c36a1823b&sig=W7ACJX%2F0FrlqxYg7TlPfjojO3Ajf%2FiHy7eW4%2FfgK%2BAk%3D&st=2018-10-25T01%3A49%3A06Z&se=2118-10-25T01%3A49%3A06Z",
                    "type": "video/mp4"

                }
            ]);</script>
  - title: "Create Intelligent Apps for IoT Sensors"
    excerpt: >
        In the era of intelligent cloud and intelligent edge, developers will need to write applications for a range of connected devices. The Azure IoT Edge runtime makes it easy to create applications from cloud to edge, leveraging advanced AI services. The Vision AI Developer Kit, a member of the Microsoft Azure IoT Starter kit family, can be used by IoT solution makers to easily deploy AI models built using Azure Machine Learning and Azure IoT Edge.

Quonos:
  - image_path: /assets/images/icon-innovation.svg
    alt: "placeholder 2"
    excerpt: >
        This is a a test of the emergency broadcast system
  - image_path: /assets/images/icon-cog.svg
    alt: "placeholder 2"
    excerpt: >
        This is a a test of the emergency broadcast system
  - image_path: /assets/images/icon-mount.svg
    alt: "placeholder 2"
    excerpt: >
        This is a a test of the emergency broadcast system
  - image_path: /assets/images/icon-sdk.svg
    alt: "placeholder 2"
    excerpt: >
        This is a a test of the emergency broadcast system
---

<div class="feature__outer_wrapper">
{% include feature_row id="VAIDK_More" type="dual" %}
</div>

<div class="feature__outer_wrapper">
{% include feature_row id="more_info" type="dual" %}
</div>
