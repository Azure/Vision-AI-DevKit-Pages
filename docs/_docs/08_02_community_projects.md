---
title: "Community Project: Workplace Safety Identification"
permalink: /docs/community_project02
excerpt: "Ensuring worplace safety using Custom Vision ML and Azure services"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
comments: 
  provider: "disqus"
  disqus: 
    shortname: https-azure-github-io-vision-ai-devkit-pages-docs-community-pr.disqus.com
last_modified_at: 2019-08-20
---
<br>
<html>
<table><tr><td><b>Summary</b></td></tr>
<tr><td>
This project demonstrates the implementation of a Custom Vision ML model to the Vision AI DevKit to identify the presence of workplace safety equipment such as hardhats, vests, and safety glasses. As each object is detected, the information is stored and an alarm is triggered when a person that is not wearing the specified eqipment is detected in the frame.  <br> </td></tr>
</table></html>

<html><table>
<tr><td>
<b> Implementation </b> </td></tr>
<tr><td>
In addition to the standard Custom Vision ML model, Azure services are used for a number of functions in this project. Azure Stream Analytics is the main program in use, which detects information captured by the DevKit in real time. Blob storage is utilized for long term storage of detected objects, Azure SQL database is used to process the collected data, and Azure App Services generates the website to view the information (shown below).  <br>
</td></tr></table></html>
<html><tr> <img src="images/workplace_detectionscreen.PNG" alt="i"> </tr> 
<tr><img src="images/workplace_graphs.PNG" alt="i"></tr>
<html><table>
 <tr>
    <td width = "50%"> <b> Software and Services used</b> </td>
    <td width = "50%"> <b> Hardware </b> </td> 
    <td rowspan="24"></td> </tr>
 <tr>
    <td> <ul type="disc" >
            <li>Custom Vision</li>
            <li>Azure Stream Analytics</li>
            <li>Azure SQL database</li>
            <li>Azure App Services</li>
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
Download the photos used to train the Custom Vision workplace module <a href="https://bbiotstore.blob.core.windows.net/others/WorkplaceSafetyPics.zip">here</a>. <br>
Alternatively, downlod the Custom Vision model zip file <a href="https://bbiotstore.blob.core.windows.net/others/Model.zip">here</a>. <br>
Find more information and relevant code <a href="https://github.com/sseiber/peabody-local-service/blob/master/README.md">here</a>. <br>
Users are always encouraged to innovate and continue to improve the functionality of current projects. 
</td></tr>
<tr><td>
<b> Future Improvements and Project Suggestions </b> </td></tr>
<tr><td>
 EXPAND ON POTENTIAL PROJECTS THAT CAN USE THIS CODE OR WAYS USERS CAN CONTRIBUTE TO FUNCTIONALITY
  Feel free to fork the project and contribute back any improvements or suggestions. Contributors and maintainers are encouraged.
</td></tr>
</table></html>
<html><table>
<tr><td width="70%"><b> About the Creator </b> </td></tr>
<!-- <td rowspan="2" width="30%"> <img src="images/scott.PNG" alt="i"> </td></tr> -->
<td>
INSERT SHORT BIO HERE
<br>
You can learn more about what Scott is working on <a href="https://github.com/sseiber">LINK TO GITHUB WILL GO HERE</a>.
</td>
</table></html>

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = https://azure.github.io/Vision-AI-DevKit-Pages/docs/community_project02#;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = community_project_01; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://https-azure-github-io-vision-ai-devkit-pages.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            


