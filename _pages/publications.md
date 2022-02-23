---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

Selected Publications with significant contribution
=================

**Search for vector-like leptons in the multilepton final states in pp collisions at sqrt(s)=13 TeV**, The CMS Collaboration, Phys. Rev. D 100, 052003 (2019)

**Search for new physics in multilepton final states in pp collisions at sqrt(s)=13 TeV**, The CMS Collaboration, CMS-PAS-EXO-19-002

**Search for vector-like leptons in the multilepton final states in pp collisions at sqrt(s)=13 TeV**, The CMS Collaboration, CMS-PAS-EXO-18-005

**Search for evidence of the Type-III Seesaw Mechanism in multilepton final states in proton-proton Collisions at sqrt(s)=13 TeV**, The CMS Collaboration, Phys. Rev. Lett.  119, 221802 (2017)

**Electron and photon reconstruction and identification with the CMS experiment at the CERN LHC**, The CMS Collaboration, JINST 16 , 05 (2021) P05014

**Search for Type-III Seesaw Heavy Fermions with Multilepton Final States using 2.3/fb of 13 TeV proton-proton Collision Data**, The CMS Collaboration, CMS-PAS-EXO-16-002


{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
