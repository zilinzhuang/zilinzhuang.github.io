---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <div class="wordwrap">You can also find my articles on <a href="{{ site.author.googlescholar }}">my Google Scholar profile</a>.</div>
{% endif %}

{% include base_path %}

## Journal Papers
{% for post in site.publications reversed %}
  {% if post.publication_type == "journal"
        or post.pubtype == "journal"
        or post.type == "journal"
        or post.venue contains "Journal"
        or post.venue contains "Transactions"
        or post.venue contains "Letters" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

## Conference Papers
{% for post in site.publications reversed %}
  {% if post.publication_type == "conference"
        or post.pubtype == "conference"
        or post.type == "conference"
        or post.venue contains "Conference"
        or post.venue contains "Conf."
        or post.venue contains "Symposium"
        or post.venue contains "Workshop" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}
