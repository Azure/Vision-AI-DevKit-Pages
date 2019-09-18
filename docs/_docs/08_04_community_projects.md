---
title: "Sign Language Gesture Recognition "
permalink: /docs/community_project04/
excerpt: "Recognizing sign language symbols representing the alphabet"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
comments: 
  provider: "disqus"
  disqus: 
    shortname: https-azure-github-io-vision-ai-devkit-pages-docs-community-pr.disqus.com
last_modified_at: 2019-09-4
---
<br>
<html>
<table><tr><td><b>Summary</b></td></tr>
<tr><td>
The idea for this project came from a <a href="https://www.kaggle.com/datamunge/sign-language-mnist" target="_blank">Kaggle competition</a>. The goal for the competition was to help the deaf and hard-of-hearing better communicate using computer vision applications. The National Institute on Deafness and other Communications Disorders (NIDCD) indicates that the 200-year-old American Sign Language is a complete, complex language (of which letter gestures are only part) but is the primary language for many deaf North Americans. ASL is the leading minority language in the U.S. after the "big four": Spanish, Italian, German, and French. One could implement computer vision and some Text-to-Speech to enabling improved and automated translation applications. The original project was created over a year ago using Android App as the edge device, this is the updated version of it using the Vision AI Dev Kit camera as the edge device. <br> </td></tr>
</table></html>

<html><table>
<tr><td>
<b> Implementation </b> </td></tr>
<tr><td>
The project uses the Custom Vision service to create and export the model and integrates it with the Vision AI DevKit.
</td></tr>
</table></html>

<html> <table>
<tr>
<td width="50%"><img src="{{'assets/images/signlanguagetraining.png' | relative_url}}"></td>
<td width="50%"> <img src="{{'assets/images/signlanguagerecognition.jpg' | relative_url}}"> </td>
</tr>
</table></html>


<html><table>
<tr>
    <td width = "50%"> <b> Software and Services used</b> </td>
    <td width = "50%"> <b> Hardware </b> </td> 
    <td rowspan="24"></td> </tr>
 <tr>
    <td> <ul type="disc" >
            <li>Custom Vision</li>
            <li>Azure IoT Hub</li>
            <li>Azure Storage Account</li>
            <li>VLC Media Player</li>
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
Find all relevant information, including code, pictures used for model training, and the Custom Vision model file for full implementation of this product <a href="https://aka.ms/signlanguage-vaghela" target="_blank">here</a>. <br>
Users are always encouraged to innovate and continue to improve the functionality of current projects. 
</td></tr>
<tr><td>
<b> Future Improvements and Project Suggestions </b> </td></tr>
<tr><td>
One potential additional function could be to enable audio output using the built-in speakers of the camera. 
 <br>
  Feel free to fork the project and contribute back any improvements or suggestions. Contributors and maintainers are encouraged.
</td></tr>
</table></html>

<html><table>
<tr><td width="30%"><b> About the Creator </b> </td></tr>
<tr><td rowspan="2" width="30%"> <img src="{{'assets/images/jomit.jpg' | relative_url}}"></td></tr>
<td width = "70%">
Jomit Vaghela is a Technology Strategist, Architect and Developer working on fulfilling the promises of Digital Transformation using Machine Learning, IoT, Blockchain and Cloud.
<br>
You can learn more about what Jomit is working on <a href="https://github.com/jomit " target="_blank">here</a>.
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
this.page.identifier = community_project_04; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
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
                             


