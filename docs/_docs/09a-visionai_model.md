---
title: "Vision AI Model"
permalink: /docs/model/
excerpt: "Vision AI Model"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-07-26
---

## Vision AI Model layout

Vision AI models which run on the Vision AI DevKit consists of three files:

* .DLC file - containing the model
* .TXT file - containing a list of the objects recognized by the model
* .json file - containing the VAM engine configuration

the model is stored in camera in /data/misc/camera folder

In addition .dlc file the camera can run an AI model in .tflite (Tensorflow lite) format.

## Contents of the .json VAM engine configuration file

You can check the VAM configuration file for the default model using platform tools (ADB):
```terminal
adb shell cat /data/misc/camera/va-snpe-engine-library-config.json
```

Here is a breakdown of key attributes and their values in VAM config:

*"EngineOutput":0,*  --> Engine output: Possible values:
'0' --> Single;
'1' --> Multi;

*"InputFormat":3,*  --> SNPE input format: Possible values:
'0' --> RGB
'1' --> BGR
'2' --> RGB Float
'3' --> BGR Float

    Note: SNPE common engine currently supports only BGR Float

*"NetworkIO":0"* --> Network IO: Possible values:
'0' --> UserBufer
'1' --> ITensor

*"ScaleWidth":,*  --> ScaleWidth
*"ScaleHeight":,* --> ScaleHeight
*"BlueMean":,*   --> BlueMean
*"GreenMean":,*   --> GreenMean
*"RedMean":,*   --> RedMean
Mean Range [0 - 255]

*"UseNorm":1,*   --> Normalization
'0' --> Do not use normalization
'1' --> Use normalization

*"TargetFPS":30,*   --> Target Frames Per Second

*"ConfThreshold":0.0,*   --> ConfThreshold, percentage of confidence needed for labeling an object
Range [0.0 - 1.0]

*"DLC_NAME":".dlc",* --> dlc file name
*"LABELS_NAME":".txt",* --> labels file name
*"InputLayers"* --> Input layers
*"OutputLayers"* --> Output layers - array of strings.
It is possible to have single entry

*"ResultLayers"* --> Used for comparing the results.
It is possible to have single entry.
For ComplexEngine, use the following convention:
'[ ]'

*"Runtime":0,*  --> Runtime: Possible values:
'0' --> CPU;
'1' --> DSP;
