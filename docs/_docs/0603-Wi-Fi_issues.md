---
title: "Troubleshooting Wi-Fi Issues"
permalink: /docs/Wi-Fi_issues/
excerpt: "Resolving Wi-Fi issues"
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
