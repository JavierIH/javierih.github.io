---
title: ""
permalink: /robots/
layout: single
author_profile: true
# Laid out in rows of 3; entries without a url are empty "?" tiles
robots:
  - { name: "EchoEar × Kame32", url: /robots/echoearxkame32/, image: /assets/images/echokame-square.jpg }
  - { name: "Kame32", url: /robots/kame32/, image: /assets/images/kame32-square.jpg }
  - { name: "Raider", url: /robots/raider/, image: /assets/images/raider-square.jpg }
  - { name: "Pandatron", url: /robots/pandatron/, image: /assets/images/pandatron-square.jpg }
  - { name: "Zowi", url: /robots/zowi/, image: /assets/images/zowi-square.jpg }
  - { name: "Abrelatas", url: /robots/abrelatas/, image: /assets/images/abrelatas-square.jpg }
  - { name: "Maus", url: /robots/maus/, image: /assets/images/maus-square.jpg }
  - { name: "Ratatron", url: /robots/ratatron/, image: /assets/images/ratatron-square.jpg }
  - { name: "Minikame", url: /robots/minikame/, image: /assets/images/minikame-low.jpg }
  - { name: "Micropanda", url: /robots/micropanda/, image: /assets/images/micropanda-square.jpg }
  - { name: "Beerbot", url: /robots/beerbot/, image: /assets/images/beerbot-square.jpg }
  - { name: "Twimaro", url: /robots/twimaro/, image: /assets/images/twimaro-square.jpg }
  - {}
  - { name: "Predator", url: /robots/predator/, image: /assets/images/predator-square.jpg }
  - { name: "Laser Tower", url: /robots/laser-tower/, image: /assets/images/laser-tower-square.jpg }
  - { name: "Zowimanoids", url: /robots/zowimanoids/, image: /assets/images/zowimanoids-square.jpg }
  - {}
  - {}
  - {}
  - { name: "Erizos bailones", url: /robots/erizos-bailones/, image: /assets/images/erizos-square.jpg }
  - {}
---

<div class="robots-grid">
{% for robot in page.robots %}
  {% if robot.url %}
  <a class="robots-grid__item" href="{{ robot.url | relative_url }}">
    <img src="{{ robot.image | relative_url }}" alt="{{ robot.name }}" loading="lazy">
    <span>{{ robot.name }}</span>
  </a>
  {% else %}
  <div class="robots-grid__item">
    <img src="{{ '/assets/images/empty.jpg' | relative_url }}" alt="">
  </div>
  {% endif %}
{% endfor %}
</div>
