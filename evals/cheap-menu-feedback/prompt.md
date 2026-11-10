---
tags: [motion-feels]
max_turns: 12
timeout_seconds: 600
allowed_tools: [Read, Glob, Grep, Skill]
---

the mobile menu on my site feels cheap and kind of jumpy, can you make it nicer? here's the css:

```css
.mobile-menu { transform: scale(0); opacity: 0; transition: all .8s cubic-bezier(.34,1.56,.64,1); }
.mobile-menu.open { transform: scale(1); opacity: 1; }
```
