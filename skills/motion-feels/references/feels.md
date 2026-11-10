# Motion feels: full vocabulary

Two layers, plus dials:
1. **Feel: how it moves.** A speed plus an easing curve. 14 feels.
2. **Effect: what moves.** Mask reveals, parallax, marquees and so on. 14 recipes, each with the feel it usually uses.

Values go into CSS variables or one config object, so "a bit slower" changes one number. Live demos: `../assets/feels-demo.html` and `../assets/effects-demo.html`. If you change a value here, change it in the demo's FEELS list too.

---

## How to describe what you want

No motion words needed. Five plain answers are enough:

```
Feel:     slow and expensive        (or a feel name: "Luxurious, but a bit slower")
Effect:   headline lines slide up one by one
When:     as you scroll to it
What:     the headline, then the photo
Avoid:    any bounce
```

Everyday words and feedback map to feels and dials in the tables in `SKILL.md` ("Everyday words").

---

## Feels: how it moves

A feel is a speed plus a curve. The same curve at another speed is another feel: `expo.out` at 300 ms is Snappy; a similar long-tail curve at 1.2 s is Luxurious.

### Quick and responsive
| Feel | Speed | Curve shape | CSS · GSAP | Say | Use for |
|---|---|---|---|---|---|
| **Crisp** | 150 ms | fast start, quick soft stop | `cubic-bezier(0.33, 1, 0.68, 1)` · `power2.out` | instant, crisp, responsive, tight | buttons, toggles, hovers |
| **Snappy** | 300 ms | shoots out, settles fast | `cubic-bezier(0.16, 1, 0.3, 1)` · `expo.out` | snappy, quick, decisive, punchy | menus, cards, bold entrances |
| **Springy** | 600 ms | quick, a small overshoot, settles | spring with bounce 0.3 over 0.6 s (damping ratio 0.7, about 5% overshoot), or CSS `linear()` · no GSAP spring, closest `back.out(1.2)` | springy, lively, physical, iOS-like | drawers, sheets, drag and release |

### Smooth and calm
| Feel | Speed | Curve shape | CSS · GSAP | Say | Use for |
|---|---|---|---|---|---|
| **Smooth** | 500 ms | soft start, soft stop, even | `cubic-bezier(0.65, 0, 0.35, 1)` · `power2.inOut` | smooth, fluid, polished, even | moving things across the screen, slides |
| **Gentle** | 700 ms | easy start, speed fades out slowly | `cubic-bezier(0.61, 1, 0.88, 1)` · `sine.out` | gentle, soft, calm, relaxed | fades, captions, calm brands |
| **Luxurious** | 1.2 s | quick start, very long slow settle | `cubic-bezier(0.22, 1, 0.36, 1)` · `power4.out` | luxurious, silky, elegant, unhurried | editorial reveals, hero images, fashion |
| **Floaty** | 2 s | slow and even, no clear start or stop | `cubic-bezier(0.37, 0, 0.63, 1)` · `sine.inOut` | floaty, dreamy, weightless, drifting | background loops, ambient shapes |

### Big moments
| Feel | Speed | Curve shape | CSS · GSAP | Say | Use for |
|---|---|---|---|---|---|
| **Dramatic** | 1.2 s | long wind-up, rush through the middle, long settle | `cubic-bezier(0.87, 0, 0.13, 1)` · `expo.inOut` | dramatic, powerful, cinematic, bold | hero moments, first load, full-screen wipes (page transitions on every click stay at 600 ms or less) |
| **Wind-up** | 800 ms | pulls back first, overshoots the end | `cubic-bezier(0.68, -0.6, 0.32, 1.6)` · `back.inOut(1.7)` | anticipation, wind-up, cartoony | playful transitions, attention moments |

### Playful and physical
| Feel | Speed | Curve shape | CSS · GSAP | Say | Use for |
|---|---|---|---|---|---|
| **Pop** | 450 ms | shoots past the end, comes back once | `cubic-bezier(0.34, 1.56, 0.64, 1)` · `back.out(1.7)` | pop, cheeky, energetic, overshoot | badges, icons, success states |
| **Elastic** | 1 s | wobbles several times, then settles | CSS `linear()` · `elastic.out(1, 0.3)` | elastic, jelly, wobbly, rubbery | toys, games; one element at a time |
| **Bounce** | 900 ms | drops and bounces like a ball | CSS `linear()` · `bounce.out` | bouncy, gravity, dropped, cartoon | things landing: icons, dropped cards |

### Mechanical
| Feel | Speed | Curve shape | CSS · GSAP | Say | Use for |
|---|---|---|---|---|---|
| **Mechanical** | 1 s | the same speed from start to end | `linear` · `none` | mechanical, robotic, constant, steady | marquees, loaders, scroll-scrubbed motion |
| **Stepped** | 900 ms | jumps in 6 frames, nothing in between | `steps(6)` · `steps(6)` | stepped, choppy, retro, stop-motion | pixel art, counters, typewriters, glitch |

CSS `linear()` is how CSS does springs, elastic and bounce: a list of points sampled from the curve. The demo page builds them from the GSAP formulas.

---

## The dials

Adjust any feel with these. Name the feel first, then the dial: "Luxurious, but a softer stop".

| Dial | Options and the values behind them |
|---|---|
| **Speed** | faster or slower than the feel's speed: about 1.5× per step ("a bit slower" = 1.5× longer) |
| **Stop** | softer stop = longer tail, one step at a time: `power2.out` `cubic-bezier(0.33, 1, 0.68, 1)` → `power3.out` `cubic-bezier(0.25, 1, 0.5, 1)` → `power4.out` `cubic-bezier(0.22, 1, 0.36, 1)` → `expo.out` `cubic-bezier(0.16, 1, 0.3, 1)` · firmer stop: the other way. Already at `expo.out` and still abrupt? Slow it down instead. |
| **Overshoot** | none: `expo.out` `cubic-bezier(0.16, 1, 0.3, 1)` · a little (about 5%): `back.out(1.2)` `cubic-bezier(0.34, 1.4, 0.64, 1)`, spring bounce 0.3 · medium (about 10%, Pop): `back.out(1.7)` `cubic-bezier(0.34, 1.56, 0.64, 1)`, spring bounce 0.4 · a lot (about 19%): `back.out(2.5)` `cubic-bezier(0.34, 1.84, 0.64, 1)`, spring bounce 0.55 |
| **Stagger (rhythm)** | together 0 ms · cascade 30–60 ms · flowing 80–120 ms · wave (delay grows with distance) · random |
| **Distance** | subtle 4–8 px · medium 20–40 px · big 80 px or more · full-screen wipes |
| **Delay** | start later or earlier in 100 ms steps; between elements use Stagger |
| **Trigger** | on load · on scroll into view · scrubbed with scroll · on hover · on click · on cursor move · loop |
| **Intensity** | one hero moment · a few accents · everything moves |

Exits run at about 75% of the entrance duration.

---

## Effects: what moves

Each recipe is an effect with the feel it usually uses. Swap the feel to change the mood: a mask reveal with Snappy instead of Luxurious reads as tech, not fashion.

### Calm and premium

#### 1. Functional · feel: Crisp
Quiet UI motion that helps without being noticed. For apps, dashboards and forms.
- **Say:** subtle, quick, crisp, functional, barely there
- **Values:** 150–250 ms · `power3.out` · move 4–8 px · opacity plus a small translate · stagger 20–40 ms
- **Avoid:** overshoot, scale above 1.03, anything longer than 400 ms

#### 2. Editorial · feel: Luxurious
Slow, confident and expensive, like turning a magazine page.
- **Say:** elegant, restrained, line-by-line, mask reveal, slow zoom-out, settle
- **Values:** 0.8–1.4 s · `expo.out` or `power4.out` · text lines rise 100% inside a mask (`overflow: hidden`) · images scale 1.1 → 1 over 1.2–1.6 s · stagger 80–120 ms per line
- **Avoid:** bounce, rotation, fast stagger

#### 3. Organic / Ambient · feel: Floaty
Alive and breathing; it never stops, but it never asks for attention.
- **Say:** flowing, drifting, breathing, liquid, morphing, soft loop, gradient drift
- **Values:** loops of 4–20 s · `sine.inOut` · yoyo · small amplitude · offset the loops so they never sync
- **Avoid:** hard starts and stops, sharp easing

#### 4. Cinematic · feel: Dramatic
Moves like a film camera: depth, slow push-ins, one big moment.
- **Say:** cinematic, camera push-in, depth, rack focus (blur to sharp), dramatic reveal, letterbox
- **Values:** 1.2–3 s · `power2.inOut` or `power3.inOut` · slow scale 1 → 1.05–1.15 · blur 10 px → 0 · layers at different speeds
- **Avoid:** UI timings, many small moving parts

---

### Energetic and expressive

#### 5. Snappy · feel: Snappy
Fast, decisive, lands hard. Tech launches, bold brands.
- **Say:** snappy, punchy, crisp, decisive, tight stagger
- **Values:** 250–500 ms · `expo.out` · distance 40–100 px · stagger 30–60 ms · scale 0.95 → 1
- **Avoid:** long fades, sine easing, overshoot

#### 6. Playful · feel: Pop or Springy
Friendly and toy-like, with a bit of overshoot.
- **Say:** bouncy, springy, squishy, wobbly, pop, squash and stretch
- **Values:** 400–700 ms · `back.out(1.7)` or `elastic.out(1, 0.5)` · springs around stiffness 300, damping 15 · pops 0 → 1.1 → 1 · wiggles ±3–6°
- **Avoid:** serious or luxury brands. Bounce reads as dated on most brands; use it only when the brand is playful.

#### 7. Kinetic type · feel: Snappy
The text is the hero and moves like a poster.
- **Say:** kinetic type, split letters, staggered characters, rotating word, marquee, stretch, variable font weight
- **Values:** 15–40 ms stagger per character · 400–800 ms per character · `expo.out` · marquees at 40–100 px per second · one mask per line

#### 8. Brutalist · feel: Stepped
Raw and abrupt on purpose.
- **Say:** hard cut, instant, no easing, jump, stepped, blunt, flash, invert
- **Values:** 0 ms cuts or `steps(2–4)` · `linear` · flashes of 80–150 ms · big position jumps · colour inversions
- **Avoid:** soft fades, gentle easing

#### 9. Glitch · feel: Stepped
Digital, hacked, data-driven.
- **Say:** glitch, text scramble, decode, RGB split, flicker, noise, scanlines
- **Values:** scramble ticks of 30–60 ms per character · flicker with `steps(1)` at random 50–120 ms · RGB offset 2–6 px · bursts of 200–400 ms, then rest

#### 10. Hand-made · feel: Stepped
Crafted and imperfect, frame by frame. Includes pixel and retro.
- **Say:** stop-motion, hand-drawn, boiling lines, jitter, on twos, paper cut-out, pixel, 8-bit
- **Values:** `steps()` · 8–12 fps (on twos) · random jitter of 1–2 px and ±1° · sprite sheets
- **Avoid:** silky 60 fps easing, which breaks the illusion

---

### Driven by the visitor

#### 11. Scrollytelling · feel: Mechanical (scrubbed)
The scroll drives the animation; the visitor controls the pace.
- **Say:** scroll-scrubbed, pinned section, plays as you scroll, sticky, progress-linked
- **Values:** `scrub: true`, or 0.5–1 for smoothing · pin length 100–300% of the screen height · `ease: none` on scrubbed tweens · one idea per pinned section

#### 12. Parallax / Depth · feel: Mechanical (scroll-linked)
Layered, as if the page has 3D space.
- **Say:** parallax, depth layers, foreground faster than background, tilt, perspective, float
- **Values:** layer speeds 0.8–1.2× (subtle) to 0.5–1.5× (strong) · tilt ±5–10° · perspective 800–1200 px
- **Avoid:** parallax on body text, big speed differences on mobile

#### 13. Magnetic / Cursor · feel: Springy
The page notices the visitor: things lean toward, trail or light up from the cursor.
- **Say:** magnetic, cursor-follow, trailing, lazy follow, spotlight, hover tilt
- **Values:** follow smoothing (lerp) 0.1–0.2 per frame, lower is lazier · magnetic pull 20–40% of the distance · spring back in 400–600 ms with `elastic.out(1, 0.4)` or `power3.out`

#### 14. Morph · feel: Smooth
Nothing jumps; one thing turns into the next.
- **Say:** morph, seamless, shared element, turns into, continuity, layout animation
- **Values:** 300–600 ms · `power2.inOut` or `expo.inOut` · GSAP Flip or the browser's View Transitions · icon morphs

---

## Ready-to-paste code

### Springs, elastic and bounce in plain CSS

```css
:root {
  /* Springy: bounce 0.3, about 5% overshoot. Use at 400-600 ms. */
  --ease-springy: linear(0, 0.01, 0.036, 0.075, 0.124, 0.18, 0.242, 0.306, 0.371, 0.436, 0.5, 0.562, 0.62, 0.675, 0.726, 0.772, 0.815, 0.853, 0.887, 0.917, 0.943, 0.965, 0.984, 1, 1.013, 1.023, 1.031, 1.037, 1.042, 1.044, 1.046, 1.046, 1.045, 1.044, 1.042, 1.04, 1.037, 1.034, 1.031, 1.028, 1);
  /* Elastic: elastic.out(1, 0.3). Use at about 1 s. */
  --ease-elastic: linear(0, 0.163, 0.392, 0.646, 0.891, 1.097, 1.25, 1.341, 1.373, 1.354, 1.296, 1.215, 1.125, 1.039, 0.966, 0.912, 0.879, 0.868, 0.875, 0.895, 0.924, 0.956, 0.986, 1.012, 1.031, 1.043, 1.047, 1.044, 1.037, 1.027, 1.016, 1.005, 0.996, 0.989, 0.985, 0.984, 0.984, 0.987, 0.99, 0.994, 0.998, 1.002, 1.004, 1.005, 1.006, 1.006, 1.005, 1.003, 1.002, 1.001, 0.999, 0.999, 0.998, 0.998, 0.998, 0.998, 0.999, 0.999, 1, 1, 1);
  /* Bounce: bounce.out. Use at about 900 ms. */
  --ease-bounce: linear(0, 0.004, 0.016, 0.035, 0.062, 0.098, 0.141, 0.191, 0.25, 0.316, 0.391, 0.473, 0.562, 0.66, 0.766, 0.879, 1, 0.941, 0.891, 0.848, 0.812, 0.785, 0.766, 0.754, 0.75, 0.754, 0.766, 0.785, 0.812, 0.848, 0.891, 0.941, 1, 0.973, 0.953, 0.941, 0.938, 0.941, 0.953, 0.973, 1, 0.988, 0.984, 0.988, 1);
}
```

For the few old browsers without `linear()`, swap in the closest curves:

```css
@supports not (transition-timing-function: linear(0, 1)) {
  :root {
    --ease-springy: cubic-bezier(0.34, 1.4, 0.64, 1);
    --ease-elastic: cubic-bezier(0.34, 1.56, 0.64, 1);
    --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
  }
}
```

For other spring settings, copy `spring()` and `toLinear()` from `../assets/feels-demo.html`.

### Scroll reveal that plays once, and never hides content

```html
<script>document.documentElement.classList.add('js');</script> <!-- early in <head> -->
```

```css
.js .reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity var(--motion-dur) var(--motion-ease), transform var(--motion-dur) var(--motion-ease);
  transition-delay: calc(var(--i, 0) * var(--motion-stagger, 0ms));
}
.js .reveal.is-in { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) {
  .js .reveal { transform: none; }
}
```

```js
const io = new IntersectionObserver((entries) => {
  for (const e of entries) {
    if (!e.isIntersecting) continue;
    e.target.classList.add('is-in');
    io.unobserve(e.target); // play once
  }
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach((el, i) => { el.style.setProperty('--i', i % 6); io.observe(el); });
```

### Hover that only runs with a mouse, and reverses smoothly

```css
.card { transition: transform 250ms cubic-bezier(0.16, 1, 0.3, 1); }
@media (hover: hover) and (pointer: fine) {
  .card:hover { transform: translateY(-4px); }
}
```

---

## Where this comes from
- Timings: common interface practice (durations by purpose, ease-out curves, exits at about 75% of the entrance).
- Easing names: GSAP's ease set (power1–4, expo, sine, back, elastic, steps).
- Feels: standard easing families (Penner curves as used by GSAP and easings.net), a damped spring for Springy (bounce as in SwiftUI and Motion: damping ratio = 1 − bounce), and GSAP's elastic and bounce formulas.
- When to animate, interface vs showcase speeds, build rules and the review list (in SKILL.md): adapted for websites from Emil Kowalski's skills (MIT), github.com/emilkowalski/skills, 10 Nov 2026.
- Style families: Disney's 12 principles (squash and stretch, slow in and out), IBM Carbon's productive vs expressive motion, and the categories used by motion showcases such as Osmo Supply and Made With GSAP.
