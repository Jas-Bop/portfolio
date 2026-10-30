---
layout: post
title: CSS to Sass Refactor Homework
author: Jas-Bop
categories: [SASS]
permalink: /homework/sass-refactor/
---

## Goal

Convert an existing CSS file to SCSS, connect it to the site's shared stylesheet, and remove the old CSS file and its link. I chose the profile page's Save-button shake animation because it is a small component whose compiled behavior can be compared directly with the original.

## Original CSS

The original file was `assets/css/Aesthetihawk/shake.css`. It defined five animation positions and a class that played the animation for `0.3s`:

```css
@keyframes shake {
    0% { transform: translateX(0); }
    25% { transform: translateX(-15px); }
    50% { transform: translateX(15px); }
    75% { transform: translateX(-15px); }
    100% { transform: translateX(0); }
}

.shake-animation {
    animation: shake 0.3s ease-in-out;
}
```

`_layouts/profile.html` loaded it with a separate stylesheet link. That link used lowercase `aesthetihawk`, while the source folder was named `Aesthetihawk`, which can prevent loading on a case-sensitive host.

## Converted SCSS

The new file is `_sass/open-coding/profile-shake.scss`:

```scss
@import "materials/main.scss";

$profile-shake-distance: 15px;
$profile-shake-duration: 0.3s;

@keyframes shake {
    0% { transform: translateX(0); }
    25% { transform: translateX(-$profile-shake-distance); }
    50% { transform: translateX($profile-shake-distance); }
    75% { transform: translateX(-$profile-shake-distance); }
    100% { transform: translateX(0); }
}

.shake-animation {
    animation: shake $profile-shake-duration ease-in-out;
}
```

The distance variable controls all three moving positions. Unary negation produces the leftward movement from the same value. The duration variable controls the animation speed. Changing the distance to `10px` would produce positions of `-10px` and `10px` without editing each keyframe.

The materials import follows the lesson's shared-utilities convention. This animation has no color properties, so it does not need a palette variable. Its keyframes and single class also do not need nested selectors or a mixin; those would be useful for a component with related child selectors or repeated groups of declarations.

## Registration and cleanup

I added this import at the end of the imports in `_sass/open-coding/_main.scss`:

```scss
@import "profile-shake";
```

The component now enters the shared import chain:

```text
_sass/minima/custom-styles.scss
  → open-coding/_main.scss
    → profile-shake.scss
      → materials/_main.scss
```

I removed the original `assets/css/Aesthetihawk/shake.css` file and its stylesheet link from `_layouts/profile.html`. The parent `aesthetihawk` layout already links the shared `/assets/css/style.css` stylesheet.

## Validation

I compiled the component with the locally installed Sass compiler:

```sh
sass --scss --style expanded --load-path _sass \
  _sass/open-coding/profile-shake.scss /tmp/portfolio-profile-shake.css
```

Compilation passed. Comparing the compiled animation rules with the original CSS, ignoring comments and whitespace, confirmed that the keyframe positions, animation name, duration, and easing stayed the same. I also checked that the new import exists and that the old CSS file and profile link are gone.

I attempted a full site build:

```sh
bundle exec jekyll build --destination /tmp/portfolio-sass-hw-site
```

The build could not start because the local Ruby bundle is missing the `csv` gem. Full site compilation and browser verification remain pending. After resolving the bundle, the browser check is to open the profile page, confirm the shared stylesheet contains the animation, and temporarily apply `shake-animation` to the Save button to verify the motion.

## Reflection

SCSS keeps this animation's settings in one place while compiling to the same CSS rules. Registering the component in the shared import hub removes the separate stylesheet request and its case-sensitive path issue. For larger components, I would also use shallow nesting for related selectors, shared palette variables for colors, and mixins for declarations reused across components.
