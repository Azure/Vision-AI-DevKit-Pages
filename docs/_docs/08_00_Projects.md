---
layout: archive
title: "Project Catalog"
permalink: /docs/projects/
author_profile: false
---

<h3><a href="https://azure.github.io/Vision-AI-DevKit-Pages/docs/community_projects/" target="_blank"><b>What is a Community Project?</b></a>
<br>
<h3><a href="https://azure.github.io/Vision-AI-DevKit-Pages/docs/involvement/" target="_blank"><b>How can I contribute to the Community?</b></a>
<br>

<h3>Check out these Community Projects contributed by users of the Vision-AI-DevKit!</h3>


<div class="grid__wrapper grid__catalog">

  {% assign projects = '' | split: '' %} {% comment %} Empty array {% endcomment %}

  {% for project in site.projects %}
    
    {% comment %} Collect all the multi-part projects based on the presence of the part attribute of the file {% endcomment %}
    {% if project.part != nil and project.part == 1 %}
      {% assign projects = projects | push: project %}
      
    {% comment %} Collect all the single page projects {% endcomment %}
    {% elsif project.part == nil %}
      {% assign projects = projects | push: project %}
    
    {% endif %}

  {% endfor %}


  {% for post in projects %}
    {% include archive-single.html type="grid" %}
  {% endfor %}

</div>