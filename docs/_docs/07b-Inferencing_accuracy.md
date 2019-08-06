---
title: "Improve Inferencing Accuracy"
permalink: /docs/Inferencing_accuracy/
excerpt: "Using the CPU to improve inferencing accuracy"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-03
---
## Improve inferencing accuracy by using the CPU in place of the DSP

Due to quantization, the DSP may provide low quality inferencing. To run inferencing on the CPU, change the **va-snpe-engine-library_config.json** fields ***NetworkIO*** and ***Runtime*** to the value of 0.
