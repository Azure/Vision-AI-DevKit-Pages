---
title: "Docker Status"
permalink: /docs/Docker_status/
excerpt: "Using the ADB shell to review Docker Container status"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
## What you will need

Some troubleshooting steps require the use of an ADB command line. For more information (and to install the ADB utility, please visit the [Platform Tools]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"} section.)

## Check Docker Container status

Use the command line

```cmd
adb shell docker ps
```

or

```cmd
adb shell watch docker ps
```

* If edgeAgent is still being downloaded, you will see the docker container is empty. To check if it’s in progress, you can use the command line

    ```cmd
    adb shell watch ifconfig wlan0
    ```

  to see if the RX bytes are increasing.
* If edgeAgent is downloaded, you will see it running. Once you see edgeAgent is downloaded, you can use the command line

  ```cmd
  adb shell docker logs -f edgeAgent
  ```

  to see the progress. Once completed, the device is ready to deploy a module from IoT Hub.
