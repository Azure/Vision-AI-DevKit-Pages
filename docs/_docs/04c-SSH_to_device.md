---
title: "SSH"
permalink: /docs/SSH/
excerpt: "How to SSH to the device"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-05-31
---
## What you will need

* Linux terminal
* SSH login need to be enabled during OOBE (Out-Of-Box experience)

## For Windows

For Windows you'll need Linux app for ssh.
1. Install Linux for Windows https://docs.microsoft.com/en-us/windows/wsl/install-win10


2. Check the IP address of your device with ```adb shell ifconfig wlan0```
3. To login to the device run following command in your Linux client ```ssh [ssh_username]@[ipaddress]```
4. Type in the password that was configured for SSH during OOBE

## Note

SSH uses WiFi. In order for the SSH to work the device and laptop used in a connection need to be in the same WiFi network.
