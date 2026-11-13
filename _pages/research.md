---
layout: single
title: "Research"
permalink: /research/
author_profile: true
---
{% include base_path %}

## Funding

### External Funding

{% assign grants = site.data.funding | sort: "end" | reverse %}{% for grant in grants %}{% include rs-cvrow.html item=grant %}{% endfor %}

### Internal Funding

{% assign grants = site.data.internal_funding | sort: "end" | reverse %}{% for grant in grants %}{% include rs-cvrow.html item=grant %}{% endfor %}

## Honors and Awards

{% for award in site.data.awards %}{% include rs-cvrow.html item=award %}{% endfor %}
