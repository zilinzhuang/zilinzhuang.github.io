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


### Travel

<style>
  /* 滚动相册的外部容器 */
  .scroll-album {
    display: flex;           /* 让内部的图片横向排列 */
    overflow-x: auto;        /* 内容超出时允许横向滚动 */
    gap: 16px;               /* 照片之间的间距 */
    padding-bottom: 15px;    /* 底部留白，防止滚动条挡住文字 */
    scroll-snap-type: x mandatory; /* 增加滚动时的吸附手感（可选） */
  }

  /* 每一张照片和描述的容器 */
  .scroll-album figure {
    flex: 0 0 auto;          /* 防止照片被自动挤压变窄 */
    margin: 0;
    width: 240px;            /* 【修改这里】：控制每张照片的宽度 */
    scroll-snap-align: start;
  }

  /* 照片本身的样式 */
  .scroll-album img {
    width: 100%;
    height: 180px;           /* 【修改这里】：控制照片的统一高度 */
    object-fit: cover;       /* 确保照片被裁剪以填充框距，且不会变形 */
    border-radius: 8px;      /* 增加一点圆角让照片看起来更精致（不需要可删除） */
  }

  /* 照片下方的文字描述 */
  .scroll-album figcaption {
    font-size: 0.85em;
    opacity: 0.75;
    margin-top: 0.5rem;
    text-align: center;
    line-height: 1.3;
    white-space: normal;     /* 允许文字多行显示 */
  }

  /* 优化滚动条的外观（仅在支持 Webkit 的浏览器生效） */
  .scroll-album::-webkit-scrollbar {
    height: 6px;
  }
  .scroll-album::-webkit-scrollbar-thumb {
    background-color: #cccccc;
    border-radius: 4px;
  }
</style>

<div class="scroll-album">
  <figure>
    <img src="{{ '/images/IMG_5209.JPG' | relative_url }}" alt="Mt. Siguniang, Sichuan, China">
    <figcaption>Mt. Siguniang, Sichuan, China</figcaption>
  </figure>

  <figure>
    <img src="{{ '/images/IMG_7352.JPG' | relative_url }}" alt="Charles River, Boston, USA">
    <figcaption>Charles River, Boston, MA, USA</figcaption>
  </figure>

  </div>

{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
