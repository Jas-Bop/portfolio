---
layout: post
title: SASS Button Grammar HW
codemirror: true
categories: [SASS]
lesson_language: SASS
lesson_topic: Buttons HW
lesson_part: interactive
lesson_type: lesson
permalink: /sass/buttons-hw/ 
author: Jas-Bop
---

## Goal

Replace inline styles with the shared OCS button grammar. Use anchors for navigation, buttons for actions, and the supplied layout containers to group related choices. Each example below is editable in a UI runner. The check-in and mood actions are local demonstrations and do not submit or store personal information.


## Popcorn Hack 1: Base Button Class

Adding `ocs__btn` applies the base button grammar. This remains an anchor because its purpose is to navigate to the resource directory.

{% capture button_challenge0 %}Popcorn Hack 1: Base Button Class{% endcapture %}

{% capture button_code0 %}
outputElement.innerHTML = [
  '<a class="ocs__btn" href="https://www.mygoodbrain.org/resources">Mental Health Resource Directory</a>'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-buttons-hw-0"
   challenge=button_challenge0
   code=button_code0
%}

## Popcorn Hack 2: Modifiers and Button Groups

The check-in action has `pill` and `fill` in addition to the base and accent classes. Both controls are inside `ocs__links`. The journal link uses the supplied resource-directory destination as a placeholder; it does not save a draft. Clicking the check-in button updates its label as a local demonstration.

{% capture button_challenge1 %}Popcorn Hack 2: Modifiers and Button Groups{% endcapture %}

{% capture button_code1 %}
outputElement.innerHTML = [
  '<div class="ocs__links">',
  '  <button type="button" class="ocs__btn accent pill fill" onclick="this.textContent = &quot;Check-In Complete (demo)&quot;">Complete Daily Check-In</button>',
  '  <a class="ocs__btn outline" href="https://www.mygoodbrain.org/resources">Save Draft Journal</a>',
  '</div>'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-buttons-hw-1"
   challenge=button_challenge1
   code=button_code1
%}

## Popcorn Hack 3: Status Tones and Wide Layout

I changed the check-in control from yellow to green, upgraded the group to `ocs__links--wide`, and added `fill` to the red support link. The task says to change a second yellow link, but the supplied starter actually has a yellow check-in button and a red link; I applied the green change to the yellow control that exists.

{% capture button_challenge2 %}Popcorn Hack 3: Status Tones and Wide Layout{% endcapture %}

{% capture button_code2 %}
outputElement.innerHTML = [
  '<div class="ocs__links--wide">',
  '  <button type="button" class="ocs__btn alert-green outline" onclick="this.textContent = &quot;Check-In Complete (demo)&quot;">Complete Check-In</button>',
  '  <a class="ocs__btn alert-red fill" href="https://www.mygoodbrain.org/resources">Get Crisis Support Resources</a>',
  '</div>'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-buttons-hw-2"
   challenge=button_challenge2
   code=button_code2
%}

## Homework Hack 1: Adaptive Resource Toolbar

All three resource categories are navigation links inside one `ocs__links` group. Urgent Support uses red, fill, and pill; Self-Care uses green, fill, and pill; Community uses accent, outline, and pill. I removed the hardcoded colors and inline layout rules. The starter mistakenly put Markdown link syntax inside `href`; each destination is now a plain HTTPS URL. All three use the resource-directory URL provided by the lesson, rather than invented category paths.

{% capture button_challenge3 %}Homework Hack 1: Adaptive Resource Toolbar{% endcapture %}

{% capture button_code3 %}
outputElement.innerHTML = [
  '<div class="ocs__links">',
  '  <a class="ocs__btn alert-red fill pill" href="https://www.mygoodbrain.org/resources">Urgent Support</a>',
  '  <a class="ocs__btn alert-green fill pill" href="https://www.mygoodbrain.org/resources">Self-Care</a>',
  '  <a class="ocs__btn accent outline pill" href="https://www.mygoodbrain.org/resources">Community</a>',
  '</div>'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-buttons-hw-3"
   challenge=button_challenge3
   code=button_code3
%}

## Homework Hack 2: Primary and Secondary Action Priority

The accent-filled mood button is the primary action, the outlined trends link is secondary, and the red outlined resources link signals the alert category. I followed the required alert action rather than the starter label “Mental Health Blog.” These links lead to the supplied resource directory, not a working trends dashboard or a direct hotline. The mood button only changes its label; it does not create a saved journal record.

{% capture button_challenge4 %}Homework Hack 2: Primary and Secondary Action Priority{% endcapture %}

{% capture button_code4 %}
outputElement.innerHTML = [
  '<div class="ocs__links">',
  '  <button type="button" class="ocs__btn accent fill" onclick="this.textContent = &quot;Mood Entry Logged (demo)&quot;">Log Mood Entry</button>',
  '  <a class="ocs__btn outline" href="https://www.mygoodbrain.org/resources">View Weekly Trends</a>',
  '  <a class="ocs__btn alert-red outline" href="https://www.mygoodbrain.org/resources">Crisis Hotline Resources</a>',
  '</div>'
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-buttons-hw-4"
   challenge=button_challenge4
   code=button_code4
%}

## Design choices

The shared base class hides repeated styling details, while modifiers describe shape, emphasis, and status. This is a styling abstraction; a reusable JavaScript function would be a procedural abstraction. Classes alone do not implement branching or save data.

The labels communicate the action as well as color. A filled action has more visual emphasis than an outline. Anchors retain real `href` values, and every action button has `type="button"` so it cannot accidentally submit an enclosing form. The native controls also support keyboard focus and activation.

## Validation

Markup checks confirm that all five examples use only the allowed OCS classes, contain no inline style attributes or custom CSS, and use valid HTTPS resource URLs. The three resource-category class combinations and the homework action hierarchy match the requirements. Notebook cells retain `%%html` and their `UI_RUNNER` comments.

The examples depend on the shared OCS styles already available in the site. No stylesheets, layouts, navigation files, or existing application behavior are changed for this assignment. Browser rendering and keyboard verification remain pending.

## Browser checks before submission

1. Run all five examples and confirm the controls render.
2. Tab through the controls; activate buttons with the keyboard and confirm their demo labels update.
3. Verify each anchor opens the lesson's resource-directory destination.
4. Check narrow and wide widths, theme colors, readable labels, and visible focus states.
5. Confirm the two homework groups show the required filled and outlined priorities.

## Reflection

The original toolbars repeated colors, padding, and border rules. The revised markup states each action's role with a short combination of shared classes. If the site changes its button styles later, these examples can inherit that change without editing each control. The two homework toolbars also separate category tones from primary-versus-secondary emphasis.

