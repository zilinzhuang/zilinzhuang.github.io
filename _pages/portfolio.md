---
layout: archive
title: "More about ZZL"
permalink: /portfolio/
author_profile: true
---

{% include base_path %}

Hi, I'm ZZL. I grew up in Jiangsu, China, and I’m the kind of person who keeps collecting hobbies. 
Feel free to connect with me on <a href="https://www.instagram.com/zilinpurple?igsh=MWZia284aDF3Y3Zqcw%3D%3D&utm_source=qr" target="_blank" rel="noopener">Instagram</a>.

### Sports
I’m genuinely passionate about sports — basketball, table tennis, badminton, Go, hiking… you name it. I also love trying new activities whenever I get the chance.

### Art
Music is another big part of my life. I play guitar and drums, do arranging/production, and I also run a small personal music podcast.

I’m a huge fan of storytelling across different forms — literature, movies/TV, and video games.  
Some of my all-time favorite books include:
- *The King of Chess* — Acheng  
- *Siddhartha* — Hermann Hesse  
- *1Q84* — Haruki Murakami  
- *The Myth of Sisyphus* — Albert Camus  

### Travel
盖将自其变者而观之，则天地曾不能以一瞬；自其不变者而观之，则物与我皆无尽也，而又何羡乎！——苏轼
<figure class="half">
  <figure>
    <img src="{{ '/images/IMG_5209.JPG' | relative_url }}" alt="Mt. Siguniang, Sichuan, China">
    <figcaption style="font-size: 0.85em; opacity: 0.75; margin-top: 0.35rem;">
      Mt. Siguniang, Sichuan, China
    </figcaption>
  </figure>

  <figure>
    <img src="{{ '/images/IMG_7352.JPG' | relative_url }}" alt="Charles River, Boston, USA">
    <figcaption style="font-size: 0.85em; opacity: 0.75; margin-top: 0.35rem;">
      Charles River, Boston, MA, USA
    </figcaption>
  </figure>
</figure>


{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
