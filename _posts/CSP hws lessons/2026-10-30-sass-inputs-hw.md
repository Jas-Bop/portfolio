---
layout: post
title: SASS Inputs HW
codemirror: true
categories: [SASS]
lesson_language: SASS
lesson_topic: Inputs HW
lesson_part: interactive
lesson_type: lesson
permalink: /sass/inputs-hw/
author: Jas-Bop
---

## Popcorn Hack: Class-Based Inputs

{% capture input_challenge0 %}Popcorn Hack: Class-Based Inputs{% endcapture %}

{% capture input_code0 %}
outputElement.innerHTML = [
  '<label for="inputs-popcorn-resource">Search PVO resources</label>',
  '<input id="inputs-popcorn-resource" name="resourceSearch" type="text" class="ocs__input large gradient" placeholder="Search PVO resources...">',
  '<label for="inputs-popcorn-name">Volunteer first name</label>',
  '<input id="inputs-popcorn-name" name="volunteerFirstName" type="text" class="ocs__input small" placeholder="Volunteer First Name" autocomplete="given-name">'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-inputs-hw-0"
   challenge=input_challenge0
   code=input_code0
%}

## Homework Hack: Signup Inputs

{% capture input_challenge1 %}Homework Hack: Signup Inputs{% endcapture %}

{% capture input_code1 %}
outputElement.innerHTML = [
  '<label for="inputs-homework-category">Assistance category</label>',
  '<input id="inputs-homework-category" name="assistanceCategory" type="text" class="ocs__input large gradient" placeholder="Assistance Category">',
  '<label for="inputs-homework-name">Volunteer first name</label>',
  '<input id="inputs-homework-name" name="volunteerFirstName" type="text" class="ocs__input small" placeholder="Volunteer First Name" autocomplete="given-name">',
  '<label for="inputs-homework-email">Volunteer email</label>',
  '<input id="inputs-homework-email" name="volunteerEmail" type="email" class="ocs__input medium" placeholder="Volunteer Email" autocomplete="email">'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-inputs-hw-1"
   challenge=input_challenge1
   code=input_code1
%}
