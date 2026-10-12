---
layout: page
title: Frames
permalink: /frames/
---

{% include mathjax.html %}

Some scenes of Fiction. Mostly science, technology and philosophy adjacent.
Cinematic fragments if you'd like.

<ul>
{% assign scenes = site.scenes | sort: "date" | reverse %}
{% for scene in scenes %}
  <li>
    <a href="{{ scene.url }}">
      {{ scene.title }}
    </a>
  </li>
{% endfor %}
</ul>
