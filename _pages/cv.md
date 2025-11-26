---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<p>
  <a href="{{ '/files/ZilinZhuang_CV.pdf' | relative_url }}" target="_blank">
    👉 点击这里打开我的 CV（PDF）
  </a>
</p>

<!-- 在页面中内嵌显示 PDF，如果浏览器不支持，会显示下载链接 -->
<object data="{{ '/files/ZilinZhuang_CV.pdf' | relative_url }}" type="application/pdf" width="100%" height="1000px">
  <p>
    如果浏览器没有直接显示 PDF，请点击这里下载：
    <a href="{{ '/files/ZilinZhuang_CV.pdf' | relative_url }}">下载我的 CV（PDF）</a>
  </p>
</object>
