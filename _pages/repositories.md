---
layout: page
permalink: /repositories/
title: repositories
description: A curated list of GitHub profiles and repositories related to my projects and collaborations.
nav: true
nav_order: 5
---

GitHub profile: <a href="https://github.com/emmanuelatindama?tab=repositories">github.com/emmanuelatindama</a>

{% if site.data.repositories.github_repos %}

## Selected Repositories

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
{% endif %}
