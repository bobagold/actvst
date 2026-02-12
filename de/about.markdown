---
layout: single
lang: de
title: "Über uns"
---

{% assign t = site.data.translations.de.about %}

{% include language-switcher.html %}

## {{ t.mission_heading }}

{{ t.mission_text }}

### {{ t.team_heading }}

| ![Vladimir](/assets/images/vladimir.png){: .avatar-circle } | ![Polina](/assets/images/polina.jpg){: .avatar-circle } |
| {{ t.team.vladimir.name }} | {{ t.team.polina.name }} |
| {{ t.team.vladimir.role }} | {{ t.team.polina.role }} |

### {{ t.vision_heading }}

{{ t.vision_text }}
