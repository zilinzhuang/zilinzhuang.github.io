---
layout: archive
title: "More about ZZL"
permalink: /portfolio/
author_profile: true
---

{% include base_path %}

Hi, I'm ZZL. I grew up in Jiangsu, China, and I’m someone with many hobbies.
Feel free to connect with me on <a href="https://www.instagram.com/zilinpurple?igsh=MWZia284aDF3Y3Zqcw%3D%3D&utm_source=qr" target="_blank" rel="noopener">Instagram</a>.

### Sports
I’m genuinely passionate about sports — basketball, table tennis, badminton, Go, hiking… you name it. I also love trying new activities whenever I get the chance.

### Art
Music is another big part of my life. I play guitar and drums, do arranging/production, and I also run a small personal music podcast.

I’m also a huge fan of literature, movies/TV, video games and chinese calligraphy.  
Some of my favorite books include:
- *The King of Chess* — Acheng  
- *Siddhartha* — Hermann Hesse  
- *1Q84* — Haruki Murakami  
- *The Myth of Sisyphus* — Albert Camus  


<style>
  .travel-album{
    display: flex;
    gap: 1rem;
    overflow-x: auto;
    padding: 0.5rem 0 1rem;
    scroll-snap-type: x mandatory;
    -webkit-overflow-scrolling: touch;
  }

  .travel-item{
    flex: 0 0 auto;
    width: clamp(220px, 55vw, 320px);  /* 控制照片显示不要太大 */
    margin: 0;
    scroll-snap-align: start;
  }

  .travel-item img{
    width: 100%;
    height: 210px;         /* 统一高度，避免忽大忽小 */
    object-fit: cover;     /* 裁切填满 */
    border-radius: 10px;   /* 可删 */
    display: block;
  }

  .travel-item figcaption{
    font-size: 0.85em;
    opacity: 0.75;
    margin-top: 0.35rem;
  }
</style>


### Travel


<div class="travel-album" aria-label="Travel photo album">
  <figure class="travel-item">
    <img
      src="{{ '/images/IMG_5209.JPG' | relative_url }}"
      alt="Mt. Siguniang, Sichuan, China"
      loading="lazy"
      decoding="async"
    >
    <figcaption>
      Mt. Siguniang, Sichuan, China
    </figcaption>
  </figure>

  <figure class="travel-item">
    <img
      src="{{ '/images/IMG_7352.JPG' | relative_url }}"
      alt="Charles River, Boston, USA"
      loading="lazy"
      decoding="async"
    >
    <figcaption>
      Charles River, Boston, MA, USA
    </figcaption>
  </figure>

</div>

{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
