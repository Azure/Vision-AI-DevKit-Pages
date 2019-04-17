---
title: "Troubleshooting Display Issues"
permalink: /docs/Display_issues/
excerpt: "Resolving display issues"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
## Display issues

* Your display must have a minimum resoltion of 1080p.
* Televisions or gaming specific monitors may not be recognized by the Vision AI DevKit.
* Use a direct HDMI connection to the display. Converters, e.g. Display Port to HDMI, will usually cause the output to fail.
* The neural processing engine (or other parts of the stack) may require a reboot occasionally. The command line

  ```
  adb reboot
  ```

  will help to reset all sub-systems.

* The object label presented in the bounding box may appear incorrect. If a new object appears in the space befor the bounding box is drawn, the label of the last object detected will be presented. This is not an inferencing bug.

  ```
  logcat | grep SNPE
  ```

  will show you the inferenced objects.