---
title: "Troubleshooting and Tips"
permalink: /docs/troubleshooting/
excerpt: "Tips and troubleshooting suggestions for the Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-15
---
## Guide to device LEDs
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-syad{background-color:#000000;color:#ffffff;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-llyw{background-color:#c0c0c0;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-y6fn{background-color:#c0c0c0;text-align:left;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-syad"><br>  Device state<br>  </th>
    <th class="tg-syad"><br>  LED1<br>  </th>
    <th class="tg-syad"><br>  LED2<br>  </th>
    <th class="tg-syad"><br>  LED3<br>  </th>
    <th class="tg-syad"><br>  Description<br>  </th>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  Setup<br>  </td>
    <td class="tg-0pky"><br>Blink Red<br></td>
    <td class="tg-0pky"><br>Blink Red<br></td>
    <td class="tg-0pky"><br>Blink Red<br></td>
    <td class="tg-0pky"><br>Device in OOBE state. Ready for WiFi Setup.<br></td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  Connected to WiFi<br>  </td>
    <td class="tg-0pky"><br>Blink Green<br></td>
    <td class="tg-0pky"><br>Blink Green<br></td>
    <td class="tg-0pky"><br>Blink Green<br></td>
    <td class="tg-0pky"><br>WiFi connected to internet access/not connected to IoT Hub<br></td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  SoftAP Mode<br>  </td>
    <td class="tg-0pky"><br>Blink Amber<br></td>
    <td class="tg-0pky"><br>Blink Amber<br></td>
    <td class="tg-0pky"><br>Blink Amber<br></td>
    <td class="tg-0pky"><br>WiFi in AP mode. Reconfigure WiFi connection.<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  IoT Hub Connected<br>  </td>
    <td class="tg-0lax"><br>Green<br></td>
    <td class="tg-0lax"><br>Green<br></td>
    <td class="tg-0lax"><br>Green<br></td>
    <td class="tg-0lax"><br>Connected to IoT Hub, downloading manifest/modules, executing modules<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Disconnected<br>  </td>
    <td class="tg-0lax"><br>Amber<br></td>
    <td class="tg-0lax"><br>Amber<br></td>
    <td class="tg-0lax"><br>Amber<br></td>
    <td class="tg-0lax"><br>Device is setup but not connected to WiFi. Modules running in Disconnected mode.<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Reboot<br>  </td>
    <td class="tg-0lax"><br>Red<br></td>
    <td class="tg-0lax"><br> <br></td>
    <td class="tg-0lax"><br> <br></td>
    <td class="tg-0lax"><br>Device is rebooting<br></td>
  </tr>
</table>

## Display issues

* Use a direct HDMI connection to the display. Using converters, e.g. Display Port to HDMI, will usually not work.
* The neural processing engine (or other parts of the stack) require a reboot occasionally. `adb reboot` will help to reset all sub-systems.
* The labels presented on the HDMI output may be incorrect. The display process picks the label of the last object that was detected and presents it to the UI. This is not an inferencing bug. `logcat | grep SNPE` will show you the inferenced objects.

## Camera hardware Wi-Fi access point passphrase

The Vision AI Dev Kit camera hardware should have a unique Wi-Fi access point passphrase found on a sticker on the bottom of the device. If there is no sticker, use `ADB tools: Run adb shell cat /data/misc/wifi/hostapd_virtual.conf` to display the access point configuration details. The output will be similar to this:

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

## Display the Vision AI DevKit hardware MAC address

Use the ADB command line:

```
    adb shell ifconfig wlan0
```

Look for **HWaddr** in the output. The MAC address will be in a format similar to this:  00:0A:G5:5B:20:9E

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

Within the adb shell, use
```
docker ps
```
or
```
watch docker ps
```

* If edgeAgent is still being downloaded, you will see the docker container is empty. To check if it’s in progress, you can use

```
watch ifconfig wlan0
```
to see if the RX bytes are increasing.
* If edgeAgent is downloaded, you will see it running. Once you see edgeAgent is downloaded, you can type

```
docker logs -f edgeAgent
```
to see the progress. Once completed, the device is ready to deploy a module from IoT Hub.

## Review logs and progress of the IoT Edge Agent
```
docker logs -f edgeAgent
```

* After you see a “Start module <your module name>” message, you can use 
```
docker logs -f <your module name>
```
to review logs for your module(s).

## Get the assigned IP address for the camera hardware

    adb shell ifconfig wlan0

## Improve inferencing accuracy by using the CPU in place of the DSP
Do to quantization, the DSP may provide low quality inferencing. To run inferencing on the CPU, change the `va-snpe-engine-library_config.json` fields `NetworkIO` and `Runtime` to a value of 0.

