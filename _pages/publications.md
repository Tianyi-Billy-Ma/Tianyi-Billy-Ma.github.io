---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <div class="wordwrap">You can also find my articles on <a href="{{site.author.googlescholar}}">my Google Scholar profile</a>.</div>
{% endif %}

{% include base_path %}

{% assign sorted = site.publications | sort: "date" | reverse %}
{% assign preprints = sorted | where: "category", "preprints" %}
{% assign survey = sorted | where: "category", "survey" %}
{% assign confs = sorted | where: "category", "conference" %}

{% if preprints.size > 0 %}
<h2 class="pub-year-heading">Preprints</h2>
<div class="pub-list">
{% for post in preprints %}{% include pub-entry.html %}{% endfor %}
</div>
{% endif %}

{% if survey.size > 0 %}
<h2 class="pub-year-heading">Survey</h2>
<div class="pub-list">
{% for post in survey %}{% include pub-entry.html %}{% endfor %}
</div>
{% endif %}

{% assign current_year = "" %}
{% for post in confs %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% if this_year != current_year %}
{% unless forloop.first %}</div>{% endunless %}
<h2 class="pub-year-heading">{{ this_year }}</h2>
<div class="pub-list">
{% assign current_year = this_year %}
{% endif %}
{% include pub-entry.html %}
{% if forloop.last %}</div>{% endif %}
{% endfor %}
