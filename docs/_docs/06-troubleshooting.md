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
## Camera hardware Wi-Fi access point passphrase

The Vision AI Dev Kit camera hardware should have a unique Wi-Fi access point passphrase found on a sticker on the bottom of the device. If there is no sticker, use the command line

```
adb shell cat /data/misc/wifi/hostapd_virtual.conf
```

to display the access point configuration details. The output will be similar to this

```

      >   ctrl_interface=/var/run/hostapd
      >   interface=softap0
      >   #driver=nl80211
      >   #ieee80211d=1
      >   ieee80211n=1
      >   hw_mode=g<br/>
      >   country_code=US
      >   ssid=MSIoT_E72FA8
      >   macaddr_acl=0
      >   channel=0
      >   wpa=2
      --- >   wpa_passphrase=NhEtVE3D  ---
      >   wpa_key_mgmt=WPA-PSK
      >   #wpa_pairwise=CCMP
      >   rsn_pairwise=TKIP CCMP
      >   ht_capab=HT20 SHORT-GI-20
      >   wmm_enabled=1
      >   ignore_broadcast_ssid=0
```

  The line marked with three dashes above contains the passphrase, which is unique to each device.

## Unable to connect the Vision AI DevKit hardware to a Wi-Fi network

The Wi-Fi passphrase for your local Wi-fi network cannot have spaces (even at the end of the passphrase string), or the camera will be unable to connect to the Wi-Fi network.

## Connect your Vision AI DevKit to a different Wi-Fi network

To change the Wi-Fi network your DevKit hardware connects to, long press the power button for more than 5 seconds to turn on the DevKit hardware access point. Connect your PC to the Wi-Fi access point using the instructions in [OOBE.]({{ '/docs/Run_OOBE/' | relative_url }}) Run through the OOBE process again, making the approriate Wi-Fi network changes.

## Display the Vision AI DevKit hardware MAC address

Use the ADB command line

```
adb shell ifconfig wlan0
```

and look for **HWaddr** in the output. The MAC address will be in a format similar to:  00:0A:G5:5B:20:9E

## Rebooting the Vision AI DevKit hardware

  * Click the reset button once, using the pin hole on the right side of the camera.
  * Press the power button on the back once.
  * Use the command line

      ```
      adb reboot
      ```

  * Long press the power button more than 12 seconds, to force a power down of the hardware. Then hold the power button for more than 12 seconds again to power up the hardware.

## Recover Vision AI Dev Kit hardware after a failed firmware update

Re-flash using Fastboot, a part of the platform tools, if the device will enter fastboot mode.

    > $ adb reboot bootloader
    > $ fastboot devices
    > $ fastboot flash abl abl.elf
    > $ fastboot flash boot qcs605-boot.img
    > $ fastboot flash system qcs605-sysfs.ext4
    > $ fastboot flash userdata qcs605-usrfs.ext4
    > $ fastboot flash persist qcs605-persist.ext4
    > $ fastboot flash cache qcs605-cache.ext4
    > $ fastboot flash systemrw qcs605-systemrw.ext4
    > $ fastboot reboot

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
