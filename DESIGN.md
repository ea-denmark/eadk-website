# DESIGN.md: Effektiv Altruisme Norge

## Source
- URL: https://www.effektivaltruisme.no/
- Capture date: 2026-08-21
- Evidence: full-page screenshot (1440×7121) + live `getComputedStyle` measurement of the
  rendered homepage (headings, body copy, buttons, nav, colour census, layout widths).
- Note: Firecrawl was unavailable in this environment (no API key), so the same evidence was
  collected by driving the page in a real browser. Computed styles are measured values, not
  inferences; anything marked *(inferred)* below was read off the screenshot instead.

## Reference Screenshot
![Full-page screenshot of Effektiv Altruisme Norge](./.firecrawl/eano-screenshot.png)

Use this screenshot as the visual source of truth for layout, hierarchy, density, and feel.
The tokens below describe the same page in machine-readable form.

## Design Summary

A quiet, warm, Scandinavian nonprofit site. The page is one continuous field of warm off-white;
structure comes from **whitespace and full-bleed colour bands**, never from borders, outlines,
or shadows — there is effectively no card chrome anywhere on the page. Two accents do all the
work: a deep forest green for the bands and feature cards, and a pale mint used almost
exclusively on buttons. Type is a single grotesque at one weight for every heading, set tight
(negative tracking, leading close to 1.1) against short, generously spaced paragraphs.

The result reads as calm and institutional rather than campaigning: no gradients, no motion of
consequence, no hero photograph behind text. Content is dense in the columns and airy between
them.

## Design Tokens

### Colors

| Role | Value | Evidence |
|---|---|---|
| Page background | `#faf8f4` warm off-white | measured, 193 elements |
| Body / heading text | `#202022` near-black | measured, 798 elements |
| Deep green (bands, feature cards, footer) | `#22352b` | measured |
| Mint (primary button fill, accents) | `#cef0dc` | measured |
| Mint, secondary tint | `#ccf2e4` | measured |
| Button label on mint | `#000000` | measured |
| Text on deep green | `#faf8f4` | measured |
| Muted text | `rgba(32,32,34,0.5)` | measured |
| Pale blue (rare accent) | `#deeaff` | measured, 1 element |

There is no red, no orange, and no third chromatic accent. Green and mint carry the whole brand.

### Typography

- Family: **Inter** across the entire page (1012 elements); `aktiv-grotesk` appears once and
  can be ignored. Fallback: `-apple-system, 'Segoe UI', Helvetica, Arial, sans-serif`.
- Every heading is **weight 600**. Body copy is 400. Nav links are 500.
- All headings carry **letter-spacing −0.02em** and leading between 1.09 and 1.19.

| Element | Size | Line-height | Tracking |
|---|---|---|---|
| H1 | 60.8px | 64.79px (1.07) | −1.216px |
| H2 | 44.8px | 49.89px (1.11) | −0.896px |
| H3 | 25.92px | 30.33px (1.17) | −0.518px |
| H4 (card/grid titles) | 19.2px | 22.86px (1.19) | −0.384px |
| Body paragraph | 19.2px | 24.96px (1.30) | normal |
| Nav link | 16px, weight 500 | — | normal |
| Button label | 19.2px, weight 500 | — | normal |

Body text at 19.2px with 1.30 leading is unusually tight for the size — it reads as dense,
efficient columns rather than relaxed long-form. *(For Danish or English at longer measures,
relaxing to ~1.5 is advisable; the tightness suits Norwegian's shorter lines.)*

### Spacing And Layout

- Main container: **1200px**. Half column 544px, three-up grid cell 344px (≈40px gutters),
  prose measure ≈694px.
- Header: **61px tall**, `position: fixed`, background `#faf8f4`, **no bottom border**, no
  shadow, no backdrop blur.
- Radius: buttons `20px` (reads as a pill at these paddings); composed feature cards ≈`16px`
  *(inferred from screenshot)*; **content images have radius 0** (measured).
- Button padding: `24px 35.2px` — very generous, roughly `1.5rem 2.2rem`.
- Colour bands (newsletter, footer) are **full-bleed with radius 0**; feature/announcement
  cards are inset within the container and rounded.
- Borders: none. Shadows: none. This is the single most defining rule of the system.

## Components

**Announcement card (top of page).** Deep-green rounded rectangle inset in the container,
split text-left / photo-right. Small heading, two short paragraphs, one mint pill button.
Replaces what most sites would make a hero band — it is compact, not full-viewport.

**Photo with overlapping caption card.** A wide photograph with a white rounded card
overlapping its lower-left corner carrying a single headline. The most distinctive composition
on the page.

**Text-column sections.** Left-aligned H1/H2, then two or three columns of small H3/H4 plus a
short paragraph. No dividers, no boxes — columns are separated by gutter alone.

**Action grid ("Hva du kan gjøre").** Centred headline and intro, then a 3×2 grid of
image + H4 + paragraph. No card background, no border, no hover lift.

**Promo card.** Deep-green rounded card, heading + date subheading, two pill buttons side by
side (mint filled, then white outline).

**Buttons.** Mint fill, black label, weight 500, 20px radius, generous padding. Secondary is a
white/outline pill. No uppercase, no letter-spacing, no icon.

**Newsletter band.** Full-bleed deep green, white heading, inline first/last/email inputs with
white fills, mint pill submit.

**Testimonials.** Italic quote, thin rule, then name and role in small text. Multi-column,
no cards, no portraits.

**Footer.** Deep green, brand blurb and org number on the left, two link columns on the right,
newsletter form repeated beneath, social icons.

## Page Patterns

Section order on the homepage:

1. Announcement card (recruiting/news)
2. Photo band with overlapping caption card
3. **"Hva er effektiv altruisme?"** — explain the idea first
4. **"Hva du kan gjøre"** — only then ask for action
5. Event promo card
6. "Effektiv altruisme i Norge" — about the org, with a mint CTA
7. Newsletter band (deep green)
8. Testimonials
9. Footer (deep green)

The explain-before-act ordering is the notable structural choice: the site earns the ask before
making it. Sections alternate between left-aligned and centred alignment rather than between
background colours.

Responsive behaviour *(inferred)*: the 3-up grids collapse to 1 column, the split cards stack
text-above-photo, and the container falls back to full width minus a ~24px gutter.

## Content Style

Headings are plain declarative statements or direct questions — "Hva er effektiv altruisme?",
"Hva du kan gjøre", "Når gode intensjoner blir til ekte resultater". No slogans, no
exclamation except on genuine announcements. CTAs are short and unhyped: "Lær mer", "Meld på",
"Bli med", "Finn ut mer om oss". Paragraphs run two to four sentences. Bold is used inline to
pick out key terms inside paragraphs rather than as a separate heading level.

## Agent Build Instructions

To build a page in this style:

1. Set the page background to `#faf8f4` and all text to `#202022`. Do not introduce a third
   text colour; use `rgba(32,32,34,0.5)` for genuinely secondary text only.
2. Load Inter (400/500/600). Set every heading to weight 600, `letter-spacing: -0.02em`, and
   `line-height: 1.1`. Never use a serif, never use uppercase, never use letter-spaced labels.
3. Remove every border and box-shadow. Group content with whitespace, gutters, and colour
   fields exclusively. If a block needs to feel separate, give it a deep-green fill and 16px
   radius, or a full-bleed green band.
4. Constrain content to 1200px; prose to ~694px; use 3-up grids of ~344px cells.
5. Buttons: mint `#cef0dc` fill, black label, weight 500, `border-radius: 20px`, padding
   `1.5rem 2.2rem`. Secondary buttons are outlined pills, same geometry.
6. Keep the header 61px, fixed, background-matched, borderless.
7. Order sections to explain before asking: identity → what it is → what you can do →
   community → questions → newsletter.
8. Motion should be near-absent: at most a colour transition on hover. No lifts, no glows.

Do not reuse Effektiv Altruisme Norge's logo, photography, or copy — this document describes a
visual language only.

## Rerun Inputs
workflow: firecrawl-website-design-clone
source_url: https://www.effektivaltruisme.no/
target_stack: Hugo theme overlay (themes/eadk/static/css/theme-norge.css, plus
  theme-roed.css which reuses the whole system with EA Denmark's red in place of
  the forest green)
output: DESIGN.md
