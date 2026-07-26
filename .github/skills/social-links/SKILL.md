---
name: social-links
description: Add or update social media links and sponsor/supporter credits on the Compliment Fest site. Use when someone wants to surface an Instagram, TikTok, Discord, or other social/contact link, or credit a sponsor. Explains the shared "Follow along" social block, the "Sponsored by"/"Supported by" credits pattern, the accessible markup, and the on-brand styling so new links and credits stay consistent.
---

This is a static single-page site (`index.html` + `styles.css`, no build step). Social links live in the footer inside the `.footer-social` "Follow along" block. Reuse that block for every social/contact link so they stay visually consistent and accessible.

## Where links live

- HTML: the `.footer-social` block in `index.html`, placed after `.footer-date` (it is the last block in the footer now that credits were promoted into the `.supporters` main-content section — see "Adding a sponsor credit" below).
- CSS: the `/* Social / "Follow along" */` section in `styles.css`.

The current block contains one Instagram link. Add more links as additional `.footer-social-link` anchors inside the same `.footer-social` container.

## How to add a social link

1. Add an anchor inside `.footer-social`, following the existing Instagram example:

```html
<a class="footer-social-link"
   href="SOCIAL_URL"
   target="_blank" rel="noopener noreferrer"
   aria-label="Follow Compliment Fest on PLATFORM (opens in a new tab)">
  <svg class="footer-social-icon" viewBox="0 0 24 24" width="26" height="26"
       fill="none" stroke="currentColor" stroke-width="2"
       stroke-linecap="round" stroke-linejoin="round"
       aria-hidden="true" focusable="false">
    <!-- platform icon paths -->
  </svg>
  <span class="footer-social-handle">@handle</span>
</a>
```

2. Requirements for every link:
   - `target="_blank"` **and** `rel="noopener noreferrer"` (external links open in a new tab).
   - Descriptive `aria-label` that names the platform and notes it opens in a new tab.
   - Inline SVG icon using `stroke="currentColor"` so it inherits the button text color; mark it `aria-hidden="true" focusable="false"`.
   - A visible `.footer-social-handle` label (the @handle or name).

3. If you add several links, they already lay out as a centered column (`.footer-social` uses `flex-direction: column; gap`). For a horizontal row of icon-only buttons, wrap the anchors in a flex row and drop the `.footer-social-handle` spans — but keep the `aria-label`.

## Styling / brand notes

Match the site's warm, playful palette via existing CSS variables — do not hardcode hex values:

- Colors: `--gold #F5C842`, `--pink #E84B8A`, `--pink-light`, `--gold-light`, `--brown #5C3D2E`, `--cream #FFF8E7`.
- The `.footer-social-link` button uses a gold→pink-light gradient, a `2.5px` `var(--gold)` border, a fully rounded pill (`border-radius: 999px`), and a chunky offset "hard shadow" (`box-shadow: 0 4px 0 #2a1a12, ...`) consistent with other buttons/cards on the site.
- Hover/focus lifts the button (`translateY(-3px) rotate(-1.5deg)`) and flips the gradient to pink→gold. Always keep a `:focus-visible` state matching hover for keyboard users.
- Fonts: `--font-script` for the small "Follow along" label, `--font-body` (bold) for handles.

> **Lesson learned — outline color on the dark footer:** The footer background is dark brown (`--brown #5C3D2E`), so an outline/border must contrast with it. A `--brown` border was effectively invisible (brown-on-brown). A `--cream` border worked but reads cold; the on-brand choice is a warm accent — use `var(--gold)` for the pill outline. Even where the gold border overlaps the gold end of the gradient fill, the pill's outer edge against the brown background plus the dark offset hard-shadow keep it distinct. Rule of thumb: pick outline colors for contrast against the dark footer, and prefer a warm accent (gold) over neutrals.

## Verification

No linter/build/test exists. After editing, open `index.html` in a browser and confirm: the link renders in the footer, opens the correct profile in a new tab, is keyboard-focusable with a visible focus state, and the icon/handle are legible against the dark footer.

## Adding a sponsor credit ("Sponsored by")

Sponsors are a **credit**, not a social link, so they live grouped with the other credits (under the same "Supported by" grant attribution) — not in `.footer-social`. This keeps supporters and sponsors visually grouped rather than bolted on elsewhere.

> **Credits can live in main content, not just the footer.** Credits started in the footer but were promoted into a dedicated `.supporters` main-content section (`#supporters`, headed "Our Supporters") placed directly above the `.community` section — with the grant ("Supported by") first and the sponsor ("Sponsored by") beneath it, both inside `.supporters-inner`. Wherever they live, keep "Supported by" and "Sponsored by" grouped together. If credits ever move back into the footer, re-check the styling (see the background-contrast lesson below).

- HTML: add a `.supporters-sponsor` block inside `.supporters-inner`, after the `.supporters-support` grant block.
- CSS: the `/* SUPPORTERS SECTION */` block in `styles.css`.

Markup (a well-styled **text** link — do NOT fabricate a logo you don't have):

```html
<!-- Sponsor credit: SPONSOR_NAME -->
<div class="supporters-sponsor">
  <p class="supporters-label">Sponsored by</p>
  <a class="supporters-sponsor-link"
     href="SPONSOR_URL"
     target="_blank" rel="noopener noreferrer"
     aria-label="Visit our sponsor SPONSOR_NAME (opens in a new tab)">
    <span class="supporters-sponsor-name">SPONSOR_NAME</span>
  </a>
</div>
```

Requirements match the social links: `target="_blank"` **and** `rel="noopener noreferrer"`, a descriptive `aria-label` that names the sponsor and notes it opens in a new tab.

Styling: `.supporters-sponsor-link` reuses the pill shape (gold→`--pink-light` gradient, `border-radius: 999px`, chunky offset hard shadow, hover/focus lift that flips the gradient to pink→gold), but tuned for the **light** main-content background — see the contrast lesson below. `.supporters-label` uses `--font-script` in `--pink` with a hairline `--brown` stroke for legibility on cream. Prefer a tasteful text credit; a well-styled text link beats a fake/guessed logo. If a real logo is provided, mirror the `.supporters-logo-link` white-card treatment (white card, `2.5px var(--brown)` border) instead.

> **Lesson learned — match outline/shadow to the background.** The footer is dark brown, so credit pills there used a `var(--gold)` border and a near-black hard shadow (`#2a1a12`). When credits moved into the **light/cream** `.supporters` section, that treatment stopped working: a gold border on a gold-ish pill barely reads against cream, and a black shadow looks harsh. The on-brand fix is the same chunky-outline language the site's other light-background pills/cards use — a `2.5px solid var(--brown)` border and a **brown** hard shadow (`0 4px 0 var(--brown)`), with script labels in `--pink` (hairline brown stroke) instead of `--gold-light`. Rule of thumb: on the dark footer use a warm gold outline; on light main content use a brown outline + brown shadow. Always verify contrast visually after moving between the two.
