---
layout: post
title: SASS Grids HW
codemirror: true
categories: [SASS]
lesson_language: SASS
lesson_topic: Grids HW
lesson_part: interactive
lesson_type: lesson
permalink: /sass/grids-hw/
author: Jas-Bop
---

## Goal

Use the OCS grid grammar to organize lab readings and a keypad. Each grid has one variant, and every direct child has `ocs__grid-cell`. The homework markup uses no custom classes, CSS, or inline styles; only Popcorn 2 uses the lesson's allowed `fr` experiment.


## Popcorn Hack 1: Fix the Beaker Row

The three beakers now use one standard grid and three cells. The inline flex layout and `box` class are removed. On a wide screen there are three equal columns; the shared small-screen rule reduces the standard grid to two columns.

{% capture grid_challenge0 %}Popcorn Hack 1: Fix the Beaker Row{% endcapture %}

{% capture grid_code0 %}
outputElement.innerHTML = [
  "<div class=\"ocs__grid ocs__grid--standard\">",
  "  <div class=\"ocs__grid-cell\">Beaker A: Water</div>",
  "  <div class=\"ocs__grid-cell\">Beaker B: Salt Water</div>",
  "  <div class=\"ocs__grid-cell\">Beaker C: Vinegar</div>",
  "</div>"
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-grids-hw-0"
   challenge=grid_challenge0
   code=grid_code0
%}

## Popcorn Hack 2: Size the Beakers with fr

I used `1fr 1fr 1fr 2fr`: four track values create four columns. The Control Beaker receives two of the five shares of available track space, while each other beaker receives one. Gaps are separate from these shares. This inline style is used only for the permitted fraction experiment; it deliberately keeps all four columns in one row.

{% capture grid_challenge1 %}Popcorn Hack 2: Size the Beakers with fr{% endcapture %}

{% capture grid_code1 %}
outputElement.innerHTML = [
  "<div class=\"ocs__grid ocs__grid--standard\" style=\"grid-template-columns: 1fr 1fr 1fr 2fr;\">",
  "  <div class=\"ocs__grid-cell\">Beaker 1</div>",
  "  <div class=\"ocs__grid-cell\">Beaker 2</div>",
  "  <div class=\"ocs__grid-cell\">Beaker 3</div>",
  "  <div class=\"ocs__grid-cell\">Control Beaker</div>",
  "</div>"
].join("");
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-grids-hw-1"
   challenge=grid_challenge1
   code=grid_code1
%}

## Homework Hack: Temperature Trial and Keypad

Grid 1 uses the standard variant for readings. Its header spans the full row, and Beaker 3 is accented because 31.6 °C is the outlier. Grid 2 uses the calculator variant for four square keypad cells, with Avg accented. The keypad demonstrates layout only; averaging behavior is outside this task. Press Run to render the grids and recompute the PASS/FIX checklist after edits.

{% capture grid_challenge2 %}Homework Hack: Temperature Trial and Keypad{% endcapture %}

{% capture grid_code2 %}
outputElement.innerHTML = [
  "<div class=\"ocs__grid ocs__grid--standard\">",
  "  <div class=\"ocs__grid-cell ocs__grid-cell--header\">Temperature Trial (\u00b0C)</div>",
  "  <div class=\"ocs__grid-cell\">Beaker 1: 22.4</div>",
  "  <div class=\"ocs__grid-cell\">Beaker 2: 22.9</div>",
  "  <div class=\"ocs__grid-cell ocs__grid-cell--accent\">Beaker 3: 31.6</div>",
  "</div>",
  "<div class=\"ocs__grid ocs__grid--calculator\">",
  "  <div class=\"ocs__grid-cell\">7</div>",
  "  <div class=\"ocs__grid-cell\">8</div>",
  "  <div class=\"ocs__grid-cell\">9</div>",
  "  <div class=\"ocs__grid-cell ocs__grid-cell--accent\">Avg</div>",
  "</div>"
].join("");

const grids = [...outputElement.querySelectorAll('.ocs__grid')];
const cells = [...outputElement.querySelectorAll('.ocs__grid > div')];
const allowed = new Set(['ocs__grid', 'ocs__grid--standard', 'ocs__grid--calculator',
  'ocs__grid-cell', 'ocs__grid-cell--header', 'ocs__grid-cell--accent']);
const all = [...outputElement.querySelectorAll('*')];
const checks = [
  ['No inline style attributes', !outputElement.querySelector('[style]')],
  ['No made up classes', all.every(el => [...el.classList].every(c => allowed.has(c)))],
  ['Has exactly two ocs__grid roots', grids.length === 2],
  ['Exactly one variant on each grid', grids.length === 2 && grids.every(el =>
    [...el.classList].filter(c => c.startsWith('ocs__grid--')).length === 1)],
  ['Uses the standard variant for Grid 1', !!grids[0]?.classList.contains('ocs__grid--standard')],
  ['Uses the calculator variant for Grid 2', !!grids[1]?.classList.contains('ocs__grid--calculator')],
  ['Every box uses ocs__grid-cell', cells.length === 8 && cells.every(el => el.classList.contains('ocs__grid-cell'))],
  ['Title is a header cell', !!grids[0]?.firstElementChild?.classList.contains('ocs__grid-cell--header')],
  ['Outlier beaker and Avg key are accent cells', !!grids[0]?.lastElementChild?.classList.contains('ocs__grid-cell--accent') &&
    !!grids[1]?.lastElementChild?.classList.contains('ocs__grid-cell--accent')]
];
const report = document.createElement('ul');
report.setAttribute('aria-label', 'Homework validation results');
for (const [label, passed] of checks) {
  const item = document.createElement('li');
  item.textContent = (passed ? 'PASS ' : 'FIX ') + label;
  report.appendChild(item);
}
outputElement.prepend(report);
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-grids-hw-2"
   challenge=grid_challenge2
   code=grid_code2
%}

## MCQ

Question 1: **A — `cols-4`** adds four columns to a standard grid. The calculator class selects a different variant, `--wide` changes one cell's span, and `4fr` describes one track rather than four.

MCQ Grids: pending — only question 1 was included in the supplied lesson text. Questions 2–4 and a genuine score line still need to be completed in the lesson's quiz.


## Validation and reflection

Structural checks confirm three cells in Popcorn 1, four fraction values in Popcorn 2, and two homework grids with the required header and accent cells. The runner's checklist checks the homework markup on every run. Browser rendering and the lesson MCQ submission remain pending.

This checkout does not contain the lesson's full OCS grid definitions. These examples rely on the shared lesson styles being available; no site stylesheets are modified for this homework. The student markup contains no custom CSS.

A variant describes the whole layout, while a cell modifier describes an individual item's role. This makes the outlier and title clear without writing individual widths. Choosing the variant first also makes it easier to explain why the readings use rows and the keypad uses square cells.

## Submission notes

Lesson: OCS Grid Grammar (SASS Grids)  
MCQ Grids: pending questions 2–4 and quiz result  
Popcorn 1: three beakers refactored to ocs__grid — yes  
Popcorn 2: fr values used = 1fr 1fr 1fr 2fr  
Homework: structural checks pass; run the browser checklist and confirm rendered layout before submission.

