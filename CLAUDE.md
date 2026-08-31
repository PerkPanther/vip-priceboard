# Guidance for Claude sessions working on this repo

Single-file static price board (`index.html`) for a tanning salon, shown
fullscreen on an in-store display. Vercel auto-deploys `master` to
https://vip-priceboard.vercel.app. See README.md for the feature overview.

## Hard-won rules — read before changing anything

1. **Multiple Claude sessions work on this repo in parallel and push to
   `master`.** Before starting any change, `git fetch` and merge
   `origin/master` into your branch. If a fast-forward of master fails,
   someone else pushed — merge their work in, never force-push or clobber it.

2. **The public site serves `master` only.** The owner looks at
   vip-priceboard.vercel.app. Work left on a feature branch is invisible to
   them and they will report "I don't see any changes." When they approve a
   change, merge it to `master` promptly. Remind them to hard-refresh.

3. **The whole board must fit 100vh with zero scrolling.** Row chips in the
   package panels flex-shrink; enlarged fonts overflow and stack digits onto
   neighboring rows (this has happened — twice). If you grow any font in the
   panels, shrink something else or verify the tight 6-row Ultra panels still
   fit. Do not add `transform: scaleX()` stretches to prices — it caused
   label overlap and was removed deliberately.

4. **Font intent:** Anton (condensed, tall) for display headings and hero
   prices; Archivo 900 (wide digits) for package-panel prices — chosen
   because the owner wants panel numbers wide, not tall. Panel prices are
   styled like the hero EFT prices: solid gold, soft glow, **no text-stroke
   outlines** (strokes made digits muddy and were removed).

5. **Images:** this sandbox CANNOT reach `static.wixstatic.com`,
   `vipsteve.wixsite.com`, `vercel.app`, or most of the web (egress policy).
   You cannot preview remote images. If you must obtain or inspect a remote
   asset, the proven workaround is a temporary GitHub Actions workflow that
   downloads it and commits it (runners have open internet); delete the
   workflow after. Prefer hosting images locally in `img/`. The Wix VersaSpa
   media (`914cee_f863...`) is a broken 104×150 pre-cropped file — never
   reuse it; local `img/versaspa-*.png` replaced it.

6. **Editable-text system:** elements with class `.ed` become
   `contenteditable` in Edit mode. Promo-price swaps use `.px` elements with
   `data-normal` / `data-promo`; the Half-Off toggle rewrites their
   textContent. When adding a price that changes during the event, follow
   that pattern (see the Wellness Single Visit row). `.reg` renders a
   "reg. " prefix via CSS `::before` and is struck through only under
   `body.promo`; `.promo-only` elements appear only during the event.

7. **Staff settings** (Half-Off toggle, Edit, Save Copy) live behind a
   PIN-locked sheet opened by the header gear (`var PIN` in the script).
   Don't resurface those controls on the board itself.

8. The owner communicates tersely and via screenshots of the live display.
   Before "fixing" something they say is still broken, verify whether your
   change actually reached `master` and whether they're seeing a cached page.
