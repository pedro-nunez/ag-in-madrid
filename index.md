---
layout: default
title: Algebraic Geometry in Madrid
---

<div class="info-toggle-wrap">
  <button type="button" id="info-toggle" class="info-toggle" aria-expanded="false" aria-controls="info-popup" title="About this website" aria-label="About this website">&#9432;</button>
  <div id="info-popup" class="info-popup" hidden>
    <p>A list of algebraic geometry conferences, workshops, and seminars
    in Madrid.</p>
    <p>You can suggest to add an event through the Add Event button. Any
    help keeping this list up to date is appreciated!</p>
    <p class="info-popup-credit">&mdash; Maintained by
    <a href="https://pedro-nunez.github.io/">Pedro Núñez</a> &mdash;</p>
  </div>
</div>

<div class="last-updated-bar">
  <p class="last-updated">Last updated in {{ site.time | date: "%B %Y" }}</p>
</div>

<h1>Algebraic Geometry in Madrid</h1>

[Add Event](https://github.com/pedro-nunez/ag-in-madrid/issues/new?template=add-event.yml){: .button }

{% assign today = site.time | date: "%Y-%m-%d" %}
{% assign events = site.data['madrid-events'] %}
{% assign upcoming = "" | split: "" %}
{% assign past = "" | split: "" %}
{% for event in events %}
  {% assign cutoff = event.end | default: event.start | date: "%Y-%m-%d" %}
  {% assign one = events | slice: forloop.index0, 1 %}
  {% if cutoff >= today %}
    {% assign upcoming = upcoming | concat: one %}
  {% else %}
    {% assign past = past | concat: one %}
  {% endif %}
{% endfor %}
{% assign upcoming = upcoming | sort: "start" %}
{% assign past = past | sort: "start" | reverse %}

## Upcoming

<ul>
{% for event in upcoming %}
  <li>
    {% include date-range.html start=event.start end=event.end %}:
    {% if event.url %}<a href="{{ event.url }}" class="event-link">{{ event.title }}</a>{% else %}{{ event.title }}{% endif %},
    at {{ event.institution }}.
  </li>
{% endfor %}
</ul>

## Past

<ul>
{% for event in past %}
  <li>
    {% include date-range.html start=event.start end=event.end %}:
    {% if event.url %}<a href="{{ event.url }}" class="event-link">{{ event.title }}</a>{% else %}{{ event.title }}{% endif %},
    at {{ event.institution }}.
  </li>
{% endfor %}
</ul>
