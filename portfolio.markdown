---
layout: single
lang: en
title: "Flutter & Firebase Mobile App Portfolio"
---

{% assign t = site.data.translations.en.portfolio.fifteentwenty %}

{% include language-switcher.html %}

## <img src="{% link assets/images/1520/logo.png %}" alt="Fifteentwenty — 1520" width="50" height="50" class="avatar-circle"> - {{ t.heading }}

**{{ t.role }}**  
**{{ t.tech_stack }}** {{ t.tech_list }}  
**{{ t.duration }}** {{ t.duration_text }}  
**{{ t.support }}** {{ t.support_text }}

![Fifteentwenty — 1520]({% link assets/images/1520/screen.png %})

{{ t.intro }}

### {{ t.contributions_heading }}
{% for contribution in t.contributions %}
- {{ contribution }}
{% endfor %}

{{ t.outro }} [{{ t.postmortem }}](https://www.sunsethq.com/blog/why-did-1520-fail) [{{ t.more_details }}]({% post_url 2025-02-26-developing-1520 %})