---
layout: page
title: playground
permalink: /playground/
description: Interactive things I have built, mostly about the places where intuition and arithmetic disagree. Everything here runs in your browser.
nav: true
nav_order: 4
horizontal: false
---

<!-- Cards come from the `_projects` collection: one markdown file per project,
     sorted by its `importance` field. Adding a project here means adding a file
     to _projects/ and nothing else -- this page does not name any of them. -->

<div class="projects">
  {% assign sorted_projects = site.projects | sort: "importance" %}
  {% if sorted_projects.size > 0 %}
    <div class="row row-cols-1 row-cols-md-2 g-4">
      {% for project in sorted_projects %}
        {% include projects.liquid %}
      {% endfor %}
    </div>
  {% else %}
    <p>Nothing here yet.</p>
  {% endif %}
</div>
