---
page_id: events
layout: page
title: events
permalink: /events/
description: A growing collection of events planned and organised by the GIL
nav: true
nav_order: 3
display_categories: [2026]
horizontal: false
---

<!-- pages/events.md -->
<div class="events">
  {% if site.enable_event_categories and page.display_categories %}
    <!-- Display categorized events -->
    {% for category in page.display_categories %}
      <a id="{{ site.data[site.active_lang].strings.categories[category] }}" href=".#{{ site.data[site.active_lang].strings.categories[category] }}">
        <h2 class="category">{{ site.data[site.active_lang].strings.categories[category] }}</h2>
      </a>
      {% assign categorized_events = site.events | where: "category", category %}
      {% assign sorted_events = categorized_events | sort: "importance" %}
      <!-- Generate cards for each event -->
      {% if page.horizontal %}
        <div class="container">
          <div class="row row-cols-1 row-cols-md-2">
            {% for event in sorted_events %}
              {% include events_horizontal.liquid %}
            {% endfor %}
          </div>
        </div>
      {% else %}
        <div class="row row-cols-1 row-cols-md-3">
          {% for event in sorted_events %}
            {% include events.liquid %}
          {% endfor %}
        </div>
      {% endif %}
    {% endfor %}
  {% else %}
    <!-- Display events without categories -->
    {% assign sorted_events = site.events | sort: "importance" %}
    <!-- Generate cards for each event -->
    {% if page.horizontal %}
      <div class="container">
        <div class="row row-cols-1 row-cols-md-2">
          {% for event in sorted_events %}
            {% include events_horizontal.liquid %}
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="row row-cols-1 row-cols-md-3">
        {% for event in sorted_events %}
          {% include events.liquid %}
        {% endfor %}
      </div>
    {% endif %}
  {% endif %}
</div>
