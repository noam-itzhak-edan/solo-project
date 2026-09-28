# Design tokens: The Locker

Source: brief §5 and §7 (canonical values) plus the attached mockup (`mockup-portrait.webp`, 941×1672, read as a 390 px wide portrait viewport, so 1 CSS px ≈ 2.41 image px).
When the mockup and the brief disagree, the brief's hex values are canonical, and the mockup decides shape, layout and proportion.

## 1. Color

### Primitives (canonical, from brief §7)

| Token | Hex | Mockup median sampled | Where the mockup uses it |
|---|---|---|---|
| `--c-offwhite` | `#EDECE8` | `#D7CECA` (lit shirts) | Primary text on dark plates, unlocked bone tees |
| `--c-concrete-300` | `#C9C7C2` | `#A6A29F` (tooltip button) | Light button plate ("Add to cart"), hang-tags in light |
| `--c-concrete-500` | `#9A9894` | `#A8AAAC` (lit floor) | Lit concrete, secondary text on charcoal |
| `--c-steel` | `#7A7C7E` | `#777672` (LVL plate) | Raw steel plates, rails, bolts |
| `--c-concrete-700` | `#5E5D5B` | `#5E5C58` (mid rock) | Rock mid-tones, dark plates that carry text |
| `--c-gunmetal` | `#3A3B3D` | `#3E3E3E` (locked shirt) | Locked shirts, secondary dark plates |
| `--c-charcoal` | `#2E2E2F` | `#2F2F2F` / `#303030` (tooltip, cart bar, label inset) | Label insets, tooltip plate, cart bar |
| `--c-amber` | `#C79A5B` | `#AA805A` (fills, graded darker in scene) | Log in, active tab underline, active toggle, thin progress fills. Under 5% of any screen |

Proposed addition (logged in DECISIONS.md): `--c-recess` `#1E1E1F`. The mockup's recessed progress tracks sample at `#262626` and its black tees at `#101010`; nothing in the brief palette is dark enough for a recess.

Measured amber share in the mockup: **2.66%** of pixels (heuristic hue mask). The 5% budget holds.

### Semantic aliases

| Alias | Maps to | Use |
|---|---|---|
| `--surface` | `--c-concrete-700` | Scene and page ground |
| `--surface-deep` | `--c-charcoal` | Editorial sections, footer |
| `--plate` | `--c-concrete-700` | Plates that carry text (see contrast note) |
| `--plate-raw` | `--c-steel` | Structural steel: rails, trims, bolts, the LVL plate with dark text |
| `--plate-inset` | `--c-charcoal` | Engraved label insets, tooltip, cart bar |
| `--plate-light` | `--c-concrete-300` | Light button plate |
| `--recess` | `--c-recess` | Progress tracks, slider tracks |
| `--text` | `--c-offwhite` | Text on plate, inset, surface-deep |
| `--text-muted` | `--c-concrete-500` | Secondary text on inset or charcoal only |
| `--text-on-light` | `--c-charcoal` | Text on plate-light, raw steel, amber |
| `--border` | `--c-steel` | 1 px hairlines |
| `--accent` | `--c-amber` | Fills and indicators, never text on dark, never glow |
| `--focus` | `--c-offwhite` | 2 px outline with 2 px offset, never amber |

### WCAG contrast matrix (ratio, foreground on background)

| fg \ bg | offwhite | light-concrete | mid-concrete | steel | dark-concrete | gunmetal | charcoal | recess | amber |
|---|---|---|---|---|---|---|---|---|---|
| offwhite | — | 1.4 | 2.4 | 3.5 | 5.6 | 9.5 | 11.5 | 14.1 | 2.2 |
| light-concrete | 1.4 | — | 1.7 | 2.5 | 3.9 | 6.6 | 8.0 | 9.9 | 1.5 |
| mid-concrete | 2.4 | 1.7 | — | 1.5 | 2.3 | 3.9 | 4.7 | 5.8 | 1.1 |
| steel | 3.5 | 2.5 | 1.5 | — | 1.6 | 2.7 | 3.2 | 4.0 | 1.6 |
| dark-concrete | 5.6 | 3.9 | 2.3 | 1.6 | — | 1.7 | 2.1 | 2.5 | 2.6 |
| gunmetal | 9.5 | 6.6 | 3.9 | 2.7 | 1.7 | — | 1.2 | 1.5 | 4.4 |
| charcoal | 11.5 | 8.0 | 4.7 | 3.2 | 2.1 | 1.2 | — | 1.2 | 5.3 |
| recess | 14.1 | 9.9 | 5.8 | 4.0 | 2.5 | 1.5 | 1.2 | — | 6.5 |
| amber | 2.2 | 1.5 | 1.1 | 1.6 | 2.6 | 4.4 | 5.3 | 6.5 | — |

Rules this matrix forces:
- **Off-white on raw steel is 3.5:1, which fails AA for normal text.** The mockup's top bar reads as mid-grey steel with light lettering, so any plate that carries small text renders at `--c-concrete-700` (5.6:1) or puts the text on a charcoal inset (11.5:1). Raw steel carries only dark text (charcoal on steel 3.2:1 is large text only) or no text.
- Log in button: charcoal on amber, 5.3:1, passes. Off-white on amber (2.2:1) is not allowed.
- `--text-muted` (mid-concrete) only on charcoal (4.7:1) or recess (5.8:1).
- Non-text UI (progress fill against its recess track): amber on recess 6.5:1, which passes the 3:1 rule.

## 2. Typography (proposed, confirm in Phase 1)

- Display/UI: **Archivo** variable (`wdth` 62–125, `wght` 100–900), used at `wdth` 62–75, `wght` 600–800, uppercase. The mockup's lettering is a condensed bold grotesque with flat terminals; Archivo's width axis covers it in one file.
- Data: **JetBrains Mono** (or IBM Plex Mono) for small stamped figures, uppercase, tracked +0.08em, `font-variant-numeric: tabular-nums`. The mockup sets its numerals in the grotesque, so mono is limited to small data labels (see the Phase 1 question).
- Modular scale, ratio 1.25, base 16: `12 · 14 · 16 · 20 · 25 · 31 · 39 · 49 · 61 · 76 · 95`. At most three sizes per section.
- Display: tracking −0.02em, line-height 0.9, `text-wrap: balance`. Labels: 12–14 px, tracking +0.08 to +0.12em.
- Minimum rendered size **12 px**. At 390 px wide the mockup's hang-tag text would render at about 4 px, which is a layout problem, not a type token (see the Phase 1 question).

## 3. Space, shape, material

| Token | Value | Note |
|---|---|---|
| `--grid` | 8 px | All spacing is a multiple of 4 or 8: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128 |
| `--radius` | 0 | Tailwind radius scale collapses to 0; a build check fails on any non-zero radius or any `backdrop-filter` |
| `--chamfer-xs` | 4 px | Hang-tag top corners, cart badge |
| `--chamfer-sm` | 8 px | Button plates, toggle, small plates |
| `--chamfer-md` | 14 px | LVL plate ends, counter strip, top bar |
| `--chamfer-cut` | 45°, full plate height | Angled right edge of rack label insets ("5K  TIER I" block) |
| `--hairline` | 1 px `--border` | Plate edges, dividers in the tooltip |
| `--bevel` | 1 px top-left highlight `rgb(237 236 232 / .14)`, 1 px bottom-right shade `rgb(0 0 0 / .45)` | Plate edges derived from the upper-left key light |
| `--bolt` | 6 px square-ish hex head, inset 8 px from each corner | Four corners on large plates, two ends on strips. Always the same positions |
| `--engrave` | text `--text`, 1 px inner shadow down-right | Lettering cut into plate |
| `--stamp` | mono, uppercase, 1 px highlight below, slight ink bleed | Hang-tags, LVL, counters |
| `--shadow` | `4px 8px 0 rgb(0 0 0 / .35)` plus `12px 24px 32px rgb(0 0 0 / .25)` | One style only, cast down-right from the upper-left key light. Applied to a sibling layer when the plate is clip-pathed |
| `--grain` | 4% opacity, animated at 12 fps; frozen under reduced motion | One full-screen overlay |
| Plate textures | brushed steel, diamond tread (rack plates), stamped sheet (hang-tags) | Procedural SVG/noise until real textures ship |

## 4. Motion

| Token | Value |
|---|---|
| `--dur-micro` | 200 ms (range 180–240) |
| `--dur-std` | 750 ms (range 600–900) |
| `--dur-cine` | 1300 ms (range 1.1–1.6 s) |
| `--stagger` | 55 ms (range 40–70) |
| `--ease-arrive` | `cubic-bezier(0.16, 1, 0.3, 1)` |
| `--ease-wipe` | `cubic-bezier(0.76, 0, 0.24, 1)` |
| `--ease-leave` | `cubic-bezier(0.7, 0, 0.84, 0)`, exit at about 65% of enter duration |
| Bounce | Only hanger sway (damped spring) and padlock rattle |
| Reduced motion | Lenis off, static parallax, no shake, sway or particles, frozen grain, 200 ms fades |

## 5. Layering (z-index)

`scene-far 0 · scene-mid 10 · scene-near 20 · racks 30 · avatar 40 · hud 50 · tooltip 60 · cart-bar 70 · modal 80 · transition 90 · loader 100 · cursor 110 · grain 120 (pointer-events none)`

## 6. Mockup notes that affect tokens

- Cart badge: circular in the mockup. The brief lists circular badges as an automatic fail, so the proposal is a chamfered square (`--chamfer-xs`).
- LB / RB plates beside the top bar read as gamepad shoulder-button hints.
- Warm Edison bulbs in the top-right rock: warm light belongs to the photographic plate only, never a CSS glow.
- Inventory 12/24 bar renders at about 35% fill in the mockup; the build computes it from data (50%).
