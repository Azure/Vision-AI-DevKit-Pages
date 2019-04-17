---
title: "Guide to Device LEDs"
permalink: /docs/Guide_to_device_LEDs/
excerpt: "Interpreting the LEDs on the Vision AI DevKit"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-17
---
## Guide to device LEDs

![Image of DevKit camera with LEDs highlighted]({{ '/assets/images/LED_Guide.PNG' | relative_url }})

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-syad{background-color:#000000;color:#ffffff;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-llyw{background-color:#c0c0c0;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-red{background-color:#FF0000;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-green{background-color:#00FF00;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-amber{background-color:#FFFF00;border-color:inherit;text-align:left;vertical-align:top}
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
    <td class="tg-red"><br>Blink Red<br></td>
    <td class="tg-red"><br>Blink Red<br></td>
    <td class="tg-red"><br>Blink Red<br></td>
    <td class="tg-0pky"><br>Device is ready for setup.<br></td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  Connected to WiFi<br>  </td>
    <td class="tg-green"><br>Blink Green<br></td>
    <td class="tg-green"><br>Blink Green<br></td>
    <td class="tg-green"><br>Blink Green<br></td>
    <td class="tg-0pky"><br>WiFi connected to internet access/not connected to IoT Hub<br></td>
  </tr>
  <tr>
    <td class="tg-llyw"><br>  Powering ON/OFF<br>  </td>
    <td class="tg-red"><br>Red<br></td>
    <td class="tg-red"><br>Red<br></td>
    <td class="tg-red"><br>Red<br></td>
    <td class="tg-0pky"><br>Device is powering on/off and/or performing system restore<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  IoT Hub Connected<br>  </td>
    <td class="tg-green"><br>Green<br></td>
    <td class="tg-green"><br>Green<br></td>
    <td class="tg-green"><br>Green<br></td>
    <td class="tg-0lax"><br>Connected to IoT Hub, downloading manifest/modules, executing modules<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Offline<br>  </td>
    <td class="tg-amber"><br>Amber<br></td>
    <td class="tg-amber"><br>Amber<br></td>
    <td class="tg-amber"><br>Amber<br></td>
    <td class="tg-0lax"><br>Device is setup but not connected to WiFi. Modules running in Offline mode.<br></td>
  </tr>
  <tr>
    <td class="tg-y6fn"><br>  Reboot<br>  </td>
    <td class="tg-red"><br>Red<br></td>
    <td class="tg-0lax"><br> <br></td>
    <td class="tg-0lax"><br> <br></td>
    <td class="tg-0lax"><br>Device is rebooting<br></td>
  </tr>
</table>
