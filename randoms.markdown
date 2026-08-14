---
layout: page
title: Randoms
permalink: /randoms/
---

Solicited & Unsolicited thoughts. Not supported by substantial research. Seeds for current and future work.

<ul>
{% assign randoms = site.randoms | sort: "date" | reverse %}
{% for note in randoms %}
  <li>
    <a href="{{ note.url }}">
      {{ note.date | date: "%Y-%m-%d" }}
    </a>
  </li>
{% endfor %}
</ul>
