# How to access the CeeRO store

## 0. The permanent link
**https://unborn7g.github.io/ceero/** — the storefront.
**https://unborn7g.github.io/ceero/plan/** — the master plan.

Both are plain GitHub Pages, free, no account needed to view. See
`PUBLISH-TO-GITHUB.md` for the push steps if the site is not live yet.

## 1. Right now — live preview (easiest)
The store is running on a live server in this workspace. Open the **Live Preview** panel beside this conversation and choose **CeeRO storefront**. It is a real HTTP URL you can open on your phone too.

Nothing to install, nothing to log into. It stays up while this session is active.

## 2. Anywhere, forever — the single file
`ceero-store/index.html` is fully self-contained: every image is embedded, there are no external scripts, fonts or CDNs.

- Download the file and double-click it. It opens in any browser, online or offline.
- You can email it, put it on a USB stick, or upload it anywhere.
- It also previews inside this app — open the file directly.

## 3. A permanent public URL with your own domain
The build is one static file, so any static host works free.

**Netlify Drop (no account needed to test)**
1. Go to `app.netlify.com/drop`
2. Drag the whole `ceero-store` folder onto the page
3. You get a URL like `ceero-demo.netlify.app` in about 10 seconds
4. Create a free account to keep it, rename it, or attach a domain

**Vercel**
```bash
npm i -g vercel
cd ceero-store
vercel --prod
```

**Cloudflare Pages** — create a project, upload the folder as a direct upload, get `*.pages.dev`.

**Your own domain** — buy `ceero.com` (~$10–12/yr) or `ceero.ng`, then add it in the host's dashboard. DNS takes effect within an hour. Verify the handle is free *before* you print packaging.

## 4. What this demo is not
It is a **front-end prototype**: no database, no payment capture, no orders. The catalogue, cart persistence (localStorage) and checkout are simulated in the browser on purpose, so it can be shared and clicked without a backend.

To take real money you need the stack in the master plan (§7):
- **Medusa** for products, carts, orders, regions and promotions
- **Paystack** hosted checkout plus a verified webhook — that webhook is the only thing that should ever mark an order paid
- **Postgres** for storage, **Resend** for order email, **CJ Dropshipping** for fulfilment

The demo is the design reference a developer builds against: same components, same copy, same flow, with the in-browser state swapped for Medusa calls and the demo checkout swapped for Paystack.

## 5. Quick tour of what to click
| Do this | To see |
|---|---|
| Open `#/shop` | The full seven-product collection and category filters |
| Open any product | Size/colour selection, quantity stepper, add-ons, specs, reviews |
| Add to Bag | Slide-in glass drawer with free-delivery meter |
| Switch ₦ NGN / $ USD | Every price re-renders in the second currency |
| Go to Bag, enter `CEERO10` | 10% discount applied (also try `WIND20`, `FREESHIP`) |
| Checkout → fill the form → Place demo order | The full order-confirmation state |
| Resize to phone width | The mobile layout: stacked hero, sticky nav, thumb-friendly controls |
