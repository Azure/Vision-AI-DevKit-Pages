---
title: "Troubleshooting"
permalink: /docs/04-troubleshooting/
excerpt: "How to troubleshoot issues related to Vision AI Dev Kit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-02-11
---
## Display issues
* Use a direct HDMI connection to the display. Using converters, e.g. Display Port to HDMI, will usually not work.
* The neural processing engine (or other parts of the stack) require a reboot occasionally. `adb reboot` will help to reset all sub-systems.
* The labels presented on the HDMI output may be incorrect. The display process picks the label of the last object that was detected and presents it to the UI. This is not an inferencing bug. `logcat | grep SNPE` will show you the inferenced objects.

## Camera hardware Wi-Fi access point passphrase
* The Vision AI Dev Kit camera hardware should have a unique Wi-Fi access point passphrase found on a sticker on the bottom of the device. If there is no sticker, use `ADB tools: Run adb shell cat /data/misc/wifi/hostapd_virtual.conf` to display the access point configuration details. The output will be similar to this:

    
      >   ctrl_interface=/var/run/hostapd<br/>
      >   interface=softap0<br/>
      >   #driver=nl80211<br/>
      >   #ieee80211d=1<br/>
      >   ieee80211n=1<br/>
      >   hw_mode=g<br/>
      >   country_code=US<br/>
      >   ssid=MSIoT_E72FA8<br/>
      >   macaddr_acl=0<br/>
      >   channel=0<br/>
      >   wpa=2<br/>
      >   **wpa_passphrase=NhEtVE3D** <br/>
      >   wpa_key_mgmt=WPA-PSK<br/>
      >   #wpa_pairwise=CCMP<br/>
      >   rsn_pairwise=TKIP CCMP<br/>
      >   ht_capab=HT20 SHORT-GI-20<br/>
      >   wmm_enabled=1<br/>
      >   ignore_broadcast_ssid=0<br/>

     The bold line contains the passphrase, which is unique to each device.

## Display the MAC address
Using adb<br/>
    `adb shell ifconfig wlan0`

Look for **HWaddr** in the output. The MAC address will be in a format similar to this:  00:0A:G5:5B:20:9E

## Recover 'bricked' devices after a failed firmware update
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

## Additional Commands
### Check Docker Container status
Within the adb shell, use `docker ps` or `watch docker ps`

* If edgeAgent is still being downloaded, you will see it empty. To check if it’s in progress, you can use watch ifconfig wlan0 and see if the RX bytes are increasing. 
* If edgeAgent is downloaded, you will see it running here. Once you see edgeAgent is downloaded, you can type docker logs -f edgeAgent to see its progress. Now the device is ready to deploy a module from IoT Hub.

### Review logs and progress of the IoT Edge Agent
Use `docker logs -f edgeAgent`

* After you see “Start module <your module name>” message then you can use `docker logs -f <your module name>` to review logs for your module(s).

### Get the assigned IP address for the camera hardware

    adb shell ifconfig wlan0

### Improve inferencing accuracy by using the CPU in place of the DSP
Do to quantization, the DSP may provide low quality inferencing. To run inferencing on the CPU, change the `va-snpe-engine-library_config.json` fields `NetworkIO` and `Runtime` to a value of 0.

### Guide to device LEDs
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
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Red<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Red<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Red<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Device in OOBE state. Ready for WiFi Setup.<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  Connected to WiFi<br>  </td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;WiFi connected to internet access/not connected<br>&nbsp;&nbsp;to IoT Hub<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  SoftAP Mode<br>  </td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Blink Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;WiFi in AP mode. Reconfigure WiFi connection.<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  IoT Hub Connected<br>  </td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Green<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Connected to IoT Hub, downloading<br>&nbsp;&nbsp;manifest/modules, executing modules<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Disconnected<br>  </td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Amber<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Device is setup but not connected to WiFi.<br>&nbsp;&nbsp;Modules running in Disconnected mode.<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Reboot<br>  </td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Red<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp; <br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp; <br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Device is rebooting<br>&nbsp;&nbsp;</td>
  </tr>
</table>
