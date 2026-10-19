# CeeRO

A working storefront demo for calm-home dog goods — plus the operating plan behind it.

**Live:** https://unborn7g.github.io/ceero/

| | |
|---|---|
| **Storefront** | https://unborn7g.github.io/ceero/ |
| **Master plan** | https://unborn7g.github.io/ceero/plan/ |
| **Unit economics** | [ceero-unit-economics.xlsx](ceero-unit-economics.xlsx) |
| **Design notes** | [DESIGN-NOTES.md](DESIGN-NOTES.md) |

## What this is

CeeRO sells seven things for dogs who pace, gulp and startle: a calming bed,
a lick mat, a slow feeder, a snuffle mat, a travel bottle, grooming gloves and
a bundle. The storefront is a real, clickable flow — browse, filter, open a
product, pick a variant, add to bag, apply a coupon, check out, confirm.

It is a **demo**. No real payments, no real orders, no card is ever stored.
The payment step is simulated on purpose and labelled as such in the UI.

- Currency toggle: ₦ NGN (Nigeria, Track A) and $ USD.
- Codes that work: `CEERO10`, `WIND20`, `FREESHIP`.
- Free delivery over ₦50,000, flat ₦2,500 under that.
- Light and dark mode, with the choice remembered.

## Everything is one file

`index.html` is 1.16 MB of self-contained HTML — CSS, JS and every photo
inlined as a data URI. No build step, no CDN, no fonts to fetch, no network
calls. It works offline, from a USB stick, or on any static host.

The plan at `plan/index.html` is the same idea: 205 kB, self-contained.

## Hosting

Served by GitHub Pages straight from the `main` branch root. No Jekyll
(`.nojekyll` is present), no Actions, nothing to keep alive.

## Further reading

- [DESIGN-NOTES.md](DESIGN-NOTES.md) — the design system, motion inventory, what was tried and rejected.
- [HOW-TO-ACCESS.md](HOW-TO-ACCESS.md) — how to open the site locally or on a phone.

---

Prototype. Not a real shop yet.
