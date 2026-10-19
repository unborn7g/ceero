# Design notes — what I took from the three galleries

Sources reviewed: [Land-book](https://land-book.com/) (ecommerce curation), [Behance](https://www.behance.net/search/projects?search=apple%20style%20ecommerce%20website), [Prompt Motion](https://prompt-motion.com/).

## Land-book — ecommerce curation (Eadem, Nossara, SIHA, Heist, MATE the Label)
**Pattern:** premium stores open with one product photograph and a single sentence, not a carousel. Colour is left in the photography; the interface stays neutral. Product listings use generous gutters and few items per row.

**Applied:** full-bleed hero with the dog on the right and type on the left; 980px content column; 4-up product grid with 1:1 imagery; centred section statements; no badges or starbursts anywhere.

## Behance — Apple-style ecommerce / IoT case studies
**Pattern:** case-study presentations rely on three devices — the *spec block* (three short numbers under a product), the *macro detail band* (an extreme close-up proving material quality), and *tile stacks* where one wide tile is followed by two halves.

**Applied:** the `12 cm / Cold wash / 3 sizes` spec row, the bouclé macro band with dark scrim, the wide bed tile + two half tiles, and the dark "Wind-Down Set" tile for contrast. Same devices, real dog products.

## Prompt Motion — motion language
**Pattern:** the videos that feel premium are short, slow and tied to a physical property — material flexing, light moving, a texture resolving into focus. Fast cuts read as cheap.

**Applied in the store:** 18px scroll reveals, 700ms easing, slow 1.03× image scale on hover, a 380ms drawer. **Not applied:** scroll-jacking, parallax layers, autoplaying video. On a mid-range Android in Lagos, those cost frames and conversions.

## The Apple specifics worth knowing
1. **One idea per section.** Each band makes a single claim and stops.
2. **Type does the work.** Tight tracking (−0.02em), 600 weight, no decorative fonts.
3. **Blue means action.** #0071E3 appears only on things you can click.
4. **Hairlines, not shadows.** Dividers separate; drop shadows are reserved for the floating drawer and toast.
5. **Negative space is the product.** Studio-neutral backgrounds let the object breathe.
6. **Restraint in motion.** If it needs a 60fps phone to look right, it is wrong.

## What I deliberately did not copy
- **Serif headlines** from the v1 build — Apple-style needs a single sans voice.
- **Sticky "buy" bars and countdown timers.** They convert, but they read as discount retail and undercut a premium brand claim.
- **Infinite scroll product feeds.** Seven products is the point; a shopper should be able to see the whole range.

## Where premium and conversion trade off
Apple can afford long pages and few calls to action because people already want the product. A new store cannot. The compromise in this build: Apple's visual discipline, but the price, delivery promise and Add to Bag sit above the fold on every product page, and the free-delivery threshold is stated in the header.

---

# v3 — Liquid Glass, dark mode, and Mochi

## The glass material
Every translucent surface is one recipe: `backdrop-filter: blur(22px) saturate(180%)` over a semi-transparent fill, plus three edge treatments that do the heavy lifting — an inset 1px white highlight on top, an inset dark hairline at the bottom, and a soft ambient shadow. That combination is what makes a panel read as *glass* rather than *grey box*.

A specular highlight follows the pointer across `.glass` and product cards (`--mx` / `--my` custom properties), which is the "liquid" part: the surface appears to catch light as you move.

## Dark mode
One token set, two palettes. `[data-theme="dark"]` redefines ~25 variables — surfaces, hairlines, glass fills, accent hues, shadow depths. Nothing in the components knows which theme is active.

- **Default:** follows the OS via `prefers-color-scheme`.
- **Override:** the nav toggle writes to `localStorage`, so a choice survives reloads.
- **Transition:** `document.startViewTransition` where supported, plus a 500ms colour cross-fade; falls back to an instant swap in older browsers.
- **Photography:** images drop to 82–96% brightness in dark so they don't glare.
- **Mesh:** five drifting colour blobs sit behind everything at `z-index:-2`, tinted differently per theme, with a faint grain layer on top to kill banding.

## The animation list (what actually moves)
| Element | Motion |
|---|---|
| Hero | 24s Ken Burns drift, pointer parallax, staggered type entrance (50→360ms) |
| Nav | Floating glass capsule that shrinks and rounds tighter on scroll; logo tilts on hover; clay dot pulses |
| Scroll | 2px gradient progress bar; sections reveal at 26px with a 6px blur-out, staggered 70ms per child |
| Cards | Pointer tilt (2.4–3.2°), light glare following the cursor, lift on hover, press animation |
| Buttons | Spring scale on hover/active, gradient bevel, specular sweep across primaries, click ripple from the pointer |
| Bag | "Fly to bag" — a clone of the product image arcs into the icon, which then pops; count badge bumps |
| Drawer | Spring open at 580ms, cart lines stagger in from the right with delays |
| Stats | Numbers count up from zero when scrolled into view |
| Gallery | Light sweep across the product image on hover; thumbnail border snaps |
| Accordions | Height + opacity easing instead of a hard show/hide |
| Marquee | Trust strip scrolls infinitely, pauses on hover; icons float |
| Confirmation | Tick springs in with a drawn checkmark, 24 SVG paws and bones scatter and fall |
| Mochi | Breathing bob, blink every ~5.6s, tail wag, occasional ear flick, jump when you add to bag |
| Theme | View-transition wipe |

## Mochi
A cream puppy who lives bottom-left. Facts: breathes, blinks, wags, flicks an ear, jumps when you add something to the bag, and comments on where you are — shop, cart, checkout, confirmation — with a dry line or two. Dismissible (the ✕ writes `ceero-mochi=off` to localStorage); coming back is a click on the orb.

Drawn as inline SVG with CSS-animated parts (`.m-tail`, `.m-eye`, `.m-ear-l/r`), so she weighs nothing and inherits theme colours.

## Keeping it honest
- `prefers-reduced-motion` kills every looping animation and sets transitions to 0.001ms — verified: zero invisible elements under reduced motion.
- Nothing animates on scroll position except the progress bar and reveals; no scroll-jacking, no parallax on text.
- Everything is CSS or the Web Animations API — no animation library, no bundle cost.
- Full page is still one file: 1.16 MB, mostly inlined photography.
