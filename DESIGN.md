# Design Documentation — Precedent Study Website

*AI War Cloud Database precedent study · Krishna Goyal · Methods as Practices, Columbia GSAPP
MSCDP, 2026. This file records the design system and the decisions behind it, as developed
across three iterations.*

## Concept

The site is designed to be **stylistically situated in its subject**. AI War Cloud's own
visual language — a dark field, a drifting network graph, forensic data presentation — is
adopted as the study's language, so that reading the analysis feels like being inside the
precedent. The mood target was *ominous but not heavy*: the gravity of the subject carried by
palette, spacing, and a quietly surveillant background rather than by effects.

## Color

| Token | Value | Role |
|---|---|---|
| `--bg` | `#0b0b0d` | near-black ground |
| `--text` | `#e8e4dc` | bone — reading text |
| `--dim` | `#8b877e` | muted — metadata, captions, hints |
| `--red` | `#d0342c` | signal red — the single accent: kickers, links, hot nodes, the alert strip |
| `--line` | `rgba(232,228,220,0.14)` | hairline frames and dividers |

One accent only. Red is reserved for what should alarm or orient: section kickers, links,
the mapped weapon systems in the diagrams, and the 2px alert strip along the top of every
page.

## Typography

Two families with a strict division of labor:

- **Sans** (`Helvetica Neue` stack) — display and reading text. Titles set very large
  (`clamp(2.2rem, 4.6vw, 3.6rem)` for sections; up to 5.6rem on the opening page) with tight
  leading and negative letter-spacing, after the reference template (codexalgorithm.com).
- **Mono** (`ui-monospace` stack) — everything that is *data*: the datasheet table, both
  bibliographies, captions, kickers, hints, the wordmark. This mirrors the precedent's own
  graph/spreadsheet duality: prose performs, mono verifies.

Title case on all section headings. Section kickers are small, tracked, uppercase, red.

## Structure & Navigation

The site is a **full-screen paged experience** (12 pages), not a scroll:

- **Click zones**: right half of the screen advances, left half goes back. Arrow keys work.
  Links, the menu, and the interactive diagram are excluded from the click zones.
- A pulsing hint bottom-right ("click right to continue → · left to go back") and a page
  counter bottom-left (`06 / 12`) keep the reader oriented.
- **Overlay menu**: a two-line burger (top right) rotates into an ×, opening a full-screen
  menu listing every section with an index number; items turn red on hover. Modeled on the
  reference site's toggle.
- Page order: Opening → Datasheet → three Layers of Analysis → Relational Diagram →
  Methodology → Rhetorical Analysis → Wider Practice → Personal Assessment → two
  Bibliographies.

## The Two Live Diagrams

**Background network** (every page): ~70 nodes on three parallax depth planes (far/mid/near),
each plane webbing only to itself, shifting subtly with the mouse. Every eighth node runs
hot red, and near-plane hot nodes carry the names of real entities from the precedent's
database (LAVENDER, PALANTIR, WHATSAPP, ROOMBA…) — the background is content, not decoration.
Kept faint (edge opacity ≤ 0.18) so it is felt rather than watched.

**Actor-network diagram** (hero + Relational Diagram page): a custom force simulation
(repulsion + edge springs + centering) of 27 actors in the project's production network.
Circles = people/institutions, squares = tools/artifacts, red diamonds = mapped
techno-military systems; solid/dashed/dotted edges = makes/informs/data-flows. Nodes are
draggable; hovering isolates a node's neighborhood. Labels flip sides near the right edge so
they stay in frame. The same canvas element is moved between the opening hero and the diagram
page in the DOM.

Both canvases render at `devicePixelRatio` (capped at 2) for crisp lines on high-DPI screens.

## Opening Sequence

The first page pairs the title block with Ciston's actual network-graph image, which fades
out over four seconds to reveal this study's live actor-network running beneath it — the
precedent literally dissolving into its analysis.

## Layout Rules

- Content pages use a 7/5 two-column grid: analysis text left, a sticky credited figure
  right. Captions sit **below** images, never on them.
- On the Relational Diagram and Bibliography pages, text and list items run the full
  container width, aligned to the diagram frame's edges. Bibliography markers hang left so
  item text aligns flush with the title.
- Every image is hotlinked from a bibliography source with an explicit credit line, and
  hides gracefully (`onerror`) if its source disappears.

## Accessibility & Resilience

`prefers-reduced-motion` renders the background network as a static field. The menu closes on
Escape. All interactive canvases are `aria-hidden` or labeled. The site is a single HTML file
plus one stylesheet — no frameworks, no build step.

## Iteration Log

1. **v1 — gradient page** (Part 1): single page, red–orange gradient, white text, one font.
2. **v2 — forensic dark** (Part 2): black ground, signal red, sans/mono split, drifting
   labeled network background with parallax depth; sections in one scroll.
3. **v3 — paged edition** (Part 3): full-screen click-through pages after the
   codexalgorithm.com template; overlay menu; hero crossfade; per-section imagery from the
   bibliography; interactive actor-network diagram; high-DPI rendering; alignment and
   title-case pass.
