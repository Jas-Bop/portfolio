---
layout: post
title: SASS Toggles HW
codemirror: true
categories: [SASS]
lesson_language: SASS
lesson_topic: Toggles HW
lesson_part: interactive
lesson_type: lesson
permalink: /sass/toggles-hw/
author: Jas-Bop
---

## Popcorn: Understanding the parts

1. The **checkbox input** stores whether the toggle is on or off.
2. The **track (slider)** is the visible part that changes appearance.
3. The question about `.switch` cannot be answered exactly from the paste because that selector's definition is missing. In the OCS version, `ocs__toggle` is the wrapper for the input, track, and label.
4. **`border-radius`** makes the track rounded.
5. **`::before`** is a pseudo-element, not a class. It creates the moving knob and can define its shape and appearance.

The input owns the checked state; the track displays that state. JavaScript reads `.checked` as a Boolean.


## Popcorn Hack: Fix the Missing Track

I added `ocs__toggle-track` to the missing span and kept it decorative with `aria-hidden="true"`. The visible label names the native checkbox, and the live output now reports the notification setting. This example changes local UI text; it does not request browser notification permission.

{% capture toggle_challenge0 %}Popcorn Hack: Fix the Missing Track{% endcapture %}

{% capture toggle_code0 %}
outputElement.innerHTML = [
  '<label class="ocs__toggle ocs__toggle--green">',
  '  <input id="toggle-popcorn-notifications" class="ocs__toggle-input" type="checkbox">',
  '  <span class="ocs__toggle-track" aria-hidden="true"></span>',
  '  <span class="ocs__toggle-label">Enable Notifications</span>',
  '</label>',
  '<output id="toggle-popcorn-status" for="toggle-popcorn-notifications" aria-live="polite">Notifications: off</output>'
].join("");

// The missing class belongs on the visible track; the checkbox stores the state.
const notifications = outputElement.querySelector('#toggle-popcorn-notifications');
const notificationStatus = outputElement.querySelector('#toggle-popcorn-status');
function updateNotifications() {
  notificationStatus.textContent = notifications.checked ? 'Notifications: on' : 'Notifications: off';
}
notifications.addEventListener('change', updateNotifications);
updateNotifications();
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-toggles-hw-0"
   challenge=toggle_challenge0
   code=toggle_code0
%}

## Homework: Interactive Study Settings

My three toggles independently control study tips, a worked example, and study reminders. They all use the OCS toggle grammar and have distinct labels, IDs, and controlled sections. Tips start enabled; the other two start disabled. Every change updates both visibility and the enabled count. Settings reset when the runner is run again.

{% capture toggle_challenge1 %}Homework: Interactive Study Settings{% endcapture %}

{% capture toggle_code1 %}
outputElement.innerHTML = [
  '<section aria-labelledby="study-toggle-title">',
  '  <h2 id="study-toggle-title">Customize Your Study Panel</h2>',
  '  <label class="ocs__toggle ocs__toggle--green">',
  '    <input id="study-toggle-tips" class="ocs__toggle-input" type="checkbox" aria-controls="study-tips-panel" checked>',
  '    <span class="ocs__toggle-track" aria-hidden="true"></span>',
  '    <span class="ocs__toggle-label">Show study tips</span>',
  '  </label>',
  '  <label class="ocs__toggle ocs__toggle--green">',
  '    <input id="study-toggle-steps" class="ocs__toggle-input" type="checkbox" aria-controls="study-steps-panel">',
  '    <span class="ocs__toggle-track" aria-hidden="true"></span>',
  '    <span class="ocs__toggle-label">Show worked steps</span>',
  '  </label>',
  '  <label class="ocs__toggle ocs__toggle--green">',
  '    <input id="study-toggle-reminders" class="ocs__toggle-input" type="checkbox" aria-controls="study-reminders-panel">',
  '    <span class="ocs__toggle-track" aria-hidden="true"></span>',
  '    <span class="ocs__toggle-label">Show study reminders</span>',
  '  </label>',
  '  <p><output id="study-toggle-count" for="study-toggle-tips study-toggle-steps study-toggle-reminders" aria-live="polite" aria-atomic="true">1 of 3 toggles on</output></p>',
  '  <section id="study-tips-panel" aria-labelledby="study-tips-heading">',
  '    <h3 id="study-tips-heading">Study tips</h3>',
  '    <p>Predict the output before running a program, then compare the actual result.</p>',
  '  </section>',
  '  <section id="study-steps-panel" aria-labelledby="study-steps-heading" hidden>',
  '    <h3 id="study-steps-heading">Worked steps: total a list</h3>',
  '    <ol>',
  '      <li>Start total at 0.</li>',
  '      <li>For each number in [4, 6, 8], add that number to total.</li>',
  '      <li>The running totals are 4, 10, and 18.</li>',
  '    </ol>',
  '  </section>',
  '  <section id="study-reminders-panel" aria-labelledby="study-reminders-heading" hidden>',
  '    <h3 id="study-reminders-heading">Study reminders</h3>',
  '    <p>Test a normal input, an empty input, and a boundary case before submitting.</p>',
  '  </section>',
  '</section>'
].join("");

// Each toggle controls a different real section inside this runner output.
const settings = [
  ['#study-toggle-tips', '#study-tips-panel'],
  ['#study-toggle-steps', '#study-steps-panel'],
  ['#study-toggle-reminders', '#study-reminders-panel']
].map(([inputSelector, panelSelector]) => ({
  input: outputElement.querySelector(inputSelector),
  panel: outputElement.querySelector(panelSelector)
}));
const count = outputElement.querySelector('#study-toggle-count');

function updateStudyPanel() {
  let enabledCount = 0;
  for (const setting of settings) {
    // .checked is a Boolean; .value would not tell me whether the checkbox is on.
    const enabled = setting.input.checked;
    // Negation hides a panel when its corresponding checkbox is off.
    setting.panel.hidden = !enabled;
    if (enabled) enabledCount += 1;
  }
  // Recalculate from current states, avoiding a counter that drifts after repeated changes.
  count.textContent = enabledCount + ' of ' + settings.length + ' toggles on';
}

for (const setting of settings) {
  setting.input.addEventListener('change', updateStudyPanel);
}
// Initialize immediately so prechecked inputs, visible panels, and the count agree before any click.
updateStudyPanel();
{% endcapture %}

{% include runners/ui.html
   runner_id="sass-toggles-hw-1"
   challenge=toggle_challenge1
   code=toggle_code1
%}

## How the logic works

Each input supplies a Boolean condition. Selection decides whether to count it, and Boolean negation sets the matching section's `hidden` state. Iteration applies the same logic to all three settings. The `settings` collection pairs each control with its target instead of maintaining three separate change handlers.

The track is decorative, while the nested checkbox supplies the accessible control and keyboard behavior. `aria-controls` identifies each controlled section. The count is an `output` with polite live announcements, so it can report changes without moving focus.

## Test cases

| Toggle state (tips, steps, reminders) | Expected count | Expected visible sections |
| --- | --- | --- |
| On, off, off (initial) | 1 of 3 | Tips |
| Off, off, off | 0 of 3 | None |
| Off, on, off | 1 of 3 | Worked steps |
| Off, off, on | 1 of 3 | Reminders |
| On, on, off | 2 of 3 | Tips and worked steps |
| On, off, on | 2 of 3 | Tips and reminders |
| Off, on, on | 2 of 3 | Worked steps and reminders |
| On, on, on | 3 of 3 | All three |

Browser checks still needed: press Run, activate each switch with mouse and keyboard, confirm the corresponding section changes, and check narrow and wide layouts. The examples rely on the site's shared toggle styling. No stylesheet or application files are changed for this homework.

## Reflection

A toggle should control a visible feature rather than only change color. I connected each switch to a different section and recalculated the total from actual checked states. Calling the update function on startup also prevents the first render from contradicting a prechecked input. The code includes comments explaining Boolean state, negation, counting, and initialization.

