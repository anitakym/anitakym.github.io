---
title: highlight-practice
date: 2023-11-14 10:53:18
tags:
---
### IntersectionObserver
```
mark {
  animation-name: highlight;
  animation-timeline: view();
}
@​keyframes highlight { to { --light: 1; }}
mark span {
  background-position: calc((1 - var(--light)) * 110%) 0;
  transition: background 1s;
}
```
The "trick" is to animate a custom property with a scroll-driven animation. These will flip in a binary fashion if not using @​property. And that's what you want.

You can then use that value to set the style on the highlights (<mark>). What you see is the transition of a background-position to get the multi-line highlight. A technique posted on this account before 🤙

Added bonuses:
– Could use another element for the author initials of a highlight and animate that in too. Here the pseudoelement is being used. But another accessible span would do the trick.
– Highlight color is scoped inline via hue.
– View transition theme switch for a bonus that looks like a triangle. Been messing with Vercel docs so was the easiest thing to go with 