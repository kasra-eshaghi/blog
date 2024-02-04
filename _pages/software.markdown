---
layout: single
title: "HEY! Software here!"
permalink: /software/
---

The software projects below were mostly completed during my PhD. Anything related to swarms is from the research I completed at the <a href="https://cimlab.mie.utoronto.ca/" target="_blank">Computer Integrated Manufacturing Lab</a> and the <a href="http://asblab.mie.utoronto.ca/" target="_blank">Autonomous Systems and Biomechatronics Lab</a>, both at the University of Toronto. 

{% for project in site.software %}
  <h2>
    <a href="{{ site.baseurl }}{{ project.url }}">
      {{ project.title }}
    </a>
  </h2>
  
  <p>{{ project.excerpt }}</p>
  
{% endfor %}

