---
title: "Interview"
layout: archive
permalink: categories/interview
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories['Interview'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}