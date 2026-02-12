---
layout: single
lang: de
title: "Kontaktieren Sie uns für Mobile-Entwicklungsprojekte"
---

{% assign t = site.data.translations.de.contact %}

{% include language-switcher.html %}

## {{ t.heading }}

{{ t.intro }}

### {{ t.services_heading }}

{% for service in t.services %}
- **{{ service.title }}** - {{ service.description }}
{% endfor %}

### {{ t.ready_heading }}

{{ t.ready_text }}

**{{ t.email_label }}** [bobagold.actvst@gmail.com](mailto:bobagold.actvst@gmail.com)

**{{ t.connect_label }}** [GitHub](https://github.com/bobagold)

*{{ t.footer_text }}*
