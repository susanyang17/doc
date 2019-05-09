---
title: "Form Controls"
---

# Customize Form Control Style
Each form control is an HTML element that has its own CSS class, so you can customize their style by overriding rules of their CSS class e.g. `.k-ctrl-button`

## For a specific button
Keikai also generates an extra CSS class upon a button's name in lower case for a button. For example, if a button's name is `submit`, keikai will generate a CSS class, `submit`, on the button. So that you can customize through that specific CSS class:

```css
.submit{
    color: blue;
}
```
