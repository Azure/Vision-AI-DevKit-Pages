---
title: "Logs"
permalink: /docs/Review_logs/
excerpt: "Reivew logs and progress of the IoT Edge Agent"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-03
---
## What you will need

* ADB command line utility ([Instructions]({{ '/docs/platform_tools/#adb' | relative_url }}){:target="_blank"})

## Review logs and progress of the IoT Edge Agent

  ```cmd
  adb shell docker logs -f edgeAgent
  ```

* After you see a “Start module (your module name)” message, you can use

  ```cmd
  adb shell docker logs -f <your module name>
  ```

to review logs for your module(s).
