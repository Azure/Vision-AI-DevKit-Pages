---
title: "Supported frameworks and runtimes"
permalink: /docs/frameworks/
excerpt: "Supported frameworks and runtimes"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-07-30
---

## Supported Neural Network frameworks and formats

Here is a list of neural networks and runtimes that run on the devices DSP that provides adequate performance for real time inferencing.

<table style="width:100%">
  <tr>
    <th>Network Topology</th>
    <th>Verified Formats</th>
    <th>Support for DSP</th>
  </tr>
  <tr>
    <td>AlexNet</td>
    <td>Caffe2</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>DeepLabV3+</td>
    <td>Tensorflow</td>
    <td>Partial</td>
  </tr>
    <tr>
    <td>GoogleNet</td>
    <td>Caffe2</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>Inception-V3</td>
    <td>Tensorflow, Caffe</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Inception-V3 2016</td>
    <td>Tensorflow</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Inception-ResNet v2</td>
    <td>Tensorflow</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Inception-V4</td>
    <td>Caffe</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>MobileNet</td>
    <td>TensorFlow</td>
    <td>*</td>
  </tr>
  <tr>
    <td>MobileNet-v2</td>
    <td>TensorFlow, Caffe</td>
    <td>*</td>
  </tr>
  <tr>
    <td>MobileNet-SSD</td>
    <td>TensorFlow, Caffe</td>
    <td>*</td>
  </tr>
  <tr>
    <td>ResNet-50</td>
    <td>TensorFlow</td>
    <td>Y</td>
  </tr>
   <tr>
    <td>ResNet-101</td>
    <td>Caffe</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>ShuffleNet</td>
    <td>TensorFlow</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>SqueezeNet</td>
    <td>TensorFlow</td>
    <td>Y</td>
  </tr>
    <tr>
    <td>VGG-16</td>
    <td>TensorFlow</td>
    <td>Y</td>
  </tr>  <tr>
    <td>VGG-19</td>
    <td>Caffe</td>
    <td>Y</td>
  </tr>
</table>

  *this network topology requires changes to preserve accuracy when quantized. Instructions for topology modification are available from Qualcomm.

### ONNX support

ONNX support is currently experimental and most models will run on the CPU, rather than be offloaded to the DSP.

ONNX models from the following networks can be converted for use with the Vision AI DevKit:

* bvlc_alexnet
* bvlc_googlenet
* bvlc_reference_caffenet
* bvlc_reference_rcnn_ilsvrc13
* densenet121
* inception_v1
* inception_v2
* resnet_50
* vgg16
* vgg19
