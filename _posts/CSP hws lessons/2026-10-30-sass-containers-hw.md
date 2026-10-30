---
layout: post
title: SASS Containers HW
codemirror: true
categories: [SASS]
lesson_language: SASS
lesson_topic: Containers HW
lesson_part: interactive
lesson_type: lesson
permalink: /sass/containers-hw/
author: Jas-Bop
---

## Goal

Rebuild the Poway Scripps Rotary Parade invite and hub using only OCS container grammar. Each runner is a separate example with exactly one container and one card. All content belongs inside that card, with no inline styles or made-up classes.

The schedule and statuses below are sample content from the exercise, not a verified announcement of an upcoming event.


## Popcorn Hack: Parade Invite Rescue

The outer `page-wrap` becomes `ocs__container`, and one card groups the title, my own description, and the schedule. Three `ocs__grid-cell` elements replace the flex row and `box` classes. I accented the start time so visitors can quickly find when to arrive. The shared standard grid handles the responsive layout.

{% capture container_challenge0 %}Popcorn Hack: Parade Invite Rescue{% endcapture %}

{% capture container_code0 %}
outputElement.innerHTML = [
  "<div class=\"ocs__container\">",
  "  <div class=\"ocs__card\">",
  "    <h2 class=\"ocs__section-title\">Poway Rotary Parade Invite</h2>",
  "    <p class=\"ocs__description\">Celebrate local service and community spirit with the Poway Scripps Rotary Club.</p>",
  "    <div class=\"ocs__grid ocs__grid--standard cols-3\">",
  "      <div class=\"ocs__grid-cell\">Location: Poway Road</div>",
  "      <div class=\"ocs__grid-cell ocs__grid-cell--accent\">Start time: 9:00 AM</div>",
  "      <div class=\"ocs__grid-cell\">What you get: Local culture, community connections, and a chance to support service projects.</div>",
  "    </div>",
  "  </div>",
  "</div>"
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-containers-hw-0"
   challenge=container_challenge0
   code=container_code0
%}

## Homework Hack: Parade Hub Page

The header cell labels the whole grid. The accented cell emphasizes arrival time, the regular cell gives the location, and the muted cell supplies a secondary volunteer reminder. The table wrapper groups the activity/status table, which has a header row and exactly two body rows. The final callout gives visitors a clear takeaway.

{% capture container_challenge1 %}Homework Hack: Parade Hub Page{% endcapture %}

{% capture container_code1 %}
outputElement.innerHTML = [
  "<div class=\"ocs__container\">",
  "  <div class=\"ocs__card\">",
  "    <h2 class=\"ocs__section-title\">Poway Scripps Rotary Parade Hub</h2>",
  "    <p class=\"ocs__description\">Find parade details, explore community activities, and plan how to help your neighbors.</p>",
  "    <div class=\"ocs__grid ocs__grid--standard cols-3\">",
  "      <div class=\"ocs__grid-cell ocs__grid-cell--header\">Parade Day Overview</div>",
  "      <div class=\"ocs__grid-cell ocs__grid-cell--accent\">Start time: 9:00 AM \u2014 plan to arrive before the parade begins.</div>",
  "      <div class=\"ocs__grid-cell\">Location: Poway Road \u2014 meet local groups and enjoy community floats.</div>",
  "      <div class=\"ocs__grid-cell ocs__grid-cell--muted\">Volunteer reminder: Check your assigned role with the event coordinator.</div>",
  "    </div>",
  "    <div class=\"ocs__table-wrap\">",
  "      <table class=\"ocs__table\">",
  "        <thead>",
  "          <tr><th scope=\"col\">Activity</th><th scope=\"col\">Sample status</th></tr>",
  "        </thead>",
  "        <tbody>",
  "          <tr><td>Parade float entries</td><td>Registration open</td></tr>",
  "          <tr><td>Community food drive</td><td>Collecting donations</td></tr>",
  "        </tbody>",
  "      </table>",
  "    </div>",
  "    <div class=\"ocs__callout\">One community, many ways to serve: join the parade, volunteer, or support the food drive.</div>",
  "  </div>",
  "</div>"
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-containers-hw-1"
   challenge=container_challenge1
   code=container_code1
%}

## Design thinking

**Empathize:** A visitor needs to locate the parade's time and place quickly, including while reading on a phone. A volunteer also needs secondary reminders without losing the main event details.

**Define:** Keep the hub inside one readable boundary, group related information in one card, and distinguish the schedule, activity statuses, and final takeaway.

**Ideate:** Use the standard grid for short event details and a table for repeated activity/status pairs. Give the most urgent schedule information an accent and keep the volunteer reminder muted.

**Prototype:** Replace the broken wrapper and tile classes with the shared container, card, grid, table, and callout grammar. Use semantic headings and scoped table headers.

**Test and revise:** Check the markup against the required structure first. Next, run both examples in the browser at wide and narrow widths; look for clipped text, horizontal page overflow, and an unreadable table. Browser verification is still pending, so no phone or desktop visual pass is claimed.

## Why the container matters

The container sets the outer page boundary. A card groups related content inside that boundary; the grid and table organize different kinds of content inside the card. Shared styles provide consistent spacing and theme preferences. Reusing a class is a styling abstraction, while procedural abstraction specifically involves reusable procedures.

## Validation

The completed markup has no `style` attributes, embedded stylesheets, legacy `border` attributes, or invented classes. Each example has one container and one card. The homework has one standard `cols-3` grid, header/accent/muted cells, a wrapped table with two body rows, and one final callout.

The optional SCSS variant is omitted so the submission stays within the required OCS grammar. No site stylesheet, layout, or shared component is changed for this homework. The local checkout may lack some of the lesson's shared OCS styles; the markup relies on that styling being available in the lesson/site environment.

## Browser checks before submission

1. Press Run on each example and confirm that its content appears.
2. At a wide width, verify that the invite has three schedule columns and the hub header spans its grid.
3. At a narrow width, check that the site's shared grid rules reduce columns and keep the text readable.
4. Confirm the table's two activity rows remain readable without overflowing the page.
5. Change the site's theme preferences and check that shared OCS elements follow them.

These browser checks have not been performed in this session.

