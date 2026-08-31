# VIP Tanning & Wellness Oxford — Price Board

A single-page price board for VIP Tanning & Wellness (Oxford), designed to run
fullscreen on an in-store display.

- **Live site:** https://vip-priceboard.vercel.app (deploys automatically from `master`)
- **Everything lives in `index.html`** — no build step, no framework.

## Layout

1. **Header** — title plus a gear button that opens the PIN-locked staff settings.
2. **VIP Smart Pay Memberships (EFTs)** — four hero cards: VHR, All UV Access,
   Wellness & Spray, All UV & Wellness (featured, with rotating equipment carousel).
3. **Package panels** — four color-coded columns: VHR Bed & Stand-Up (red),
   Ultra VHR/HP (yellow), Ultra High Pressure (black), Wellness & Spray (blue).
4. **Perks strip + fine print.**

## Staff settings (gear icon)

The gear in the header opens a 4-digit PIN pad (the PIN is set in `index.html`
— search for `var PIN`). Behind it:

- **Half-Off Event toggle** — flips the whole board into sale mode:
  - "1 Month Unlimited" rows show the crossed-out regular price and the
    half-off price in promo pink (e.g. Wellness: ~~reg. $139~~ **$69.50**).
  - Wellness Single Visit shows ~~reg. $35~~ **$17.50**.
  - EFT "to start" buttons switch to **FREE to start — no enrollment fee**.
  - A banner appears in the header.
  - Off = normal prices, and regular prices display as plain "reg. $XX"
    (no strikethrough outside the event).
- **Edit mode** — click any text on the board to change it in place.
- **Save Copy** — downloads the edited board as a standalone HTML file.

Prices that change during the event are driven by `data-normal` / `data-promo`
attributes on `.px` elements — edit those to change either price.

## Images

Most equipment photos load from the salon's Wix media CDN (`static.wixstatic.com`).
The VersaSpa images are hosted locally in `img/` because the Wix copy was a
broken, cropped 104×150 thumbnail:

- `img/versaspa-pro.png` — full product shot (hero card + carousel)
- `img/versaspa-thumb.png` — brightened variant for the small panel circle

To replace any other image, drop a file in `img/` and point the `<img>` at it —
local files are more reliable than the Wix CDN.

## Deploying

Push to `master` → Vercel deploys the public site automatically (~1 minute).
Feature branches get their own preview URLs. After deploying, hard-refresh
(Ctrl/Cmd+Shift+R) — the display may cache the old page.
