---
name: ifs-design-skill
description: >
  Design system skill for building UI screens and components that match the IFS Resolve
  application — an AI-powered field maintenance and fault-intelligence platform for
  industrial, energy, and aviation environments. Use whenever building any Resolve-branded
  artifact: mobile screens, tablet layouts, desktop dashboards, or individual components
  (headers, fault cards, capture modes, audio analysis, conversational AI, query bars,
  action modals). Covers all three capture modes: Video & Image, Audio & Voice, and Text.
assets:
  - assets/resolve-logo.svg           # Standalone starburst logo mark (48×48)
  - assets/resolve-header-mobile.svg  # Full header bar — mobile (390×64)
  - assets/resolve-header-desktop.svg # Full header bar — desktop (1440×72)
---

# IFS Resolve — Design System

## 1. Overview & Philosophy

Resolve is a **field-first, AI-powered** fault-reporting and maintenance intelligence
platform built by IFS. It operates in noisy, gloved-hand, eyes-busy environments —
wind farms, aircraft hangars, industrial plants — where **typing is not the primary
option**. Every design decision must reinforce speed, legibility at a glance, and
zero-friction capture.

### The three capture modes — always present as a top-level tab switcher

| Mode | Tab Label | Primary Action | When to Lead With |
|---|---|---|---|
| **Video & Image** | `Video & Image` | Camera / photo snap | Visual faults: leaks, cracks, physical damage |
| **Audio & Voice** | `Audio & Voice` | Microphone record | Sound-based faults: chatter, knocking, vibration |
| **Text** | `Text` | Conversational chat | Complex descriptions, follow-up dialogue |

> **Design rule**: Text is the *third* tab, not the first. Video & Image always leads.
> The tab switcher appears at the top of every capture/analysis flow, rendered as a
> pill-group. The active tab is filled with the accent purple; inactive tabs are ghost.

### AI analysis pipeline — visual language

When the AI is processing any input, three things happen simultaneously and must be
reflected in the UI:

1. **Status headline** — "Analyzing Fault…" / "Analyzing Audio…" in monospace, top of screen
2. **Starburst icon spins** — top-right corner, replaces static logo during processing
3. **Floating annotation chips** emerge around the analysis view — extracted metadata
   rendered as pill-shaped labels that appear to "float" at the edges of the image/waveform

---

## 2. Colour Palette

### Foundations

| Token | Hex | Usage |
|---|---|---|
| `--color-bg` | `#0A0A0A` | App background, body fill |
| `--color-surface` | `#111111` | Cards, panels, modals |
| `--color-surface-raised` | `#1A1A1A` | Hover states, elevated cards |
| `--color-border` | `#1E1E1E` | Dividers, card borders |
| `--color-border-subtle` | `#2A2A2A` | Inner dividers, table rows |

### Text

| Token | Hex | Usage |
|---|---|---|
| `--color-text-primary` | `#FFFFFF` | Headlines, primary labels |
| `--color-text-secondary` | `#888888` | Subtext, metadata, placeholders |
| `--color-text-tertiary` | `#555555` | Disabled, timestamps |

### Accent — Purple / Violet (primary interactive)

| Token | Hex | Usage |
|---|---|---|
| `--color-accent` | `#7C3AED` | Primary buttons, active tab fill, submit |
| `--color-accent-bright` | `#9B5CF6` | Glow halos, focus rings, "Yes" inline button |
| `--color-accent-muted` | `#3B1F75` | Button hover overlays, active tab bg dark variant |
| `--color-accent-glow` | `rgba(124,58,237,0.25)` | Input glow, query bar aura |

### Accent — Recording / Alert Red

| Token | Hex | Usage |
|---|---|---|
| `--color-record` | `#EF4444` | Recording dot, active mic button border |
| `--color-record-bg` | `rgba(239,68,68,0.15)` | Mic button fill when recording |
| `--color-record-text` | `#F87171` | "Recording…" label text |

### Accent — Amber / Gold (severity: moderate)

| Token | Hex | Usage |
|---|---|---|
| `--color-severity-moderate` | `#D4A017` | "Moderate" badges |
| `--color-severity-moderate-bg` | `#2A1F00` | Badge background |

### Accent — Priority / Alert tags

| Token | Hex | Usage |
|---|---|---|
| `--color-priority-high` | `#F59E0B` | Priority 9 / high tags |
| `--color-priority-high-bg` | `#2D1F00` | Tag background |
| `--color-priority-low` | `#6B7280` | Priority 3 / low |
| `--color-success` | `#22C55E` | Checkmarks, resolved state |
| `--color-destructive` | `#EF4444` | Errors, critical faults |

### Waveform colours (Audio & Voice mode)

| Token | Hex | Usage |
|---|---|---|
| `--color-waveform-played` | `#CCCCCC` | Bars left of playhead (recorded audio) |
| `--color-waveform-unplayed` | `#333333` | Bars right of playhead (silence / future) |
| `--color-waveform-playhead` | `#EF4444` | Vertical playhead line |

### Full CSS Variable Block

```css
:root {
  /* Surfaces */
  --color-bg:                   #0A0A0A;
  --color-surface:              #111111;
  --color-surface-raised:       #1A1A1A;
  --color-border:               #1E1E1E;
  --color-border-subtle:        #2A2A2A;

  /* Text */
  --color-text-primary:         #FFFFFF;
  --color-text-secondary:       #888888;
  --color-text-tertiary:        #555555;

  /* Accent purple */
  --color-accent:               #7C3AED;
  --color-accent-bright:        #9B5CF6;
  --color-accent-muted:         #3B1F75;
  --color-accent-glow:          rgba(124, 58, 237, 0.25);

  /* Recording red */
  --color-record:               #EF4444;
  --color-record-bg:            rgba(239, 68, 68, 0.15);
  --color-record-text:          #F87171;

  /* Severity */
  --color-severity-moderate:    #D4A017;
  --color-severity-moderate-bg: #2A1F00;

  /* Priority */
  --color-priority-high:        #F59E0B;
  --color-priority-high-bg:     #2D1F00;
  --color-success:              #22C55E;
  --color-destructive:          #EF4444;

  /* Waveform */
  --color-waveform-played:      #CCCCCC;
  --color-waveform-unplayed:    #333333;
  --color-waveform-playhead:    #EF4444;
}
```

---

## 3. Typography

```css
/* Font stacks */
--font-ui:   'SF Pro Display', 'Inter', 'Helvetica Neue', Arial, sans-serif;
--font-mono: 'SF Mono', 'Fira Code', 'Consolas', monospace;

/* Scale */
--text-xs:   11px;   /* part numbers, serial numbers, timestamps */
--text-sm:   13px;   /* metadata, table cells, nav items */
--text-base: 15px;   /* body, card descriptions, chat messages */
--text-md:   17px;   /* section headers, AI response text */
--text-lg:   20px;   /* card titles */
--text-xl:   26px;   /* screen heading "Resolve" */
--text-2xl:  32px;   /* hero/status text: "Analyzing Fault…" */

/* Weights */
--weight-regular:  400;
--weight-medium:   500;
--weight-semibold: 600;
--weight-bold:     700;

/* Tracking */
/* Headings:        letter-spacing: -0.5px  */
/* Nav / labels:    letter-spacing:  0.1px  */
/* Monospace codes: letter-spacing:  0.05em */
/* Status text:     letter-spacing:  0.02em (slightly open, scan-friendly) */
```

> **Key rule**: Analysis status text ("Analyzing Fault…", "Analyzing Audio…",
> step labels like "Analyzing component structure") uses `--font-mono`. This
> reinforces the machine/AI context and distinguishes AI output from human UI copy.

---

## 4. Spacing & Layout Grid

```
Base unit: 4 px
--space-1:   4px
--space-2:   8px
--space-3:  12px
--space-4:  16px
--space-5:  20px
--space-6:  24px
--space-8:  32px
--space-10: 40px
--space-12: 48px
```

### Mobile (≤ 430 px)
- 1-column layout, full-bleed cards
- Horizontal padding: 20 px (16 px inside capture cards)
- Safe area: `env(safe-area-inset-*)` on all edges
- Bottom action bar: 80 px fixed
- Mode tab switcher: full-width, 3 equal-width tabs, 48 px tall

### Tablet (431–1024 px)
- 2-column card grid
- Horizontal padding: 32 px
- Side navigation panel: 240 px

### Desktop (≥ 1025 px)
- Fixed left sidebar: 240 px
- Main content max-width: 1120 px, centred
- Header bar: 72 px fixed top
- Content top padding: 88 px

---

## 5. Border Radius

```css
--radius-sm:   6px;    /* tags, badges, annotation chips */
--radius-md:  12px;    /* cards, inputs, waveform container */
--radius-lg:  20px;    /* modals, bottom sheets */
--radius-xl:  28px;    /* floating capture bar */
--radius-pill: 9999px; /* buttons, mode tabs, annotation pills */
```

---

## 6. Component Patterns

### 6.1 App Header — Mobile

The mobile header always shows "Resolve" wordmark left-aligned and the user
avatar icon (person silhouette in a circle) on the right. During AI analysis,
the avatar is replaced by or joined by the spinning starburst.

```html
<header class="resolve-header-mobile">
  <span class="wordmark">Resolve</span>
  <button class="avatar-btn" aria-label="Profile">
    <!-- person icon SVG -->
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor"
         stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
      <circle cx="12" cy="8" r="4"/>
      <path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/>
    </svg>
  </button>
</header>

<style>
.resolve-header-mobile {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
  height: 56px;
  background: var(--color-bg);
}
.wordmark {
  font-family: var(--font-ui);
  font-size: var(--text-xl);
  font-weight: var(--weight-bold);
  color: var(--color-text-primary);
  letter-spacing: -0.5px;
}
.avatar-btn {
  width: 40px; height: 40px;
  border-radius: 50%;
  background: var(--color-surface-raised);
  border: none;
  color: var(--color-text-primary);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
}
</style>
```

### 6.2 App Header — Desktop

```html
<header class="resolve-header-desktop">
  <div class="header-left">
    <span class="wordmark">Resolve</span>
    <nav>
      <a href="#">Faults</a>
      <a href="#">Reports</a>
      <a href="#">Fleet</a>
      <a href="#">Analytics</a>
    </nav>
  </div>
  <div class="header-right">
    <button class="btn-report-issue">+ Report an Issue</button>
    <!-- Starburst logo mark SVG (see Section 6.3) -->
  </div>
</header>

<style>
.resolve-header-desktop {
  position: fixed; top: 0; left: 0; right: 0;
  height: 72px;
  background: var(--color-bg);
  border-bottom: 1px solid var(--color-border);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 32px;
  z-index: 100;
}
.header-left { display: flex; align-items: center; gap: 40px; }
.header-left nav { display: flex; gap: 24px; }
.header-left nav a {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  text-decoration: none;
}
.header-left nav a:hover { color: var(--color-text-primary); }
.btn-report-issue {
  background: var(--color-accent);
  color: #fff;
  border: none;
  border-radius: var(--radius-pill);
  padding: 8px 16px;
  font-size: 12px;
  font-weight: var(--weight-medium);
  cursor: pointer;
}
</style>
```

### 6.3 Starburst Logo Mark (inline SVG)

```html
<!-- Static: use in header right slot -->
<!-- Animating: add class="starburst-loading" during AI analysis -->
<svg width="28" height="28" viewBox="0 0 48 48" xmlns="http://www.w3.org/2000/svg">
  <g transform="translate(24,24)">
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(0)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(22.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(45)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(67.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(90)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(112.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(135)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(157.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(180)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(202.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(225)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(247.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(270)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(292.5)"/>
    <line x1="0" y1="-16" x2="0" y2="-7" stroke="#fff" stroke-width="2"   stroke-linecap="round" transform="rotate(315)"/>
    <line x1="0" y1="-13" x2="0" y2="-7" stroke="#fff" stroke-width="1.4" stroke-linecap="round" transform="rotate(337.5)"/>
    <circle r="3" fill="#fff"/>
  </g>
</svg>
```

### 6.4 Mode Tab Switcher

The top-level control for switching between the three capture modes. Lives above
the phone frame or at the very top of the capture screen.

```html
<div class="mode-tabs" role="tablist">
  <button class="mode-tab mode-tab--active" role="tab" aria-selected="true">
    Video &amp; Image
  </button>
  <button class="mode-tab" role="tab" aria-selected="false">
    Audio &amp; Voice
  </button>
  <button class="mode-tab" role="tab" aria-selected="false">
    Text
  </button>
</div>

<style>
.mode-tabs {
  display: inline-flex;
  background: #1A1A1A;
  border-radius: var(--radius-pill);
  padding: 4px;
  gap: 2px;
}
.mode-tab {
  padding: 10px 20px;
  border-radius: var(--radius-pill);
  border: none;
  background: transparent;
  color: var(--color-text-secondary);
  font-family: var(--font-ui);
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  cursor: pointer;
  transition: background 180ms, color 180ms;
  white-space: nowrap;
}
.mode-tab--active {
  background: var(--color-accent);
  color: #fff;
}
/* Audio & Voice active state: outlined variant */
.mode-tab--active-outline {
  background: transparent;
  color: #fff;
  border: 1.5px solid var(--color-accent-bright);
}
</style>
```

> **Note on active tab style**: In the screenshots, "Video & Image" uses a solid
> purple fill when active. "Audio & Voice" uses an outlined/bordered variant with
> no fill. Both are valid — use fill for the most common mode, outline for secondary.

### 6.5 AI Analysis View — Video & Image Mode

Shows while the AI is processing a captured photo or video. The image/video fills
most of the screen. Floating annotation chips appear around the image edges.

```html
<div class="analysis-screen">
  <!-- Header -->
  <header class="resolve-header-mobile">
    <span class="wordmark">Resolve</span>
    <div class="avatar-btn"><!-- person icon --></div>
  </header>

  <!-- Status line -->
  <div class="analysis-status">
    <span class="analysis-headline">Analyzing Fault...</span>
  </div>

  <!-- Image + overlay -->
  <div class="analysis-image-wrap">
    <img src="..." alt="Captured component" class="analysis-image"/>
    <!-- Scrolling step log overlaid top-left of image -->
    <div class="analysis-log">
      <p class="log-line log-line--done">Analyzing component structure</p>
      <p class="log-line log-line--done">Searching through equipment manuals</p>
      <p class="log-line log-line--active">Analysing P&amp;ID</p>
    </div>
    <!-- Spinning starburst top-right of image -->
    <div class="analysis-spinner"><!-- starburst SVG with .starburst-loading --></div>
  </div>

  <!-- Floating annotation chips (position absolute relative to screen) -->
  <div class="annotation-chip annotation-chip--left" style="top: 52%">
    Model Number: F490-NB_Gen 2
  </div>
  <div class="annotation-chip annotation-chip--right" style="top: 67%">
    GPS Location Found, Plant 1, Row 3
  </div>
  <div class="annotation-chip annotation-chip--left" style="top: 82%">
    Fluid Leaking
  </div>
</div>

<style>
.analysis-screen {
  position: relative;
  min-height: 100svh;
  background: var(--color-bg);
  overflow: hidden;
}
.analysis-status {
  padding: 8px 20px 16px;
}
.analysis-headline {
  font-family: var(--font-mono);
  font-size: var(--text-2xl);
  font-weight: var(--weight-semibold);
  color: var(--color-text-primary);
  letter-spacing: 0.02em;
}
.analysis-image-wrap {
  position: relative;
  width: 100%;
  aspect-ratio: 9/14;
  overflow: hidden;
}
.analysis-image {
  width: 100%; height: 100%;
  object-fit: cover;
}
.analysis-log {
  position: absolute;
  top: 12px; left: 12px;
  display: flex; flex-direction: column; gap: 4px;
}
.log-line {
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin: 0;
}
.log-line--done { opacity: 0.6; }
.log-line--active {
  color: var(--color-text-primary);
  opacity: 1;
}
.analysis-spinner {
  position: absolute;
  top: 12px; right: 12px;
}

/* Floating annotation chips */
.annotation-chip {
  position: absolute;
  background: rgba(20, 20, 20, 0.88);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: var(--radius-pill);
  padding: 8px 14px;
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  color: var(--color-text-primary);
  white-space: nowrap;
  backdrop-filter: blur(8px);
  /* Animate in */
  animation: chip-in 400ms cubic-bezier(0.25, 0, 0.1, 1) both;
}
.annotation-chip--left  { left: -8px; transform: translateX(0); }
.annotation-chip--right { right: -8px; transform: translateX(0); }

@keyframes chip-in {
  from { opacity: 0; transform: translateX(-12px); }
  to   { opacity: 1; transform: translateX(0); }
}
</style>
```

### 6.6 AI Analysis View — Audio & Voice Mode

Shows during audio recording and analysis. Replaces the image with a waveform
visualisation. Recording controls appear at the bottom.

```html
<div class="audio-analysis-screen">
  <header class="resolve-header-mobile">
    <span class="wordmark">Resolve</span>
    <div class="avatar-btn"><!-- person icon --></div>
  </header>

  <div class="analysis-status audio-status">
    <span class="analysis-headline">Analyzing Audio...</span>
    <div class="starburst-loading"><!-- starburst SVG --></div>
  </div>

  <!-- Waveform visualiser -->
  <div class="waveform-container">
    <canvas class="waveform-canvas" id="waveform"></canvas>
    <!-- Red playhead line is rendered on canvas -->
  </div>

  <!-- Recording status bar -->
  <div class="recording-bar">
    <div class="recording-indicator">
      <span class="recording-dot"></span>
      <span class="recording-label">Recording...</span>
    </div>
    <span class="recording-timer">00:24</span>
  </div>

  <!-- Mic button -->
  <div class="mic-cta">
    <button class="mic-btn mic-btn--active" aria-label="Stop recording">
      <!-- mic icon SVG -->
    </button>
  </div>

  <!-- Floating annotation chips -->
  <div class="annotation-chip annotation-chip--left" style="top: 40%">
    Audio pattern match
  </div>
  <div class="annotation-chip annotation-chip--right" style="top: 62%">
    Valve chatter identified
  </div>
</div>

<style>
.audio-status {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 20px 20px;
}
.waveform-container {
  margin: 0 20px;
  background: transparent;
  border-bottom: 1px solid var(--color-border);
  height: 200px;
  display: flex;
  align-items: center;
}
.waveform-canvas {
  width: 100%; height: 100%;
}
/* Draw bars via JS: played bars = #CCCCCC, unplayed = #333333, playhead = red line */

.recording-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 20px 8px;
}
.recording-dot {
  display: inline-block;
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--color-record);
  margin-right: 8px;
  animation: blink 1s ease-in-out infinite;
}
@keyframes blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.3; }
}
.recording-label {
  color: var(--color-record-text);
  font-family: var(--font-ui);
  font-size: var(--text-sm);
}
.recording-timer {
  font-family: var(--font-mono);
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
}
.mic-cta {
  display: flex;
  justify-content: center;
  padding: 20px 0 32px;
}
.mic-btn {
  width: 56px; height: 56px;
  border-radius: 50%;
  border: 2px solid var(--color-record);
  background: var(--color-record-bg);
  color: var(--color-record);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
  font-size: 22px;
}
.mic-btn--active {
  box-shadow: 0 0 0 8px rgba(239, 68, 68, 0.1);
  animation: mic-pulse 2s ease-in-out infinite;
}
@keyframes mic-pulse {
  0%, 100% { box-shadow: 0 0 0  8px rgba(239,68,68,0.10); }
  50%       { box-shadow: 0 0 0 16px rgba(239,68,68,0.04); }
}
</style>
```

### 6.7 Conversational AI Chat — Text Mode

The text mode surfaces a full conversational interface. The AI asks clarifying
questions with **inline Yes / No quick-reply buttons** to avoid typing entirely.
The bottom bar always includes mic + attach alongside the text input.

```html
<div class="chat-screen">
  <header class="resolve-header-mobile">
    <span class="wordmark">Resolve</span>
    <div class="avatar-btn"><!-- person icon --></div>
  </header>

  <div class="chat-messages">
    <!-- User message bubble (right-aligned, dark surface) -->
    <div class="chat-bubble chat-bubble--user">
      Look into the pressure drop we're seeing across the heat exchanger
      after about 10 minutes of runtime
    </div>

    <!-- AI response (left-aligned, no bubble — raw text) -->
    <div class="chat-response">
      <p>
        I'm seeing intermittent flow and pressure instability in the
        circulation loop. Let me confirm a few things. Does the pressure
        drop occur after the system has been running for several minutes?
      </p>
      <!-- Inline quick-reply buttons -->
      <div class="quick-replies">
        <button class="quick-reply quick-reply--yes">Yes</button>
        <button class="quick-reply quick-reply--no">No</button>
      </div>
    </div>
  </div>

  <!-- Input bar — always at bottom -->
  <div class="chat-input-bar">
    <input
      type="text"
      placeholder="Ask anything..."
      class="chat-input"
    />
    <div class="chat-input-actions">
      <button class="chat-action-btn" aria-label="Attach">📎</button>
      <button class="chat-action-btn chat-action-btn--voice" aria-label="Voice">
        🎙 <span class="voice-bars">▏▎▍▌▍▎▏</span>
      </button>
      <button class="chat-submit" aria-label="Send">↑</button>
    </div>
  </div>
</div>

<style>
.chat-screen {
  display: flex;
  flex-direction: column;
  height: 100svh;
  background: var(--color-bg);
}
.chat-messages {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* User bubble */
.chat-bubble--user {
  align-self: flex-end;
  max-width: 85%;
  background: var(--color-surface-raised);
  color: var(--color-text-primary);
  font-size: var(--text-base);
  line-height: 1.5;
  padding: 14px 16px;
  border-radius: var(--radius-lg);
  border-bottom-right-radius: 4px;
}

/* AI response — no bubble, plain text */
.chat-response {
  max-width: 100%;
  font-size: var(--text-base);
  color: var(--color-text-primary);
  line-height: 1.6;
}
.chat-response p { margin: 0 0 16px; }

/* Quick-reply buttons */
.quick-replies {
  display: flex;
  gap: 10px;
  margin-top: 4px;
}
.quick-reply {
  padding: 8px 24px;
  border-radius: var(--radius-pill);
  font-size: var(--text-base);
  font-weight: var(--weight-medium);
  cursor: pointer;
  transition: background 150ms;
}
.quick-reply--yes {
  background: transparent;
  border: 1.5px solid var(--color-accent-bright);
  color: var(--color-accent-bright);
}
.quick-reply--yes:hover {
  background: var(--color-accent-muted);
  color: #fff;
}
.quick-reply--no {
  background: var(--color-surface-raised);
  border: 1px solid var(--color-border);
  color: var(--color-text-primary);
}

/* Input bar */
.chat-input-bar {
  border-top: 1px solid var(--color-border);
  background: var(--color-surface);
  padding: 12px 16px;
  border-radius: var(--radius-lg) var(--radius-lg) 0 0;
}
.chat-input {
  width: 100%;
  background: transparent;
  border: none;
  outline: none;
  font-size: var(--text-base);
  color: var(--color-text-primary);
  font-family: var(--font-ui);
  padding: 4px 0 8px;
  caret-color: var(--color-accent-bright);
}
.chat-input::placeholder { color: var(--color-text-tertiary); }
.chat-input-actions {
  display: flex;
  align-items: center;
  gap: 12px;
}
.chat-action-btn {
  background: var(--color-surface-raised);
  border: none;
  border-radius: var(--radius-pill);
  padding: 8px 14px;
  color: var(--color-text-secondary);
  font-size: 14px;
  cursor: pointer;
  display: flex; align-items: center; gap: 6px;
}
.chat-submit {
  margin-left: auto;
  width: 40px; height: 40px;
  border-radius: 50%;
  background: var(--color-accent);
  border: none;
  color: #fff;
  font-size: 18px;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
}
</style>
```

### 6.8 Voice / Capture Input Bar (standalone, non-chat screens)

```html
<div class="capture-bar">
  <button class="capture-btn" aria-label="Attach photo">📎</button>
  <button class="capture-btn voice-active" aria-label="Record voice">
    🎙 <span class="waveform">· · · · · ·</span>
  </button>
  <button class="capture-submit" aria-label="Submit">↑</button>
</div>

<style>
.capture-bar {
  position: fixed;
  bottom: 24px; left: 20px; right: 20px;
  background: #181818;
  border: 1px solid #333;
  border-radius: var(--radius-xl);
  padding: 12px 16px;
  display: flex; align-items: center; gap: 12px;
  box-shadow: 0 0 0 2px var(--color-accent-glow),
              0 0 32px var(--color-accent-glow);
}
.capture-submit {
  margin-left: auto;
  width: 40px; height: 40px;
  background: var(--color-accent);
  border: none; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
  animation: pulse-glow 2s ease-in-out infinite;
}
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 0  4px rgba(124,58,237,0.3); }
  50%       { box-shadow: 0 0 0 12px rgba(124,58,237,0.1); }
}
</style>
```

### 6.9 AI Query Search Bar (Desktop)

```html
<div class="query-bar">
  <span class="query-icon">🔍</span>
  <input type="text" placeholder="Show me the parts on each tail number affected"
         class="query-input"/>
  <button class="query-ask">Ask</button>
</div>

<style>
.query-bar {
  display: flex; align-items: center; gap: 12px;
  background: #0D0D0D;
  border: 1px solid #333;
  border-radius: var(--radius-pill);
  padding: 10px 10px 10px 16px;
  box-shadow:
    0 0 0 1px rgba(124,58,237,0.4),
    0 0 40px rgba(100,80,220,0.35),
    0 0 80px rgba(80,60,180,0.15);
}
.query-input {
  flex: 1; background: transparent; border: none; outline: none;
  font-size: var(--text-base);
  color: var(--color-text-primary);
  font-family: var(--font-ui);
}
.query-ask {
  background: var(--color-accent); color: #fff; border: none;
  border-radius: var(--radius-pill);
  padding: 8px 20px;
  font-size: var(--text-sm); font-weight: var(--weight-medium);
  cursor: pointer;
}
</style>
```

### 6.10 Fault / Issue Card

```html
<div class="fault-card">
  <div class="fault-card__header">
    <span class="priority-tag">PRIORITY 9</span>
  </div>
  <p class="fault-card__system">Wind Turbine Gearbox</p>
  <h3 class="fault-card__title">Oil leak, Notable seepage observed</h3>
  <p class="fault-card__desc">
    Notable oil seepage found, suggesting a potential seal failure
    that may hinder turbine performance.
  </p>
  <div class="fault-card__meta">
    <span>Today, 09:00 AM</span>
    <span>Wind Farm A, Row A, Sector 3</span>
  </div>
</div>

<style>
.fault-card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 16px;
  display: flex; flex-direction: column; gap: 8px;
}
.priority-tag {
  display: inline-block;
  background: var(--color-priority-high-bg);
  color: var(--color-priority-high);
  font-size: var(--text-xs);
  font-weight: var(--weight-bold);
  padding: 3px 8px; border-radius: var(--radius-sm);
  letter-spacing: 0.08em; text-transform: uppercase;
}
.fault-card__title {
  font-size: var(--text-md);
  font-weight: var(--weight-semibold);
  color: var(--color-text-primary);
  margin: 0;
}
.fault-card__meta {
  display: flex; gap: 12px;
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}
</style>
```

### 6.11 Severity Badge

```html
<span class="badge badge--moderate">⚠ Moderate</span>
<span class="badge badge--closed">Closed</span>

<style>
.badge {
  display: inline-flex; align-items: center; gap: 4px;
  font-size: var(--text-xs); font-weight: var(--weight-medium);
  padding: 4px 10px; border-radius: var(--radius-sm);
}
.badge--moderate {
  background: var(--color-severity-moderate-bg);
  color: var(--color-severity-moderate);
  border: 1px solid rgba(212,160,23,0.3);
}
.badge--closed {
  background: #1A1A1A;
  color: var(--color-text-secondary);
  border: 1px solid var(--color-border);
}
</style>
```

### 6.12 Action Modal (AD / Directive card)

```html
<div class="action-modal">
  <p class="action-modal__id">AD 2024-13-02</p>
  <p class="action-modal__summary">
    Potential detachment of PSU oxygen generators poses safety risk;
    mandatory inspection and fix required.
  </p>
  <ul class="action-modal__steps">
    <li>Inspect PSUs for secure oxygen generator retention</li>
    <li>Replace or repair faulty retention hardware</li>
    <li>Verify corrective actions via follow-up inspection</li>
  </ul>
  <div class="action-modal__actions">
    <button class="btn-secondary">See Evidence</button>
    <button class="btn-primary">Create Maintenance Tasks</button>
  </div>
</div>

<style>
.action-modal {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 20px; max-width: 360px;
  display: flex; flex-direction: column; gap: 12px;
}
.btn-primary {
  background: var(--color-accent); color: #fff; border: none;
  border-radius: var(--radius-pill); padding: 14px;
  font-size: var(--text-base); font-weight: var(--weight-medium);
  cursor: pointer; width: 100%;
}
.btn-secondary {
  background: transparent; color: var(--color-text-primary);
  border: 1px solid var(--color-border-subtle);
  border-radius: var(--radius-pill); padding: 14px;
  font-size: var(--text-base); font-weight: var(--weight-medium);
  cursor: pointer; width: 100%;
}
</style>
```

### 6.13 Fleet Data Table

```html
<table class="fleet-table">
  <thead>
    <tr>
      <th></th><th>Aircraft</th><th>Tailnumber</th>
      <th>Affected Part(s)</th><th>Position</th>
      <th>Affected Part Number</th><th>Next Due</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><span class="check">✓</span></td>
      <td>A320-Neo</td><td>A7-AHB</td>
      <td><span class="expandable">2 Parts ▾</span></td>
      <td>—</td><td>Multiple P/N's</td>
      <td class="urgent">25 Oct 2025 · 50 Cycles<br><small>&lt; 30 Days</small></td>
    </tr>
  </tbody>
</table>

<style>
.fleet-table {
  width: 100%; border-collapse: collapse;
  font-size: var(--text-sm); color: var(--color-text-primary);
}
.fleet-table th {
  text-align: left; color: var(--color-text-secondary);
  font-weight: var(--weight-medium);
  padding: 10px 12px; border-bottom: 1px solid var(--color-border);
}
.fleet-table td {
  padding: 12px; border-bottom: 1px solid var(--color-border-subtle);
}
.fleet-table tr:hover td { background: var(--color-surface-raised); }
.check { color: var(--color-success); font-weight: bold; }
.expandable {
  background: var(--color-accent); color: #fff;
  border-radius: var(--radius-pill); padding: 4px 10px;
  font-size: var(--text-xs); font-weight: var(--weight-medium);
}
</style>
```

---

## 7. Interaction & Motion Principles

| Principle | Spec |
|---|---|
| **Transition duration** | 180 ms (micro), 280 ms (panel), 400 ms (modal) |
| **Easing** | `cubic-bezier(0.25, 0, 0.1, 1)` — fast-in, soft-out |
| **Glow pulse** | 2 s ease-in-out infinite on submit / AI button |
| **Voice waveform** | Animated bars scaling with audio amplitude in real-time |
| **Annotation chips** | Slide in from nearest screen edge, staggered 150 ms apart |
| **Recording dot** | Blink 1 s ease-in-out infinite while recording is active |
| **Mic button** | Pulsing outer ring while recording |
| **Analysis log lines** | Fade in sequentially, previous lines dim to 60% opacity |
| **No skeleton loaders** | Use "Analyzing…" text + starburst spin only |
| **Tab switch** | 180 ms cross-fade between mode panels, no slide |

### Starburst loading animation

```css
@keyframes starburst-spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
.starburst-loading {
  animation: starburst-spin 2s linear infinite;
  transform-origin: center;
}
```

### Waveform rendering (JavaScript canvas approach)

```javascript
// Draw waveform bars on <canvas>
function drawWaveform(canvas, amplitudes, playheadIndex) {
  const ctx = canvas.getContext('2d');
  const W = canvas.width, H = canvas.height;
  const barW = 3, gap = 2, total = barW + gap;

  ctx.clearRect(0, 0, W, H);

  amplitudes.forEach((amp, i) => {
    const x = i * total;
    const barH = Math.max(4, amp * H * 0.8);
    const y = (H - barH) / 2;
    // Played bars: light grey. Unplayed: dark.
    ctx.fillStyle = i < playheadIndex ? '#CCCCCC' : '#333333';
    ctx.beginPath();
    ctx.roundRect(x, y, barW, barH, 2);
    ctx.fill();
  });

  // Red playhead
  const px = playheadIndex * total;
  ctx.fillStyle = '#EF4444';
  ctx.fillRect(px, 0, 1.5, H);
}
```

---

## 8. Conversational AI UX Principles

These patterns, visible specifically in the Text mode, define how the AI
communicates and how to reduce the user's typing burden.

| Pattern | Rule |
|---|---|
| **Quick-reply buttons** | Always offer Yes / No or 2–3 choice buttons after clarifying questions. Never force free-text for binary decisions. |
| **AI message style** | No bubble / no background. Full-width text, left-aligned, slightly larger than user bubbles. |
| **User message style** | Dark surface bubble, right-aligned, max-width 85%, rounded corners with tighter bottom-right radius. |
| **Placeholder text** | "Ask anything…" — conversational, not "Enter message" |
| **Input bar always visible** | Never hidden by keyboard; use `viewport-fit=cover` and adjust layout. |
| **Mic always present** | Even in Text mode, the mic icon is in the input bar at all times. |
| **Attach always present** | Paperclip icon for photo/video attach is always visible in the input bar. |
| **Submit button** | Solid purple circle with up-arrow icon. Always visible, never hidden. |

---

## 9. Screen Layout Templates

### Mobile — Video & Image capture / analysis

```
┌─────────────────────────────┐
│  Resolve              [👤]  │  ← Header 56px
├─────────────────────────────┤
│  Analyzing Fault...         │  ← Mono font, 32px
│  ┌───────────────────────┐  │
│  │ Analyzing component… ✳│  │  ← Analysis log + spinner
│  │ Searching manuals…    │  │
│  │ [glitch/scan image]   │  │  ← Full image, analysis overlay
│  └───────────────────────┘  │
│                             │
│ [Model No: F490-NB_Gen 2]   │  ← Annotation chip, floats left
│            [GPS: Plant 1,Row 3]│  ← Annotation chip, floats right
│ [Fluid Leaking]             │  ← Annotation chip, floats left
└─────────────────────────────┘
```

### Mobile — Audio & Voice recording / analysis

```
┌─────────────────────────────┐
│  Resolve              [👤]  │  ← Header
├─────────────────────────────┤
│  Analyzing Audio...    [✳]  │  ← Status + spinning starburst
│                             │
│ [Audio pattern match]       │  ← Chip, left
│  ████████████████▏░░░░░░░░  │  ← Waveform: played/unplayed + red playhead
│             [Valve chatter] │  ← Chip, right
│─────────────────────────────│
│  ● Recording...      00:24  │  ← Recording bar
│         [ 🎙 ]              │  ← Mic button (red border, pulsing)
└─────────────────────────────┘
```

### Mobile — Text / Chat mode

```
┌─────────────────────────────┐
│  Resolve              [👤]  │  ← Header
├─────────────────────────────┤
│              [User bubble]  │  ← Right-aligned dark bubble
│                             │
│  AI response text here,     │  ← Left-aligned, no bubble
│  full width, asking for     │
│  clarification.             │
│                             │
│  [Yes]  [No]                │  ← Quick-reply buttons
├─────────────────────────────┤
│  Ask anything...            │  ← Input
│  [📎] [🎙▏▎▍]         [↑]  │  ← Action bar
└─────────────────────────────┘
```

### Mode Tab Switcher (sits above phone frame in marketing / sits at top of screen in app)

```
┌───────────────────────────────────────────┐
│  [● Video & Image]  [Audio & Voice]  [Text]│
└───────────────────────────────────────────┘
Active = filled purple pill. Inactive = ghost text on dark container.
```

---

## 10. Do / Don't

| ✅ Do | ❌ Don't |
|---|---|
| Dark surfaces (#0A–#1A) everywhere | Light/white backgrounds |
| Purple accent for primary CTAs and active tabs | Blue or green as primary |
| Video & Image as the **first** tab | Put Text first |
| Voice + photo as first-class inputs | Hide or downplay mic/camera |
| Monospace for AI analysis status text and codes | Serif fonts anywhere |
| Red for recording state only | Red for non-recording alerts |
| Quick-reply Yes/No buttons in chat | Force free-text for binary choices |
| Floating annotation chips during analysis | Static list of extracted metadata |
| Waveform bars (played grey / unplayed dark / red playhead) | Single-colour flat waveform |
| Starburst spin for AI loading | Generic spinner or progress bar |
| 48 px minimum touch targets | Small tappable icons |
| Glow effects on active inputs and AI states | Drop shadows on cards |
| Amber/gold for moderate severity | Red for moderate (save red for recording/critical) |

---

## 11. Asset Reference

| File | Dimensions | Use |
|---|---|---|
| `assets/resolve-logo.svg` | 48 × 48 | App icon, favicons, small logo mark |
| `assets/resolve-header-mobile.svg` | 390 × 64 | Mobile header reference |
| `assets/resolve-header-desktop.svg` | 1440 × 72 | Desktop header reference |

To embed inline: copy SVG source from the file.
To reference as `<img>`: use the relative path from your artifact's location.
