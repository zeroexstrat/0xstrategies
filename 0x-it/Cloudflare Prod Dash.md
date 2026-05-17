# 0x-it — Hub Control Transformation Playbook

This file is the deterministic spec for the **0x-it transform** — the operation that turns any HTML document into a sibling of `index.html` in the **Hub Control** design system.

When the user says **"0x-it this HTML"**, "convert to the system," "make it match the portfolio," or similar — apply the recipe below. Preserve the source content; restyle the chrome, the typography, and the structural anatomy. Never invent content the source doesn't have.

---

## 0. The transform in one sentence

**Take the source HTML's content, drop the source's chrome and styling, rebuild the document inside the Hub Control system using the canonical anatomy (doc-bar → cover → numbered sections → foot), and link it back to `index.html`.**

---

## 1. Identity

| | |
|---|---|
| Program | 0xStrategies |
| Wordmark | `0x` (mono, UPS gold) + `Strategies` (Newsreader serif, paper) |
| Tagline | "manage by design, not by default" |
| Operator | Rafael Almeida — Operations Coordinator, UPS CHEMA Hub |
| Aesthetic name | **Hub Control** — dark forest backbone, UPS-coded gold, sci-fi global logistics HUD |
| Voice | Operator's, technical, first-person, no marketing fluff |

---

## 2. Color tokens — copy `0x-system.css` verbatim

The complete token set lives in `0x-system.css`. Never re-derive — load that file or copy its `:root` block.

**Palette principles:**
- **`--bg #0D1A12` is the backbone** — every document is dark forest. Never re-skin to light.
- **`--gold #E5C260` is the sparingly-used pop.** Use for: section IDs, accents in italic serif headings, the `0x` wordmark glyph, "live" indicators, focus rings.
- **`--coral #C56247` for live/active states**, alarms, the in-operation `●` pulse.
- **`--moss #6B9A6E` for "ok" / verified / deployed** states.
- **`--amber #D9A441` for "research" / verifying** states.
- **`--plum #8B6BAE`, `--slate #5A7081`** are tertiary accents used in diagrams.
- **Paper tones** (`--paper #E8E0C7`, `--paper-2`, `--paper-3`) are text on dark — never invert.

---

## 3. Type stack

```css
--serif: "Newsreader", Georgia, serif;
--mono:  "JetBrains Mono", ui-monospace, "SF Mono", monospace;
```

Load via Google Fonts preconnect + a single `<link>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Newsreader:ital,wght@0,400;0,500;0,600;1,400;1,500&family=JetBrains+Mono:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

**Type rules:**
- **Body, prose, navigation, captions, labels — all mono.** Default font is JetBrains Mono.
- **Headings, hero phrases, important nouns — serif** (Newsreader). Italic variant carries `em` accents in gold.
- **Body text** is small (13px base) with comfortable line height (1.65–1.78). Letter-spacing `.005em`.
- **All-caps mono labels** for eyebrows / section IDs / tags. `.14em–.22em` letter-spacing.
- **No other fonts.** Don't introduce Inter, Playfair, IBM Plex, etc. anywhere.

---

## 4. Canonical document anatomy

Every transformed document has this top-to-bottom skeleton:

```
1. <doc-bar>           sticky · mark · crumb · live status · back link
2. <cover>             eyebrow · h1 (with serif italic em) · italic subtitle · 4-col meta
3. <section.box> × N   numbered /01, /02, ... · section header · content cards · prose
4. <foot>              3-col · operator · related dispatches · imprint
5. <foot-sig>          horizontal rule · transmission label · status pill
```

### 4.1 Doc-bar

```html
<div class="doc-bar">
  <div class="mark"><span class="px">0x</span><span class="nm">Strategies</span></div>
  <span class="sep">·</span>
  <span class="crumb"><a href="index.html">portfolio</a> · <a href="index.html#briefs">dispatches</a> · <span class="cur">[doc name]</span></span>
  <div class="end">
    <span class="live">[status · verified · v1.0]</span>
    <a class="back" href="index.html">← back</a>
  </div>
</div>
```

Always sticky. Always contains the crumb. Always points back to `index.html`.

### 4.2 Cover

```html
<header class="cover">
  <div class="eyebrow">[ dispatch · X · type ]</div>
  <h1>[Headline with <em>italic serif accent</em>].</h1>
  <p class="sub">[One-sentence italic standfirst.]</p>
  <dl class="meta">
    <div><dt>Author</dt><dd>Rafael Almeida<span class="sub">[role]</span></dd></div>
    <div><dt>Status</dt><dd>[live / verified / research]<span class="sub">[date · station]</span></dd></div>
    <div><dt>Scope</dt><dd>[size · scope]<span class="sub">[detail]</span></dd></div>
    <div><dt>Stack</dt><dd>[stack]<span class="sub">[tagline]</span></dd></div>
  </dl>
</header>
```

The eyebrow is wrapped in `[ ... ]` brackets visually via CSS. The h1 always has one italic serif `<em>`. The subtitle is italic Newsreader. The 4-col meta grid is mandatory.

### 4.3 Section box

```html
<section class="box" id="sN">
  <div class="sec-hdr">
    <span class="id">/ NN</span>
    <span class="t">section name with <em>italic accent</em></span>
    <span class="meta">[descriptor · status]</span>
  </div>
  [content: prose, cards, tables, diagrams]
</section>
```

Section IDs are always `/01`, `/02`, etc., bordered, gold, uppercase mono. Headings have one serif italic accent in gold. Meta sits at the right with optional `.ok` / `.warn` status spans.

### 4.4 Foot

Three-column grid: **operator** (contact), **related dispatches** (cross-links), **imprint** (deployment metadata). Followed by a full-width `.foot-sig` row: `[transmission label]` left, `[status pill]` right.

---

## 5. Component vocabulary

Use these named pieces — defined in `0x-system.css`. Don't invent variants. If the source has something not covered here, ask before adding.

| Component | Use for |
|---|---|
| `.eyebrow` | Bracketed all-caps gold label above a heading |
| `.sec-hdr` | Section header row with `/NN` ID + serif heading + meta |
| `.prose` | Serif body text blocks |
| `.sensor` | Stat card with big number + label + optional bar |
| `.cap` / `.cards` | Capability cards (2-, 3-, or 4-col grids) |
| `.briefs` / `.brief` | 5-col grid of related dispatch cards |
| `.constants` / `.const` | Greek-letter glyph cards (κ γ ε ρ etc.) |
| `.mtable` | Cargo-manifest style table (tracking · name · desc · status) |
| `.statband` / `.sb` | Stat grid (4-col by default) |
| `.tnode` | Trajectory / chronology entry with Roman numeral + meta + body |
| `.code` blocks | `<pre class="code">` with `.c` (comment) `.k` (keyword) `.v` (value) spans |
| `.callout` `.warn` `.ok` | Inline notes — gold / coral / moss left border |
| `.lattice-frame` | Target-reticle video frame with corner brackets |
| `.flow-down` | Vertical inheritance connector between phases |
| `.pdf-overlay` | DO NOT USE — was removed for reliability. Link PDFs in a new tab. |

---

## 6. Naming and labeling rules

- **Sections are numbered.** `/ 01 · / 02 · ...` Always with the leading slash and space.
- **Documents are "dispatches"** in the index.html briefings grid. Address them by their letter: `/a` deck, `/b` brief, `/c` paper, `/d` paper, `/e` spec.
- **Statuses:** `live · deployed · verified · research · verifying · staged · ok`. Color-coded by class (`.live → moss`, `.research → amber`).
- **Boundaries are decorative:** corner brackets (top-left + bottom-right pair) appear on featured cards (download, mission patch, key callouts) — not everywhere. Don't spam.
- **The `0x` wordmark is gold.** Never restyle it. The `Strategies` serif portion is paper-colored.
- **No emoji.** Mission patches, lattice reticles, and corner brackets are decoration enough.

---

## 7. Animation budget

- **Slow scan line** sweeping vertically (12s loop) — already in CSS, do not modify.
- **Pulse** (1.6s) on live indicators and the patch dot.
- **Patch spin** (60s) on the mission-patch SVG ring text.
- **Telemetry roll** (60s linear loop) for the masthead ticker.
- **All animations honor `prefers-reduced-motion: reduce`** — disable everything.
- **No transitions on hover beyond color/border** (.12–.15s ease). No transforms, no scale.

---

## 8. Responsive contract

Three breakpoints, codified in `0x-system.css` and `0x-template.html`:

| Breakpoint | Behavior |
|---|---|
| `≥ 1024px` | Full layout. 4-col stats, 2-col hero, multi-col grids. |
| `768–1024px` | Tablet. 2-col grids. Hero may stack. Sidebar narrows. |
| `< 768px` | Phone. Single column everything. Cargo-manifest tables collapse to cards. Trajectory rail collapses to inline pills. Scan line disabled (perf). |

Always test the phone breakpoint. Always.

---

## 9. The transform recipe

When asked to 0x-it a file:

1. **Read the source.** Extract: title, all content, any data (constants, tables, diagrams).
2. **Determine the document type:** brief (sort-training-platform), whitepaper (LTC, SI), spec (tracker_architecture), deck (presentation), map (chema-system-map). Each has a slightly different anatomy — see `0x-template.html` for the variants.
3. **Start from `0x-template.html`.** Copy it; rename; replace the slot placeholders with the source's content.
4. **Use the system stylesheet.** Either `<link rel="stylesheet" href="0x-system.css">` or inline the tokens — both work.
5. **Preserve the source's content faithfully.** Math blocks stay. SVG diagrams stay (but recolor fills/strokes to the palette tokens). Tables stay (restyle to `.mtable` or section-table).
6. **Add the chrome:** doc-bar with crumb back to `index.html`, cover with bracketed eyebrow + italic-em h1 + italic subtitle + 4-col meta.
7. **Renumber sections** to `/ 01`, `/ 02`, etc.
8. **Add the foot** with related dispatches.
9. **Test the phone breakpoint** before declaring done.

---

## 10. Anti-patterns — never do these

- Don't introduce a new font. Don't use Inter, Playfair, IBM Plex, or system fonts.
- Don't switch to a light theme. The system is dark-mode only by design.
- Don't use emoji.
- Don't invent new accent colors. Use the existing palette.
- Don't use `border-radius` aggressively. Sharp corners + corner brackets is the language. A few panels can be 2px; nothing rounded beyond that.
- Don't use gradients except the two existing ones: the linear lattice fade and the bar-fill `(--moss → --gold)`.
- Don't use shadows for elevation. The system is flat — depth comes from background tone shifts (`--bg → --bg-2 → --bg-3`).
- Don't use a PDF overlay modal. Link PDFs in a new tab.
- Don't add a hero image, hero photo, or stock visual. The mission patch SVG and lattice video are the only imagery.
- Don't introduce React, Tailwind, or any framework. Plain HTML + CSS + a small inline `<script>` for navigation.

---

## 11. Files in this system

| File | Purpose |
|---|---|
| `index.html` | Parent · canonical Hub Control reference |
| `0x-system.css` | Token set + every named component class |
| `0x-template.html` | Skeleton with slot placeholders for new documents |
| `CLAUDE.md` | This file — transform recipe + rules |
| `presentation_v1.1.html` | Reference: deck variant (snap-scroll slides) |
| `ltc_whitepaper_v1.0.html` · `si_whitepaper_v2.2.html` | Reference: whitepaper variant (sidebar + math) |
| `tracker_architecture_v2.11.html` | Reference: spec variant (cover + TOC + SVG diagram) |
| `sort-training-platform.html` | Reference: brief variant |
| `chema-system-map.html` | Reference: vertical inheritance flow variant |

Read the variant closest to the source before transforming.

---

*Last updated 2026-05-17 · Rafael Almeida · 0xStrategies · Hub Control*
