---
layout: archive
title: "Curriculum Vitae"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<p class="rs-cv__name">Dr. rer. nat. Agnieszka Międlar</p>

<h2 class="rs-cvhead">Education</h2>
{% for degree in site.data.education %}{% include rs-cvrow.html item=degree %}{% endfor %}

<h2 class="rs-cvhead">Employment History</h2>
{% for job in site.data.employment %}{% include rs-cvrow.html item=job %}{% endfor %}

<h2 class="rs-cvhead">Invited Research Stays</h2>
{% for stay in site.data.research_stays %}{% include rs-cvrow.html item=stay %}{% endfor %}
