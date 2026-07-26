---
name: social-links
description: Add or update social media links on the Compliment Fest site. Use when someone wants to surface an Instagram, TikTok, Discord, or other social/contact link. Explains the shared "Follow along" footer pattern, the accessible markup, and the on-brand styling so new links stay consistent.
---

This is a static single-page site (`index.html` + `styles.css`, no build step). Social links live in the footer inside the `.footer-social` "Follow along" block. Reuse that block for every social/contact link so they stay visually consistent and accessible.

## Where links live

- HTML: the `.footer-social` block in `index.html`, placed after `.footer-date` and before the `.footer-support` grant attribution.
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
