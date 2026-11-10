---
name: motion-feels
description: Website motion in everyday words. People say how an animation should feel ("calm", "premium", "like it's floating", "too jumpy", "feels cheap") and this skill turns it into one of 14 named feels, each an exact speed and easing curve with CSS, GSAP and spring values, so nobody needs to know what an easing curve is. Also covers when not to animate, interface vs showcase speeds, a motion palette per brand, build rules (performance, reduced motion, touch) and a motion review checklist. Use it whenever you build, change, review or discuss motion on a website or web page (transitions, hovers, scroll reveals, page loads, page transitions, loaders, marquees, micro-interactions), whenever someone gives motion feedback ("too fast", "feels off", "smoother", "less bouncy", "more premium"), and whenever a feel name comes up, even if the word "animation" is never said.
license: MIT
---

# Motion feels

Most people can't name an easing curve, but they know exactly how they want something to feel: calm, punchy, expensive, playful. Those words fit dozens of curves, so an AI guesses, and the work turns into rounds of "too fast", "less bouncy". This skill gives the person and you one shared set of names, each tied to exact values. **They speak in feelings; you handle the numbers.**

It's written for websites: marketing, portfolio, content and shop sites. For app or product UI the same feels work; use the fast end of every speed.

Three parts:
- **Feel: how it moves.** A speed plus an easing curve. The 14 feels are below.
- **Effect: what moves.** Mask reveal, parallax, marquee and so on. See `references/feels.md`.
- **Dials** adjust a feel: speed, stop, overshoot, stagger, distance, delay, trigger, intensity.

## Talk in feelings, not in curves

The person may not know any motion terms, and shouldn't need to.

- **Never ask them to choose** an easing, a curve, a bezier or a number of milliseconds. Ask about the feeling, with a picture from everyday life: "Should it land softly, like setting down a glass, or overshoot a little and settle, like a spring?"
- **Describe feels by what they look like**, not how they're made: "starts fast and glides to a stop", not "power4.out".
- **Feel names are an optional shortcut.** Mention one in passing ("I'll call this feel **Luxurious**") so they can reuse it. Never require it, and never correct their words.
- **Numbers go in the code**, plus one short line for whoever builds or reviews it: "For developers: 1.2 s, `cubic-bezier(0.22, 1, 0.36, 1)`." Leave that line out when nobody will build from it, for example when the person is only choosing a direction.
- **The words in this file are for you, not for them.** Dial names and CSS terms stay out of your replies. Say "the little bounce at the end" (overshoot), "one after another" (stagger), "how far it moves" (distance), "how softly it stops" (stop), "how much moves at once" (intensity), "where it grows from" (origin), "for people who turn animations off" (reduced motion).
- **One line of translation, then build.** Don't lecture, and don't hold up the work. The only exception is a word the tables below mark "ask", where one plain question comes first.
- **Seeing beats describing.** When they can't put it into words, offer the demo page (`assets/feels-demo.html`, open it in any browser) or build a quick A/B toggle and let them pick.

## The 14 feels

| Feel | Looks like | Speed | CSS | GSAP |
|---|---|---|---|---|
| **Crisp** | a light switch: instant, clean stop | 150 ms | `cubic-bezier(0.33, 1, 0.68, 1)` | `power2.out` |
| **Snappy** | shoots out and lands firmly | 300 ms | `cubic-bezier(0.16, 1, 0.3, 1)` | `expo.out` |
| **Springy** | quick, a small overshoot, then settles | 600 ms | spring, bounce 0.3 (`linear()` in CSS) | no spring; closest `back.out(1.2)` |
| **Smooth** | a sliding door: soft start, soft stop | 500 ms | `cubic-bezier(0.65, 0, 0.35, 1)` | `power2.inOut` |
| **Gentle** | drifts in and fades to a stop | 700 ms | `cubic-bezier(0.61, 1, 0.88, 1)` | `sine.out` |
| **Luxurious** | quick start, a long slow glide to rest | 1.2 s | `cubic-bezier(0.22, 1, 0.36, 1)` | `power4.out` |
| **Floaty** | a feather: slow and even, no clear start or stop | 2 s | `cubic-bezier(0.37, 0, 0.63, 1)` | `sine.inOut` |
| **Dramatic** | a theatre curtain: builds up, rushes, settles | 1.2 s | `cubic-bezier(0.87, 0, 0.13, 1)` | `expo.inOut` |
| **Wind-up** | a slingshot: pulls back first, overshoots the end | 800 ms | `cubic-bezier(0.68, -0.6, 0.32, 1.6)` | `back.inOut(1.7)` |
| **Pop** | jumps past the end and comes back once | 450 ms | `cubic-bezier(0.34, 1.56, 0.64, 1)` | `back.out(1.7)` |
| **Elastic** | jelly: wobbles a few times, then settles | 1 s | `linear()` from elastic.out | `elastic.out(1, 0.3)` |
| **Bounce** | a ball landing | 900 ms | `linear()` from bounce.out | `bounce.out` |
| **Mechanical** | a conveyor belt: same speed throughout | 1 s | `linear` | `none` |
| **Stepped** | a flipbook: jumps frame by frame | 900 ms | `steps(6)` | `steps(6)` |

A feel keeps its curve at any speed: "Springy at 400 ms" is the Springy shape, just quicker. Springs, elastic and bounce in plain CSS are a `linear()` list sampled from the curve; ready-to-paste values are in `references/feels.md` ("Ready-to-paste code"). Spring "bounce" is the 0–1 value used by SwiftUI and Motion (damping ratio = 1 − bounce).

## How to work

1. **Check the element first:** how often it's seen, and whether it's an interface part or showcase motion ("Before picking a feel" below). This can mean less motion, or none.
2. **Translate** their words into feel + dials + effect, using the tables under "Everyday words" below. If two or three feels fit, ask one plain question (or show an A/B toggle).
3. **Say the plan in one plain line before building**, e.g. "The headline lines glide up and settle slowly as you scroll to them, once (feel: **Luxurious**)." They can redirect before anything is built.
4. **Build** with duration, delay and easing in CSS variables or one config object (`--motion-dur`, `--motion-ease`, `--motion-stagger`), so every adjustment is a one-number change. Follow the "Build rules".
5. **Report** in plain words, with the values for developers. For a change, show before → after: "a bit slower: 1.2 s → 1.8 s". Keep the previous values, so "go back" restores them exactly.
6. **Keep it consistent:** once the site's feels are clear, suggest saving them as its motion palette (below) in the project's design tokens, so every section moves the same way.

## A motion palette for the whole site

A good site uses 2 or 3 feels, not 14: one for interface parts, one for showcase moments, and maybe one accent. When someone can't describe the motion at all, ask for the brand in three words and propose a palette in one line.

| The brand sounds like | Showcase | Interface | Accent |
|---|---|---|---|
| calm, trustworthy, caring (health, finance, legal) | Gentle | Crisp | — |
| premium, editorial (fashion, architecture, hotels) | Luxurious | Crisp | Dramatic for the first load |
| bold, fast, techy (startups, SaaS, sport) | Snappy | Crisp | Pop |
| friendly, playful (kids, food, consumer apps) | Springy | Snappy | Pop or Bounce |
| creative, expressive (studios, portfolios, agencies) | Luxurious or Dramatic | Snappy | Wind-up |
| dreamy, natural (wellness, beauty, meditation) | Floaty for loops, Gentle for content | Crisp | — |
| retro, raw (gaming, music, brutalist) | Stepped | Crisp | Mechanical marquees |

## Before picking a feel

### How often is it seen?

Motion that delights once gets in the way on the tenth time. Match the amount of motion to how often a visitor meets the element.

| How often | Examples | Motion |
|---|---|---|
| On every page, every visit | nav links, header, buttons, footer links, form fields | small and fast: Crisp, or only a colour change. Keyboard focus shows the focus ring at once, with no movement. An entrance on these (a nav sliding in on load) plays on the first page view only. |
| On every click | page transitions | short: 600 ms or less, even when the brand is slow and premium |
| Once per page | hero, section reveals, case study cards, stats counting up | the full feel. Scroll reveals play once, not again each time you scroll back. |
| Once per visit | intro loader, first-load hero moment | room for Dramatic and delight. Run loaders on the first page view only. |

The palette's accent goes on the result, not on the control: an add-to-cart press stays quick (Crisp), and the cart count is what pops.

When someone asks for a slow feel on an every-page element, build the fast version and say in one line how to switch: "Nav links are on every page, so I kept them quick; the slow version is a one-number swap." Don't wait for an answer; it's their call.

### Interface part or showcase?

- **Interface parts:** the visitor is trying to do something. Nav dropdowns, mobile menu, tabs, accordions, modals, tooltips, form feedback, filters. Keep them at **300 ms or less**, whatever the feel; mobile menus and modals can go up to **400 ms**. Exits run at about 75% of the entrance: put the shorter duration on the closed state.
- **Showcase motion:** sets the mood. Hero, section reveals, image reveals, marquees, background loops, the first-load moment. The feel's own speed applies, and long is fine.

### Default by element (when no feeling is given)

The speed here replaces the feel's own speed. Any feedback ("feels cheap", "too bouncy") overrides these defaults.

| Element | Feel | Speed |
|---|---|---|
| buttons, links, toggles, hovers, tooltips | Crisp | 150 ms |
| nav dropdowns, tabs, card hovers | Snappy | 250 ms |
| accordions, FAQs | Smooth | 300 ms |
| mobile menu, modals, drawers, sheets | Springy | 400 ms |
| drag and release | Springy | 600 ms |
| slides, carousels, things moving across the screen | Smooth | 500 ms |
| text and image reveals (fade up 24 px, stagger 60–80 ms) | the palette's showcase feel; with no cue, Snappy | the feel's own |
| page transitions | Smooth | 600 ms |
| hero moment, first load | Dramatic | 1.2 s |
| background loops, ambient shapes | Floaty | 2 s |
| success states, badges | Pop | 450 ms |
| loaders, marquees, scroll-scrubbed motion | Mechanical | as needed |

## Everyday words

Use these to translate. The left column is what people actually say; none of it needs motion knowledge. In a longer conversation, show each translation once, then apply it silently.

### Words → feels

| They say | Read as | Ask when |
|---|---|---|
| premium, expensive, elegant, classy, high-end, luxury, "like a magazine", "slow and confident" | **Luxurious** | — |
| smooth, fluid, buttery, seamless, silky, "glides" | **Smooth** (moving across) or **Gentle** (appearing) | the element doesn't make it obvious: "Glide evenly from start to finish, or arrive softly and fade to a stop?" |
| soft, calm, relaxed, quiet, cozy, warm, "not flashy" | **Gentle** | — |
| subtle, barely there, "don't want people to notice it" | **Crisp** (interface) or **Gentle** (content) | — |
| dreamy, airy, floating, weightless, "like a feather", "like underwater" | **Floaty** | — |
| fast, quick, responsive, instant, clicky, tight, "like a light switch" | **Crisp** (small things) or **Snappy** (bigger things) | size is unclear |
| punchy, energetic, bold, confident, strong, "lands hard", "with attitude" | **Snappy** | — |
| natural, physical, alive, "like a phone app", "like a real object" | **Springy** | — |
| fun, playful, cute, friendly, cheeky, happy | **Pop**, **Springy** or **Elastic** | almost always: "A little hop past the end, a soft springy settle, or a jelly wobble?" |
| bouncy | **Bounce** (lands and bounces) or **Pop / Springy** (overshoots, settles) | always: "Bounce like a ball landing, or overshoot a little and settle?" |
| jelly, wobbly, rubbery, squishy, jiggly | **Elastic** | — |
| cinematic, epic, "like a movie", powerful, heavy, "a wow moment", big reveal | **Dramatic** | — |
| cartoony, "winds up first", "like a slingshot" | **Wind-up** | — |
| robotic, constant, steady, "like a conveyor belt", ticker | **Mechanical** | — |
| retro, choppy, stop-motion, pixel, glitchy, "like an old video game", flipbook | **Stepped** | — |
| modern, cool, nice, clean, "make it pop", "make it look good", "add some animation", "make it alive" | nothing on its own | always: offer the 3 feels that fit the context in plain words, or ask for the brand in three words ("make it pop" may mean the Pop feel, or just "more noticeable") |

### Feedback → dials

| They say | Change |
|---|---|
| too fast, rushed, "blink and you miss it", "I can't see it" | Speed × 1.5 |
| too slow, sluggish, laggy, "takes forever", "I'm waiting for it" | Speed ÷ 1.5. On an interface part, also check the 300 ms limit. |
| abrupt, harsh, jerky, "slams into place", "stops too suddenly" | Stop: softer, one step along `power2.out` → `power3.out` → `power4.out` → `expo.out` (CSS values in `references/feels.md`) |
| mushy, "drags at the end", "crawls", "takes too long to settle" | Stop: firmer (shorter tail), or faster |
| weak, lifeless, "needs more punch", "doesn't land" | Stop firmer + Speed ÷ 1.5, or switch to Snappy |
| too bouncy, "too much", cheesy, childish, "over the top" | Overshoot down one step: Pop `cubic-bezier(0.34, 1.56, 0.64, 1)` → a little `cubic-bezier(0.34, 1.4, 0.64, 1)` → none (Snappy) |
| feels cheap | usually too much movement: Distance down and Overshoot down; if it's slow, Speed ÷ 1.5 |
| jumpy, jittery, "pops in out of nowhere" | it grows from nothing or overshoots: start at `scale(0.95)` (Build rules), Overshoot down one step, Distance down |
| stiff, robotic, dead, "needs more life" | Overshoot up one step, or switch to Springy |
| flat, boring, "nothing happens", "I don't notice it" | Stagger up, or Distance up |
| busy, distracting, "too much going on", annoying | Intensity down, Stagger down. Annoying often means it's seen too often: check "How often is it seen?" |
| "makes me dizzy", "makes me feel sick" | remove parallax, big scaling and long-distance moves; check the reduced-motion fallback |
| starts too late / too early | Delay down / up in 100 ms steps |
| feels off, "not quite", "I don't know what's wrong" | don't guess: ask "Is it the speed, the way it starts, the way it stops, or the little bounce at the end?", or show two versions side by side |

## Build rules

- **Move with `transform`, fade with `opacity`.** Don't animate `width`, `height`, `top`, `left` or `margin`; they stutter while scrolling. For accordions, `grid-template-rows: 0fr → 1fr` is the accepted exception (the content sits in an inner wrapper with `min-height: 0; overflow: hidden`). Never `transition: all`; name the properties.
- **Never grow from nothing.** Start scale-ins at `scale(0.95)` with `opacity: 0` (0.9 for bigger pops), never `scale(0)`.
- **Grow from the trigger.** Dropdowns, popovers and tooltips set `transform-origin` towards their button. Modals grow from the centre.
- **Nothing that appears uses an ease-in-only curve.** A slow start reads as lag. Ease-in is for things leaving. Wind-up and Dramatic are fine, because they end with a soft stop.
- **Hover only where there's a mouse.** Wrap hover motion in `@media (hover: hover) and (pointer: fine)`, so phones don't get stuck hover states.
- **Hovers and toggles use CSS transitions, not keyframes**, so moving the mouse out halfway reverses smoothly instead of jumping.
- **Reduced motion means gentler, not zero.** Under `prefers-reduced-motion: reduce`, keep fades and colour changes, and remove movement, scaling, parallax and auto-playing loops (marquees stop).
- **Content never depends on the animation.** If the script doesn't run, nothing stays hidden at `opacity: 0`: set the hidden start state from the script, or under a `.js` class.
- **Scroll reveals play once:** an IntersectionObserver adds the class, then stops watching that element. The snippet is in `references/feels.md` ("Ready-to-paste code").

## Reviewing motion

When asked to review, check or audit motion, or before handing a site to developers, go through this list. Write each problem in plain words, mark it **Fix** (it breaks the feel, accessibility or performance) or **Consider** (it would be better), and add the change in values for developers.

1. **Reason:** it guides the eye, shows a change, gives feedback or sets the mood. If none of these, remove it.
2. **How often:** it matches "How often is it seen?". Every-page elements are quick and small.
3. **Speed:** interface parts are 300 ms or less (mobile menus and modals 400 ms); exits are faster than entrances.
4. **Feel:** it matches the brief, and the same kind of element moves the same way across the site.
5. **Start and origin:** no `scale(0)`; popovers grow from their trigger.
6. **Interruptions:** hovering out halfway reverses smoothly; fast clicks don't stack up animations.
7. **Performance:** only `transform` and `opacity` (plus the accordion exception); smooth while scrolling on a phone.
8. **Reduced motion:** there's a fallback, and it keeps the fades.
9. **Touch:** hover motion is limited to mouse devices; nothing important hides behind a hover.
10. **Content:** reveals play once, and nothing stays hidden if the script fails.

Always **Fix**: `scale(0)`, ease-in on something appearing, slow motion on every-page or keyboard actions, no reduced-motion fallback, animated layout properties when `transform` would do, `transition: all`, and hover motion built with keyframes or without the mouse-only media query.

## Files

- `references/feels.md`: the full vocabulary, with words, uses, every dial's values and 14 effect recipes (mask reveal, parallax, marquee, kinetic type, magnetic cursor and more), each with its usual feel. Read it for dial values, effects, or anything beyond the tables above.
- `assets/feels-demo.html`: all 14 feels side by side, with each curve plotted and a slow-motion switch. Opens in any browser, no install. `assets/effects-demo.html` shows the effect recipes. If the environment can show an HTML page (a preview or an artifact), show it there.

The "how often", speed, build rules and review checklist are adapted for websites from Emil Kowalski's skills (MIT): https://github.com/emilkowalski/skills
