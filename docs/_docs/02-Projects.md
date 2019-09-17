---
layout: archive
title: "Project Catalog"
permalink: /docs/projects/
author_profile: false
---

<h3>Official tutorials that guide you build and learn Vision-AI-DevKit.</h3>


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