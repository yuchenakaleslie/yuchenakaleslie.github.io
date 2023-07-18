---
layout: page
title: programs
permalink: /programs/
description: Open-source programs and applications
nav: true
nav_order: 3
display_categories: [work, collaboration]
horizontal: false
---

<!-- pages/programs.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized programs -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_programs = site.programs | where: "category", category -%}
  {%- assign sorted_programs = categorized_programs | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for program in sorted_programs -%}
      {% include programs_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for program in sorted_programs -%}
      {% include programs.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
  <!-- Display programs without categories -->  
  {%- assign sorted_programs = site.programs | sort: "importance" -%}
  <!-- Generate cards for each program -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for program in sorted_programs -%}
      {% include programs_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for program in sorted_programs -%}
      {% include programs.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>
