---
layout: archive
title: "More about ZZL"
permalink: /portfolio/
author_profile: true
---

{% include base_path %}

Hi, I'm ZZL. I grew up in Jiangsu, China, and I’m the kind of person who keeps collecting hobbies. 
Feel free to connect with me on <a href="https://www.instagram.com/zilinpurple?igsh=MWZia284aDF3Y3Zqcw%3D%3D&utm_source=qr" target="_blank" rel="noopener">Instagram</a>.

###Sports
I’m genuinely passionate about sports — basketball, table tennis, badminton, Go, hiking… you name it. I also love trying new activities whenever I get the chance.

###Art
Music is another big part of my life. I play guitar and drums, do arranging/production, and I also run a small personal music podcast.

I’m a huge fan of storytelling across different forms — literature, movies/TV, and video games.  
Some of my all-time favorite books include:
- *The King of Chess* — Acheng  
- *Siddhartha* — Hermann Hesse  
- *1Q84* — Haruki Murakami  
- *The Myth of Sisyphus* — Albert Camus  

###Travel
I love traveling too!

<figure class="half">
  <img src="{{ '/assets/images/travel-1.jpg' | relative_url }}" alt="Travel photo 1">
  <img src="{{ '/assets/images/travel-2.jpg' | relative_url }}" alt="Travel photo 2">
</figure>

{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
