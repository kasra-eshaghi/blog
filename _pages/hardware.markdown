---
title: "Hey! Hardware here!"
permalink: /hardware/
---
<style>
p {
  text-align: justify;
}
</style>


A good engineer knows hardware better than software. That's because hardware can work without software, but software is nothing without hardware! 

Below are some of the fun hardware projects I've worked on in the past. Though, I admit, none of them would work without software. 


{% for project in site.hardware %}
  <h2>
    <a href="{{ site.baseurl }}{{ project.url }}">
      {{ project.title }}
    </a>
  </h2>
{% endfor %}
