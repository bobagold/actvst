---
layout: single
lang: en
title: "Get in Touch for Mobile Development Projects"
---

{% assign t = site.data.translations.en.contact %}

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