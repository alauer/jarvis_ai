# Palace Visual Reskin — IMPLEMENTATION

**Phase:** 3 — File-by-File Implementation Plan
**Date:** 2026-08-15
**Branch:** design/palace-visual-reskin
**Target:** `server/hud/index.html` (single-file HUD)

---

## 1. Implementation Strategy

The entire visual reskin targets **one file**: `server/hud/index.html`. Changes are organized into three logical zones within that file:

| Zone | Lines (approx) | Changes |
|------|----------------|---------|
| CSS (`<style>`) | 1-235 | Replace tokens, remove scanlines, update all selectors |
| HTML (`<body>`) | 236-359 | Update text labels, branding, boot text |
| JavaScript | 361-883 | Update STATE_STYLE colors, boot text, branding strings |

---

## 2. File-by-File Change Plan

### 2.1 `server/hud/index.html` — CSS Zone (Lines 1-235)

#### 2.1.1 Root tokens (Lines 14-18)
**Before:**
```css
:root{
  --bg:#050b14; --panel:#081523cc; --line:#0e2c40;
  --cyan:#00e5ff; --cyan-dim:#0a7f96; --teal:#19f0d8;
  --amber:#ffb300; --red:#ff4d5e; --txt:#9fd8e8; --txt-dim:#4d7d92;
}
```
**After:**
```css
:root{
  --bg:#06040a; --panel:#0e0a14dd; --line:#2a1f35; --surface:#14101c;
  --amethyst:#9b6dff; --plum:#c084fc; --violet-glow:#7c3aed;
  --txt:#d8d0e8; --txt-dim:#7a6f8a; --txt-bright:#f0ecf8;
  --ok:#a78bfa; --warn:#d4a574; --err:#e8797f;
  --active:#c084fc; --bloom:#8b5cf6;
  --hydrangea:#7c3aed; --hydrangea-hi:#a78bfa;
  --glow:#7c3aed22; --inner-glow:#7c3aed0d; --border-hi:#9b6dff33;
}
```
**Rationale:** Complete palette replacement. Remove all cyan/teal references.

#### 2.1.2 Body + scanlines (Lines 21-28)
**Before:**
```css
body{
  background:radial-gradient(ellipse at 50% 38%, #0a1a2c 0%, var(--bg) 65%);
  color:var(--txt); font-family:'Rajdhani',sans-serif; overflow:hidden;
}
body::after{ /* scanlines */
  content:""; position:fixed; inset:0; pointer-events:none; z-index:9;
  background:repeating-linear-gradient(0deg, transparent 0 2px, #00e5ff05 2px 4px);
}
```
**After:**
```css
body{
  background:radial-gradient(ellipse at 50% 38%, #0c0814 0%, var(--bg) 65%);
  color:var(--txt); font-family:'Rajdhani',sans-serif; overflow:hidden;
}
```
**Rationale:** Remove scanline overlay. Update gradient color from cyan-tinted to violet-tinted.

#### 2.1.3 Header (Lines 30-37)
Replace Orbitron with Georgia throughout header. Update colors.

#### 2.1.4 Panel styles (Lines 39-51)
Update border colors, add inner glow, soften clip-path.

#### 2.1.5 Reactor center (Lines 55-63)
Update font from Orbitron to Georgia for state labels.

#### 2.1.6 Messages (Lines 68-71)
Replace cyan border with amethyst border on `.msg.jarvis`.

#### 2.1.7 Chat input (Lines 72-77)
Update background, focus border, and glow colors.

#### 2.1.8 Buttons (Lines 78-85)
Replace all cyan references with amethyst. Update backgrounds.

#### 2.1.9 Approval cards (Lines 88-94)
Update amber colors to `--warn`.

#### 2.1.10 Viewer overlay (Lines 95-114)
Replace all cyan references with amethyst. Update box-shadow and border colors.

#### 2.1.11 Boot sequence (Lines 116-136)
Update boot logo color, remove scanline on boot overlay.

#### 2.1.12 Holographic panels (Lines 138-201)
Replace all cyan references with amethyst. Update glow colors.

#### 2.1.13 Mobile responsive (Lines 203-222)
Preserve breakpoints, no color changes needed in media query itself.

#### 2.1.14 Footer (Lines 229-234)
Update bar gradient colors.

#### 2.1.15 New additions
- Add `@media (prefers-reduced-motion: reduce)` block
- Add `:focus-visible` styles
- Add `.kv b` color update (teal → ok/amethyst)

---

### 2.2 `server/hud/index.html` — HTML Zone (Lines 236-359)

| Line | Current | New | Change Type |
|------|---------|-----|-------------|
| 6 | `<title>JARVIS</title>` | `<title>The Palace</title>` | Branding |
| 9 | `content="JARVIS"` (PWA title) | `content="The Palace"` | Branding |
| 10 | `content="#050b14"` (theme-color) | `content="#06040a"` | Meta |
| 240 | "ACCESS CODE" text | "ACCESS CODE" (unchanged) | — |
| 247 | `J.A.R.V.I.S` | `THE PALACE` | Branding |
| 248 | `HERMES NEURAL INTERFACE` | `J.Ai · COMMAND CENTER` | Branding |
| 253 | `J.A.R.V.I.S` | `THE PALACE` | Branding |
| 254 | `HERMES AGENT INTERFACE` | `J.Ai · THE PALACE` | Branding |
| 301 | `"Type to Hermes…"` | `"Type to Hermes… (unchanged functional hint)"` | Keep |
| 357 | `NOUS HERMES AGENT v0.16` | `J.Ai · The Palace` | Branding |
| 355 | empty span | `Property of the Mistress of Memory` | Branding |

**NO other HTML changes.** All element IDs, event attributes (`onclick`), and DOM structure preserved exactly.

---

### 2.3 `server/hud/index.html` — JavaScript Zone (Lines 361-883)

#### 2.3.1 STATE_STYLE (Lines 381-388)
**Before:**
```javascript
const STATE_STYLE={
  standby:{speed:.15,color:"#00e5ff",glow:18,pulse:0},
  listening:{speed:.5,color:"#19f0d8",glow:30,pulse:1},
  thinking:{speed:1.6,color:"#ffb300",glow:26,pulse:.4},
  tool:{speed:2.4,color:"#ffb300",glow:32,pulse:.6},
  speaking:{speed:.7,color:"#00e5ff",glow:34,pulse:.8},
  error:{speed:.05,color:"#ff4d5e",glow:22,pulse:0},
};
```
**After:**
```javascript
const STATE_STYLE={
  standby:{speed:.15,color:"#9b6dff",glow:18,pulse:0},
  listening:{speed:.5,color:"#c084fc",glow:30,pulse:1},
  thinking:{speed:1.6,color:"#8b5cf6",glow:26,pulse:.4},
  tool:{speed:2.4,color:"#8b5cf6",glow:32,pulse:.6},
  speaking:{speed:.7,color:"#9b6dff",glow:34,pulse:.8},
  error:{speed:.05,color:"#e8797f",glow:22,pulse:0},
};
```
**Rationale:** Map all state colors to Palace accent palette. Speed and pulse values unchanged.

#### 2.3.2 Boot lines (Lines 843-847)
**Before:**
```javascript
const BOOT_LINES=[
  ["INITIALIZING NEURAL INTERFACE",380],["LOADING HUD MODULES",300],
  ["CONNECTING HERMES CORE",650],["VOICE LINK ESTABLISHED",420],
  ["MEMORY SYSTEMS SYNCHRONIZED",420],["WEAPONS OFFLINE. KETTLE ONLINE.",300],
  ["ALL SYSTEMS NOMINAL",550],
];
```
**After:**
```javascript
const BOOT_LINES=[
  ["INITIALIZING PALACE INTERFACE",380],["LOADING COMMAND MODULES",300],
  ["CONNECTING HERMES CORE",650],["VOICE LINK ESTABLISHED",420],
  ["MEMORY SYSTEMS SYNCHRONIZED",420],["THE PALACE IS ONLINE",300],
  ["ALL SYSTEMS NOMINAL",550],
];
```
**Rationale:** Replace Iron Man references with Palace-appropriate text. "WEAPONS OFFLINE. KETTLE ONLINE." → "THE PALACE IS ONLINE."

#### 2.3.3 Holo panel title default (Line 766)
**Before:** `"INCOMING FEED"`
**After:** `"INCOMING"` (minor text change, functional semantics unchanged)

#### 2.3.4 System message (Line 882)
**Before:** `"Jarvis HUD online. Click the ring or press Space to talk."`
**After:** `"The Palace is online. Click the ring or press Space to talk."`

**NO other JavaScript changes.** All WebSocket handling, audio processing, widget refresh, and event logic remains identical.

---

## 3. Baseline Screenshots

Before implementation, capture:
1. Desktop viewport (1920×1080) — full 3-column layout
2. Mobile viewport (375×812) — stacked layout
3. Boot sequence (press B)
4. Viewer overlay (click KANBAN)

Store under: `docs/review/baseline/`

---

## 4. Verification Matrix

| Check | Method | Pass Criteria |
|-------|--------|---------------|
| No cyan/teal in CSS | `grep -c '#00e5ff\|#19f0d8\|#0a7f96\|#0e2c40'` | 0 matches |
| No Orbitron in CSS | `grep -c "Orbitron"` | 0 matches in style rules (may remain in font-family for backwards compat if needed, but we remove it) |
| All element IDs preserved | `diff <original IDs> <new IDs>` | Identical set |
| Boot text updated | Visual check | "THE PALACE" visible |
| Header text updated | Visual check | "THE PALACE" in header |
| Reactor colors changed | Visual check | Amethyst/violet, not cyan |
| Scanlines removed | Visual check | No horizontal line pattern |
| Focus styles present | Tab through controls | Visible amethyst outline |
| Reduced motion | `@media (prefers-reduced-motion)` | Animations suppressed |
| Mobile layout works | Resize to 375px | Panels stack, all content accessible |
| Console clean | Browser DevTools | No errors on load |
| No new DOM elements | Diff check | Only text content changes |
| No JS logic changes | Diff check | Only string/color values changed |
| `git diff --check` | Terminal | No whitespace errors |

---

## 5. Known Constraints

1. **Google Fonts link stays** for Rajdhani — it is already in the repo and provides the body font. We remove the Orbitron load.
2. **Canvas arc-reactor ring** remains as the presence indicator. Only colors change. Future phases may replace with avatar/presence.
3. **Holographic panel animations** retain their complexity (holoApproach, holoDismiss, etc.) — only color references change.
4. **PWA meta tags** update to "The Palace" branding.

---

## 6. Commit Strategy

1. **Commit 1:** `docs(sdd): Palace visual reskin specification` — SDD files only
2. **Commit 2:** `feat(hud): Palace visual reskin — appearance-only customization` — All HUD changes

---

*IMPLEMENTATION plan complete. Ready to execute.*
