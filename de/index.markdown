---
layout: single
lang: de
title: "Innovative Mobile-Entwicklungslösungen für iOS & Android"
---

{% assign t = site.data.translations.de.home %}

{% include language-switcher.html %}

## {{ t.heading }}

{{ t.intro }}

- **{{ t.services[0] }}**
- **{{ t.services[1] }}**
- **{{ t.services[2] }}**
- **{{ t.services[3] }}**

### {{ t.projects_heading }}

{{ t.projects_intro }}

[{{ t.view_projects }}](projects.html)

---

## {{ t.articles_heading }}

{% assign client_posts = site.posts | where: "audience", "clients" | where: "lang", "de" %}
<div class="entries-list">
{% for post in client_posts limit:10 %}
  <div style="margin-bottom: 2em;">
    {% include archive-single.html type="list" %}
  </div>
{% endfor %}
</div>
