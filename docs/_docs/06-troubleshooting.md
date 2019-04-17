---
title: "Troubleshooting and Tips"
permalink: /docs/troubleshooting/
excerpt: "Tips and troubleshooting suggestions for the Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---

## Rebooting the Vision AI DevKit hardware

  * Click the reset button once, using the pin hole on the right side of the camera.
  * Press the power button on the back once.
  * Use the command line

      ```
      adb reboot
      ```

  * Long press the power button more than 12 seconds, to force a power down of the hardware. Then hold the power button for more than 12 seconds again to power up the hardware.

## Check Docker Container status

Use the command line

```
adb shell docker ps
```

or

```
adb shell watch docker ps
```

* If edgeAgent is still being downloaded, you will see the docker container is empty. To check if it’s in progress, you can use the command line

    ```
    adb shell watch ifconfig wlan0
    ```

  to see if the RX bytes are increasing.
* If edgeAgent is downloaded, you will see it running. Once you see edgeAgent is downloaded, you can use the command line

  ```
  adb shell docker logs -f edgeAgent
  ```

  to see the progress. Once completed, the device is ready to deploy a module from IoT Hub.

## Review logs and progress of the IoT Edge Agent

```
adb shell docker logs -f edgeAgent
```

* After you see a “Start module <your module name>” message, you can use 

  ```
  adb shell docker logs -f <your module name>
  ```

  to review logs for your module(s).

## Get the assigned IP address for the camera hardware

    adb shell ifconfig wlan0

## Improve inferencing accuracy by using the CPU in place of the DSP

Do to quantization, the DSP may provide low quality inferencing. To run inferencing on the CPU, change the **va-snpe-engine-library_config.json** fields ***NetworkIO*** and ***Runtime*** to the value of 0.
