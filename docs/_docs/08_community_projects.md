---
title: "Community Project: Vision AI Dev provisioning with Azure IoT Central"
permalink: /docs/community_project
excerpt: "Vision AI Dev provisioning with Azure IoT Central"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-08-05
---
<html><table>
<tr><td><b> Summary </b></td></tr>
<tr><td width="50%">
This project introduce a Vision AI module with web client that allows the user to interact directly with the device to control it as well as experiment with Custom Vision AI models. It also demonstrates the successful implementation of a Vision AI DevKit device provisioning itself with Azure IoT Central services to enable the live reporting of telemetry, state, events, and settings with the ability to manually control the ML model.
<td width="50%"> <img src="images/community_iotcentral.PNG" alt="i"> </td></tr>
</table></html>
<html><table>
<tr><td>
<b> Implementation </b> </td></tr>
<tr><td>
This project is implemented as a NodeJS micro service and React Web client. While the IoT Central's support for IoT Edge is still in the works the project by passes IoT Hub and allows IoT Central to interact directly with the device.

This project is an excellent way to showcase the power of intelligent edge camera with telemetry and other functions built in.
</td></tr>
</table></html>
<html><table>
 <tr>
    <td> <b> Software and Services used</b> </td>
    <td> <b> Hardware </b> </td> 
    <td rowspan="24"></td> </tr>
 <tr>
    <td> <ul type="disc" >
            <li>Azure IoT Central</li>
            <li>Visual Studio Code</li>
            <li>NodeJS 10x (with NPM)</li>
            <li>Android Debug Bridge (ADB) tools</li>
         </ul> 
   </td> 
    <td> <ul type="disc">
            <li>Vision AI DevKit camera</li>
         </ul>
   </td>
</tr>   
</table></html>
<html><table>
<tr><td><b> Repository </b></td></tr>
<tr><td>
Find more information and relevant code here: <a href="https://github.com/sseiber/peabody-local-service/blob/master/README.md">Github</a>.
</td></tr>
<tr><td>
<b> Future Improvements and Project Suggestions </b> </td></tr>
<tr><td>
  <add thoughts and ideas in terms of how "community" could develop these assets further to add functionality/application to project>
</td></tr>
</table></html>
<html><table>
<tr><td width="70%"><b> About the Creator </b> </td>
<td rowspan="2" width="30%"> <img src="images/scott.PNG" alt="i"> </td></tr>
<tr><td>
Scott Seiber is ... <add a short bio about your experience and interests, why you are working on this project>
</td></tr>
<tr><td>
You can learn more about what Scott is working on <a href="https://github.com/sseiber">here</a>.
</td></tr>
</table></html>



