---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% include base_path %}

{% if site.author.googlescholar %}
<div class="wordwrap">
  You can also find my articles on <a href="{{ site.author.googlescholar }}">my Google Scholar profile</a>.
</div>
{% endif %}

{% assign pubs = site.publications | sort: "date" | reverse %}
{% capture me %}{{ site.author.name | default: site.name }}{% endcapture %}
{% capture me_bold %}<strong>{{ me }}</strong>{% endcapture %}

## Preprints
<ul class="pub-list">
{% for post in pubs %}
  {% if post.publication_type == "preprint"
        or post.pubtype == "preprint"
        or post.type == "preprint"
        or post.venue contains "Preprint"
        or post.venue contains "preprint"
        or post.venue contains "arXiv"
        or post.venue contains "ArXiv" %}
    <li>
      {%- comment -%} 优先使用 citation 字段；没有就拼接作者/年份/题目/期刊 {%- endcomment -%}
      {% capture cit %}
        {% if post.citation %}
          {{ post.citation }}
        {% else %}
          {{ post.authors | default: "" }}{% if post.date %} ({{ post.date | date: "%Y" }}){% endif %}. {{ post.title }}. {{ post.venue }}.
        {% endif %}
      {% endcapture %}
      {% assign cit = cit | replace: me, me_bold %}
      {{ cit | markdownify | replace: "<p>", "" | replace: "</p>", "" }}

      {%- assign linkurl = post.paperurl -%}
      {%- if linkurl == nil or linkurl == "" -%}{% assign linkurl = post.link %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.doi -%}{% assign linkurl = "https://doi.org/" | append: post.doi %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.arxiv -%}{% assign linkurl = "https://arxiv.org/abs/" | append: post.arxiv %}{% endif -%}
      {% if linkurl %} (<a href="{{ linkurl }}">Link</a>){% endif %}.
    </li>
  {% endif %}
{% endfor %}
</ul>

## Journal Papers
<ul class="pub-list">
{% for post in pubs %}
  {% if post.publication_type == "journal"
        or post.pubtype == "journal"
        or post.type == "journal"
        or post.venue contains "Journal"
        or post.venue contains "Transactions"
        or post.venue contains "Letters" %}
    <li>
      {% capture cit %}
        {% if post.citation %}
          {{ post.citation }}
        {% else %}
          {{ post.authors | default: "" }}{% if post.date %} ({{ post.date | date: "%Y" }}){% endif %}. {{ post.title }}. {{ post.venue }}.
        {% endif %}
      {% endcapture %}
      {% assign cit = cit | replace: me, me_bold %}
      {{ cit | markdownify | replace: "<p>", "" | replace: "</p>", "" }}

      {%- assign linkurl = post.paperurl -%}
      {%- if linkurl == nil or linkurl == "" -%}{% assign linkurl = post.link %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.doi -%}{% assign linkurl = "https://doi.org/" | append: post.doi %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.arxiv -%}{% assign linkurl = "https://arxiv.org/abs/" | append: post.arxiv %}{% endif -%}
      {% if linkurl %} (<a href="{{ linkurl }}">Link</a>){% endif %}.
    </li>
  {% endif %}
{% endfor %}
</ul>

## Conference Papers
<ul class="pub-list">
{% for post in pubs %}
  {% if post.publication_type == "conference"
        or post.pubtype == "conference"
        or post.type == "conference"
        or post.venue contains "Conference"
        or post.venue contains "Conf."
        or post.venue contains "Symposium"
        or post.venue contains "Workshop" %}
    <li>
      {% capture cit %}
        {% if post.citation %}
          {{ post.citation }}
        {% else %}
          {{ post.authors | default: "" }}{% if post.date %} ({{ post.date | date: "%Y" }}){% endif %}. {{ post.title }}. {{ post.venue }}.
        {% endif %}
      {% endcapture %}
      {% assign cit = cit | replace: me, me_bold %}
      {{ cit | markdownify | replace: "<p>", "" | replace: "</p>", "" }}

      {%- assign linkurl = post.paperurl -%}
      {%- if linkurl == nil or linkurl == "" -%}{% assign linkurl = post.link %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.doi -%}{% assign linkurl = "https://doi.org/" | append: post.doi %}{% endif -%}
      {%- if (linkurl == nil or linkurl == "") and post.arxiv -%}{% assign linkurl = "https://arxiv.org/abs/" | append: post.arxiv %}{% endif -%}
      {% if linkurl %} (<a href="{{ linkurl }}">Link</a>){% endif %}.
    </li>
  {% endif %}
{% endfor %}
</ul>

<style>
/* 简洁列表样式，接近截图效果 */
.pub-list { list-style: square; padding-left: 1.2rem; }
.pub-list li { margin: .6rem 0; line-height: 1.5; }
</style>
