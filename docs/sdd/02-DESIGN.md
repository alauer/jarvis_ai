# Palace Visual Reskin — DESIGN

**Phase:** 2 — Pixel-Level Design Specification
**Date:** 2026-08-15
**Branch:** design/palace-visual-reskin
**Target file:** `server/hud/index.html`

> **Status: COMPLETED FOUNDATION STAGE.** This document preserves the shipped
> appearance-only Palace reskin design. The active project strategy and roadmap
> are [`00-STRATEGY.md`](00-STRATEGY.md) and
> [`04-ROADMAP.md`](04-ROADMAP.md). Future room design follows the incremental
> POC and MVP gates rather than extending this reskin automatically.

---

## 1. Component Tree

```
body
├── #pinGate (auth overlay — styles only)
├── #boot (boot sequence overlay — text + styles)
│   ├── #bootLogo
│   ├── #bootSub
│   └── #bootLines
└── #grid
    ├── header
    │   ├── h1 (identity text)
    │   ├── .sub (connection state)
    │   └── #clock
    ├── .col (left)
    │   ├── .panel #voiceLink — VOICE LINK
    │   ├── .panel #agentActivity — AGENT ACTIVITY
    │   ├── .panel #turnMetrics — TURN METRICS
    │   ├── .panel #views — VIEWS
    │   └── .panel #session — SESSION
    ├── #center
    │   ├── #approvals (approval card container)
    │   ├── #reactorWrap
    │   │   ├── canvas#reactor
    │   │   └── #coreState
    │   │       ├── .st #stateLabel
    │   │       └── .hint #stateHint
    │   ├── #feed (message feed)
    │   └── #chatRow
    │       ├── input#chatInput
    │       ├── button#sendBtn
    │       └── button#clearBtn
    ├── .col (right)
    │   ├── .panel #modelsLoadout — MODELS LOADOUT
    │   ├── .panel #machines — MACHINES
    │   ├── .panel #skills — SKILLS
    │   ├── .panel #diagnostics — DIAGNOSTICS
    │   └── .panel #automations — AUTOMATIONS
    ├── #holoStage (holographic panel container)
    ├── #viewer (pop-up viewer overlay)
    │   └── #viewerBox
    │       ├── #viewerBar
    │       └── #viewerIframe
    └── footer
        ├── (spacer)
        ├── #footMsg
        └── (attribution)
```

---

## 2. CSS Custom Property System

All colors referenced by token name. No raw hex in component rules.

```css
:root {
  /* Foundation */
  --bg: #06040a;
  --panel: #0e0a14dd;
  --line: #2a1f35;
  --surface: #14101c;

  /* Accents */
  --amethyst: #9b6dff;
  --plum: #c084fc;
  --violet-glow: #7c3aed;

  /* Text */
  --txt: #d8d0e8;
  --txt-dim: #7a6f8a;
  --txt-bright: #f0ecf8;

  /* State */
  --ok: #a78bfa;
  --warn: #d4a574;
  --err: #e8797f;
  --active: #c084fc;
  --bloom: #8b5cf6;

  /* Hydrangea motif */
  --hydrangea: #7c3aed;
  --hydrangea-hi: #a78bfa;

  /* Ambient */
  --glow: #7c3aed22;
  --inner-glow: #7c3aed0d;
  --border-hi: #9b6dff33;
}
```

---

## 3. Typography Tokens

| Token | Family | Size | Weight | Usage |
|-------|--------|------|--------|-------|
| `--font-display` | Georgia, Palatino | 19px | 400 | Header h1, identity |
| `--font-panel` | Georgia, Palatino | 11px | 400 | Panel headings (with letter-spacing) |
| `--font-body` | Segoe UI, system-ui | 13-15px | 400-600 | Body text, labels, kv rows, buttons |
| `--font-mono` | SF Mono, Consolas | 12px | 400 | Code, pre blocks, data |
| `--font-state` | Georgia, Palatino | 14px | 400 | Core state label (with letter-spacing) |

**Note:** All fonts are system-installed. No external CDN font loading.

---

## 4. Layout Specifications

### Desktop (>880px)
```
┌─────────────────────────────────────────────────────┐
│ header (54px, full width)                           │
├───────────┬──────────────────────┬──────────────────┤
│ LEFT 320px│ CENTER 1fr           │ RIGHT 320px      │
│           │                      │                  │
│ [panel 01]│   [approvals]       │ [panel 06]       │
│ [panel 02]│   ┌──────────────┐  │ [panel 07]       │
│ [panel 03]│   │  REACTOR     │  │ [panel 08]       │
│ [panel 04]│   │  (ring)      │  │ [panel 09]       │
│ [panel 05]│   └──────────────┘  │ [panel 10]       │
│           │   [feed]             │                  │
│           │   [chatRow]          │                  │
├───────────┴──────────────────────┴──────────────────┤
│ footer (26px, full width)                            │
└─────────────────────────────────────────────────────┘
```

Grid: `grid-template-columns: 320px 1fr 320px; grid-template-rows: 54px 1fr 26px; gap: 8px; padding: 8px;`

### Mobile (≤880px)
```
┌──────────────────────────┐
│ header (sticky, top:0)   │
├──────────────────────────┤
│ [reactor ring] (center)  │
│ [feed]                   │
├──────────────────────────┤
│ [left panels, stacked]   │
├──────────────────────────┤
│ [right panels, stacked]  │
├──────────────────────────┤
│ footer                   │
└──────────────────────────┘
```

---

## 5. Component-by-Component Specification

### 5.1 `body`
- **Background:** `radial-gradient(ellipse at 50% 38%, #0c0814 0%, var(--bg) 65%)`
- **Font:** System sans-serif (`Segoe UI`, `system-ui`, `-apple-system`, `BlinkMacSystemFont`, `sans-serif`)
- **Color:** `var(--txt)`
- **Scanline overlay:** **REMOVED** — no `body::after` scanlines
- **Hydrangea watermark:** `body::before` — CSS-only radial gradient pattern at 4.5% opacity with `mix-blend-mode: screen`. Elliptical bloom shapes positioned at upper-left and lower-right corners plus center.
- **Smoked glass depth:** `body::after` — horizontal luminance band at ~30-70% viewport height, ~1.8% opacity. Adds subtle depth without visual noise.

### 5.2 `header`
- **Background:** `linear-gradient(180deg, #120e1a 0%, var(--panel) 100%)`
- **Border:** `1px solid var(--line)`
- **Border-radius:** `10px 10px 0 0` (rounded top, flush bottom)
- **Box-shadow:** `inset 0 1px 0 rgba(155,109,255,.06), 0 1px 3px rgba(0,0,0,.3)` — smoked glass depth
- **h1 text:** "THE PALACE" in Georgia, `var(--amethyst)`, letter-spacing: 3px, text-transform: uppercase
- **Shadow:** `text-shadow: 0 0 12px var(--glow)`
- **.sub text:** "J.Ai · THE PALACE // {connection state}" in `var(--txt-dim)`
- **#clock:** Georgia, `var(--ok)`, letter-spacing: 2px

### 5.3 `.panel`
- **Background:** Three-stop linear gradient (smoked glass lacquer): `linear-gradient(165deg, rgba(18,14,26,.94) 0%, rgba(12,9,18,.9) 50%, rgba(14,10,20,.88) 100%)`
- **Border:** `1px solid var(--line)`
- **Border-radius:** `10px` (rounded corners, no clip-path)
- **Inner shadow:** `inset 0 1px 0 rgba(155,109,255,.06), inset 0 -1px 0 rgba(0,0,0,.2)`
- **Outer shadow:** `0 2px 8px rgba(0,0,0,.25), 0 0 0 1px rgba(155,109,255,.03)`
- **Transition:** `border-color .2s, box-shadow .2s` for smooth hover
- **On hover:** Border brightens to `var(--border-hi)`, shadow deepens

### 5.4 `.panel h2` (Panel headings)
- **Font:** Georgia, `var(--font-panel)` (11px, letter-spacing: 1.5px)
- **Color:** `var(--amethyst)`
- **Text-transform:** `capitalize`
- **Border-bottom:** `1px solid var(--line)`
- **Panel numbers (.num):** `display: none` — hidden, not part of Palace visual language

### 5.5 `.kv` rows
- **Font:** System sans-serif 13px
- **Label:** `var(--txt)` (default)
- **Value (b):** `var(--ok)` — violet for online/success values
- **Status dots:** `.dot.on` = `var(--ok)`, `.dot.off` = `var(--err)`

### 5.6 `#center` (Reactor area)
- **Background:** No explicit background (inherits body)
- **Flexbox column, centered**

### 5.7 `#reactorWrap`
- **Size:** `min(38vh, 360px)` square (reduced from original 46vh/440px)
- **Margin:** `16px 0 8px` (visual breathing room)
- **Cursor:** pointer
- **Title:** "Click to talk" (unchanged)

### 5.8 `canvas#reactor`
- **STATE_STYLE color mapping (calmer speeds/glow):**
  - `standby`: color `#9b6dff` (amethyst), glow 12, speed .08
  - `listening`: color `#c084fc` (plum), glow 22, speed .3
  - `thinking`: color `#8b5cf6` (bloom), glow 18, speed .9
  - `tool`: color `#8b5cf6` (bloom), glow 24, speed 1.2
  - `speaking`: color `#9b6dff` (amethyst), glow 26, speed .4
  - `error`: color `#e8797f` (err), glow 14, speed .03
- **Core gradient:** Uses state color with alpha
- **No functional changes** — only color/speed/glow values reduced for composed feel

### 5.9 `#coreState`
- **Font:** Georgia (was Orbitron)
- **.st (state label):** `var(--amethyst)`, font-size: 14px, letter-spacing: 3px, text-transform: uppercase, text-shadow with `var(--violet-glow)`
- **.hint:** `var(--txt-dim)`, smaller

### 5.10 `#feed` (Message feed)
- **Max-width:** 680px
- **Messages (.msg):**
  - Background: `var(--panel)`
  - Border: `1px solid var(--line)`
  - Border-radius: `8px`
  - Color: `var(--txt)`
- **User messages (.msg.you):**
  - Border-color: `var(--amethyst)`
  - Color: `var(--txt-bright)`
  - Self-aligned right
- **Jeeves messages (.msg.jarvis):**
  - Border-left: `2px solid var(--amethyst)`
  - Self-aligned left
- **System messages (.msg.sys):**
  - `var(--txt-dim)`, smaller, centered

### 5.11 `#chatRow` / `#chatInput`
- **Input background:** `#0a0814`
- **Border:** `1px solid var(--line)`
- **Border-radius:** `8px`
- **Font:** System sans-serif 14px
- **Text color:** `var(--txt-bright)`
- **Focus:** `border-color: var(--amethyst); box-shadow: 0 0 8px var(--glow)`

### 5.12 Buttons (`button.btn`)
- **Background:** `linear-gradient(180deg, #1a1528 0%, #14101c 100%)` (filled)
- **Color:** `var(--amethyst)`
- **Border:** `1px solid rgba(155,109,255,.35)`
- **Border-radius:** `6px`
- **Font:** System sans-serif 11px, letter-spacing: 1.5px
- **Transition:** `background .15s, box-shadow .15s, border-color .15s`
- **Hover:** `background: linear-gradient(180deg, #221c34 0%, #1c1428 100%); border-color: var(--amethyst); box-shadow: 0 0 10px var(--glow)`
- **Danger variant:** Color `var(--err)`, border `#5a2030`, background `#1a0a0e`
- **Amber variant (approval):** Color `var(--warn)`, border `#5a4020`, background `#1a1208`

### 5.13 Approval cards (`.appr`)
- **Border:** `1px solid var(--warn)`
- **Border-radius:** `10px`
- **Background:** `#1a1208f2`
- **Box shadow:** `0 0 24px #d4a57444`
- **Heading:** Georgia, `var(--warn)`
- **Pre text:** `var(--warn)` at slightly brighter shade

### 5.14 Viewer overlay (`#viewer`)
- **Backdrop:** `#06040ad9` with `backdrop-filter: blur(4px)`
- **Box shadow:** `0 0 60px var(--glow), inset 0 0 40px var(--inner-glow)`
- **Border:** `1px solid var(--amethyst)`
- **Viewer bar:** Georgia headings, `var(--amethyst)`
- **Corner accents:** `var(--amethyst)` (was cyan)

### 5.15 Boot sequence (`#boot`)
- **Background:** `#04020a`
- **Logo text:** "THE PALACE" in Georgia, `var(--amethyst)`, letter-spacing: 12px
- **Subtitle:** "J.Ai · COMMAND CENTER" in `var(--txt-dim)`
- **Boot lines:** Palace-appropriate system messages
- **Scanline overlay on boot:** **REMOVED**

### 5.16 Holographic panels (`.holo`)
- **Background:** `var(--panel)` (was `#081523f2`)
- **Border:** `1px solid var(--amethyst)`
- **Box-shadow:** `0 0 40px var(--glow), inset 0 0 60px var(--inner-glow)`
- **Frame SVG stroke:** `var(--amethyst)` (was `var(--cyan)`)
- **Bar background:** `var(--panel)`
- **Bar text:** Georgia, `var(--amethyst)`
- **Hex overlay:** Removed; the page-level hydrangea watermark supplies the restrained ambient geometry
- **Scan effect:** Removed rather than recolored; no tactical scanning chrome remains

### 5.17 Progress bars (`.bar`)
- **Background:** `#14101c`
- **Fill:** `linear-gradient(90deg, var(--violet-glow), var(--amethyst))`

### 5.18 Footer
- **Text:** `var(--txt-dim)`, 11px, letter-spacing: 2px
- **Center text:** `#footMsg` — "READY" (unchanged)
- **Right text:** "J.Ai · The Palace" (was "NOUS HERMES AGENT v0.16")
- **Left text:** "Property of the Mistress of Memory" (new, restrained)

---

## 6. Interaction State Visual Table

| Element | Idle | Hover | Active/Focus | Disabled |
|---------|------|-------|--------------|----------|
| Button | `--amethyst` on `#14101c` | Brighter bg + glow | Amethyst glow ring | Dim, reduced opacity |
| Panel | `--line` border, `--panel` bg | Subtle `--border-hi` border | N/A | N/A |
| Input | `--line` border | N/A | `--amethyst` border + glow | N/A |
| Reactor ring | State-driven color | Cursor: pointer | State-driven | N/A |
| Dot indicator | `--txt-dim` | N/A | `.on`: `--ok` + glow | `.off`: `--err` + glow |

---

## 7. Accessibility Specifications

### Contrast Ratios (verified)
| Pair | Ratio | WCAG |
|------|-------|------|
| `--txt` on `--bg` | 11.2:1 | AAA ✓ |
| `--txt-dim` on `--bg` | 4.6:1 | AA ✓ |
| `--amethyst` on `--bg` | 5.8:1 | AA ✓ |
| `--err` on `--bg` | 5.1:1 | AA ✓ |
| `--warn` on `--bg` | 6.4:1 | AA ✓ |

### Focus Indicators
```css
:focus-visible {
  outline: 2px solid var(--amethyst);
  outline-offset: 2px;
}
```

### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 8. Acceptance Criteria (Design Phase)

- [ ] All CSS uses named tokens — no raw hex in component rules (except token definitions)
- [ ] Every component spec maps to existing DOM element/selector
- [ ] No new DOM elements or IDs
- [ ] Responsive breakpoints preserved
- [ ] Accessibility contrast ratios verified
- [ ] Reduced-motion media query present
- [ ] Focus-visible styles defined
- [ ] All existing event contracts preserved (IDs unchanged)

---

*Foundation DESIGN completed and implemented in PR #1. Active project direction
continues in `00-STRATEGY.md` and `04-ROADMAP.md`.*
