---
title: "Logs"
permalink: /docs/Review_logs/
excerpt: "Reivew logs and progress of the IoT Edge Agent"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
### What you will need

Some troubleshooting steps require the use of an ADB command line. For more information (and to install the ADB utility, please visit the [Platform Tools]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"} section.)

# Review logs and progress of the IoT Edge Agent

  ```cmd
  adb shell docker logs -f edgeAgent
  ```

* After you see a “Start module (your module name)” message, you can use

  ```cmd
  adb shell docker logs -f <your module name>
  ```

  to review logs for your module(s).
