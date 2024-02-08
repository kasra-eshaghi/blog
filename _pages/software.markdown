---
layout: single
title: "HEY! Software here!"
permalink: /software/
---
<style>
p {
  text-align: justify;
}
</style>

The software projects below were mostly completed during my PhD, where I worked on leveraging inter-robot collaboration to address the sensing limitations of individual robots in a swarm. This research was completed at the <a href="https://cimlab.mie.utoronto.ca/" target="_blank">Computer Integrated Manufacturing Lab</a> and the <a href="http://asblab.mie.utoronto.ca/" target="_blank">Autonomous Systems and Biomechatronics Lab</a>, both at the University of Toronto.

{% for project in site.software %}
  <h2>
    <a href="{{ site.baseurl }}{{ project.url }}">
      {{ project.title }}
    </a>
  </h2>
  
  <p>{{ project.excerpt }}</p>
  
{% endfor %}
