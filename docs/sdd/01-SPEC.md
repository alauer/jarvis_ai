# Palace Visual Reskin — SPEC

**Phase:** 1 — Requirements and Scope
**Date:** 2026-08-15
**Branch:** design/palace-visual-reskin
**Target file:** `server/hud/index.html` (single-file HUD, 885 lines)
**Parent repo commit:** `88998de8369e9d36f6d434b5e01feb93fcf1c33f`

---

## 1. Purpose & Scope

Transform the existing `jarvis_ai` Iron Man-themed HUD into an appearance that reads as **The Palace** — Jeeves's private command center. This is a **visual-only reskin**: colors, typography, layout proportions, decorative elements, and cosmetic text labels. No functional behavior changes.

### What this covers
- CSS custom property palette replacement (obsidian/violet/pearl)
- Typography swap from Orbitron/Rajdhani to Palace-appropriate faces
- Panel clip-path geometry softening
- Header, footer, boot sequence, and status label text rebranding
- Canvas arc-reactor state color mapping to Palace palette
- Removal of scanline overlay, Iron Man visual chrome
- Hydrangea-inspired restrained ambient detail (CSS-only, no external assets)
- Responsive layout preservation for desktop, iPad, and narrow viewports
- Dark/light polish: subtle inner glow, fine engraved borders, smoked glass
- Anti-pattern and aesthetic guardrails documented below

### What this does NOT cover
- No new features, rooms, navigation modes, or state machines
- No Kitchen Table / Workshop / Library / Gallery mode switching
- No avatar/presence system changes
- No voice, chat, approval, barge-in, telemetry, or auth behavior changes
- No new endpoints, plugins, or server modifications
- No new runtime dependencies or CDN font loading
- No structural DOM refactoring (element IDs, event contracts preserved)
- No Ghost Vessel, Live2D, ElevenLabs procurement, or memory viewer

---

## 2. Design Principles

1. **Presence first, controls second, telemetry third.** The Palace is a home for a continuous presence, not a SaaS admin panel.
2. **Restrained opulence.** Dark lacquer, fine engraved borders, subtle depth. Never garish, never cluttered.
3. **Purple is hierarchy and energy, not decoration.** Amethyst/plum/violet accents mark importance and state. The foundation is obsidian/charcoal.
4. **Calmer, not quieter.** All existing functions remain reachable. The page feels more intentional and composed.
5. **Coherent material language.** Smoked glass, soft depth, engraved edges — a unified surface vocabulary, not "the existing HUD with purple."

---

## 3. Visual Identity

### Emotional register
A private home for a powerful continuous presence. Intimate command-center elegance. Slightly occult server-shrine energy. Unmistakably The Palace.

### Anti-registers (explicitly rejected)
- SaaS admin panel
- Gamer HUD / Tony Stark cosplay
- Cyberpunk neon terminal
- Wedding invitation / grandmother's sitting room
- Iron Man arc-reactor bunker

---

## 4. Palette Direction

### Foundation
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Page background | `--bg` | `#06040a` | Deep obsidian with barely-visible warm undertone |
| Panel background | `--panel` | `#0e0a14dd` | Dark lacquer with transparency |
| Panel border | `--line` | `#2a1f35` | Muted violet-charcoal engraved edge |
| Elevated surface | `--surface` | `#14101c` | Slightly lifted panel variant |

### Accents (hierarchy palette)
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Primary accent | `--amethyst` | `#9b6dff` | Amethyst — headings, active states, key highlights |
| Secondary accent | `--plum` | `#c084fc` | Plum — secondary emphasis, subtle highlights |
| Tertiary accent | `--violet-glow` | `#7c3aed` | Deep violet for glows and shadows |

### Text
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Primary text | `--txt` | `#d8d0e8` | Pearl — highly legible on dark |
| Secondary text | `--txt-dim` | `#7a6f8a` | Lavender-mist — supporting text, labels |
| Emphasis text | `--txt-bright` | `#f0ecf8` | Near-white — for headings, key values |

### State / Functional
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Success / Online | `--ok` | `#a78bfa` | Violet for online/success states |
| Warning | `--warn` | `#d4a574` | Muted copper — warnings (not amber) |
| Danger / Error | `--err` | `#e8797f` | Muted rose — errors (not hot red) |
| Active state | `--active` | `#c084fc` | Plum — active/recording/engaged |
| Hydrangea bloom | `--bloom` | `#8b5cf6` | Decorative accent, used sparingly |

### Hydrangea motif
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Hydrangea base | `--hydrangea` | `#7c3aed` | Restrained violet for watermark/pattern |
| Hydrangea highlight | `--hydrangea-hi` | `#a78bfa` | Lighter for subtle depth variation |

### Ambient / Decorative
| Role | Token | Hex | Description |
|------|-------|-----|-------------|
| Soft glow | `--glow` | `#7c3aed22` | Ambient violet glow for borders/shadows |
| Inner glow | `--inner-glow` | `#7c3aed0d` | Very subtle inner luminance |
| Border highlight | `--border-hi` | `#9b6dff33` | Amethyst border highlight on focus/hover |

---

## 5. Typography Direction

### Display / Headings
**Primary choice:** Use system serif stack with fallback — no external CDN dependency.
```
font-family: 'Georgia', 'Palatino Linotype', 'Book Antiqua', Palatino, serif;
```
For identity/header: elegant, composed, not sci-fi. Georgia is universally available and reads as intentional, not default.

### Body / Operational text
**Primary choice:** Keep Rajdhani (already loaded from Google Fonts in the repo) — it is elegant, legible, and Palace-appropriate. No change needed.
```
font-family: 'Rajdhani', 'Segoe UI', system-ui, sans-serif;
```

### Monospace / Data
**Primary choice:** System monospace stack — no dependency.
```
font-family: 'SF Mono', 'Cascadia Code', 'Fira Code', 'Consolas', monospace;
```

### Label / Panel headers
Replace Orbitron (sci-fi angular) with Georgia for panel headings. Georgia at small sizes with letter-spacing reads as engraved/ceremonial.

---

## 6. Material Language

| Property | Current | Palace |
|----------|---------|--------|
| Border style | 1px solid `--line` | 1px solid `--line` with subtle inner glow |
| Panel clip-path | Sharp angled corners | Softened: 20px radius equivalent |
| Backgrounds | Flat with transparency | Subtle radial gradient depth |
| Glow effect | Cyan `box-shadow` | Violet `box-shadow` with reduced intensity |
| Scanlines | `body::after` repeating gradient | **Removed** |
| Depth | Flat panels | Subtle inset shadow for depth |
| Focus states | Cyan border | Amethyst border with soft glow |

---

## 7. Composition Rules

1. **Header:** Palace identity text. No Iron Man branding.
2. **Center:** Presence/interaction zone. State indicator visible.
3. **Left column:** Information panels. Calm, not alarming.
4. **Right column:** Telemetry panels. Supportive, not dominant.
5. **Footer:** Restrained attribution. "Property of the Mistress of Memory" or "J.Ai · The Palace" where compositionally appropriate — not repeated as decoration.
6. **Boot sequence:** Palace-appropriate greeting. No "WEAPONS OFFLINE" or "J.A.R.V.I.S" branding.

---

## 8. Interaction State Visual Table

| State | Reactor Color | Glow | Label | Visual Treatment |
|-------|--------------|------|-------|-----------------|
| Standby | Amethyst `--amethyst` | Low | STANDBY | Gentle pulse, calm |
| Listening | Plum `--plum` | Medium | LISTENING | Responsive pulse |
| Thinking | Violet `--bloom` | Medium | PROCESSING | Animated rings |
| Tool Use | Violet `--bloom` | High | WORKING | Active rings |
| Speaking | Amethyst `--amethyst` | High | SPEAKING | Glowing rings |
| Error | Rose `--err` | Low | ERROR | Dim, minimal motion |

---

## 9. Anti-Patterns (NOT building)

- ❌ Cyan or teal anywhere in the final UI
- ❌ Neon glow as primary decoration
- ❌ "JARVIS", "IRON MAN", "ARC REACTOR", "HERMES NEURAL INTERFACE" branding
- ❌ Giant rotating reactor as centerpiece with attention theft
- ❌ Scanline overlays
- ❌ Bright red as default status color
- ❌ Gaming/sci-fi reticles
- ❌ Circuit-board texture patterns
- ❌ Floral wallpaper or grandmother's sitting room
- ❌ Purple-for-cyan substitution (must read as coherent material reskin, not color swap)
- ❌ Runtime CDN dependencies for fonts
- ❌ DOM restructuring beyond cosmetic wrappers
- ❌ New JavaScript logic or event handling

---

## 10. Responsive Breakpoints

| Breakpoint | Layout | Treatment |
|------------|--------|-----------|
| >880px | 3-column grid (320px / 1fr / 320px) | Full desktop layout |
| ≤880px | Single column stack | Header sticky, panels stacked, reduced gaps |
| ≤480px | Narrow mobile | Further reduced sizes, full-width panels |

All breakpoints must preserve:
- Header visibility and clock
- Ring/presence indicator (resized)
- Chat feed and input
- All panel content (scrollable)
- Approval cards (centered, readable)
- Viewer overlay (full-screen)

---

## 11. Accessibility Requirements

- **Contrast:** All text on dark backgrounds must meet WCAG AA (4.5:1 for normal text, 3:1 for large text). Pearl `#d8d0e8` on obsidian `#06040a` = 11.2:1 ✓
- **Focus states:** Visible keyboard focus ring using amethyst accent
- **prefers-reduced-motion:** Reduce or eliminate animations; keep state labels readable
- **Semantic HTML:** Preserve all existing `<button>`, `<input>`, ARIA patterns
- **No color-only status:** State indicated by text label + color, not color alone
- **Touch targets:** All buttons minimum 44×44px tap area

---

## 12. Acceptance Criteria

- [ ] No cyan, teal, or neon colors anywhere in the rendered output
- [ ] Georgia-based headings read as intentional serif, not default fallback
- [ ] Rajdhani body text retained and legible
- [ ] All 10 panels visible with correct content
- [ ] Reactor ring uses amethyst/violet palette
- [ ] Scanline overlay completely removed
- [ ] Boot sequence shows Palace greeting (no Iron Man text)
- [ ] Header shows Palace branding
- [ ] Footer shows restrained attribution
- [ ] Mobile layout (≤880px) stacks correctly
- [ ] All interactive controls reachable by keyboard
- [ ] Visible focus ring on buttons and inputs
- [ ] Console free of errors on load
- [ ] No new DOM elements that break existing JS selectors
- [ ] All existing element IDs preserved
- [ ] No new runtime dependencies added
- [ ] No functional behavior changes in JS or Python

---

## 13. Open Questions

**Resolved during authoring:**
- [x] Fonts: Use Georgia (system serif) + existing Rajdhani — no new dependencies
- [x] Hydrangea motif: CSS-only radial gradient watermark — no external assets
- [x] Boot text: Replace with Palace-appropriate greeting
- [x] Footer attribution: "J.Ai · The Palace" — single instance
- [x] Canvas colors: Map STATE_STYLE to Palace accent palette
- [x] Mobile: Preserve existing breakpoints, update colors only

---

*SPEC complete. Proceed to DESIGN phase.*
