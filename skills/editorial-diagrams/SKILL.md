---
name: editorial-diagrams
description: Draw flowcharts, architecture diagrams, org charts, timelines, loops/flywheels, quadrants, bar/line charts, and other schematics as a single self-contained HTML file with inline SVG, in a consistent minimal/editorial style (warm paper background, serif titles, mono technical labels, hairline borders, one accent color, no shadows, no Mermaid-style auto-layout). Use whenever a request calls for a diagram, chart, workflow visual, or "map this out" rather than a written description.
license: MIT
---

# Editorial Diagrams

Trimmed, single-file adaptation of the `diagram-design` Claude Code plugin (Kate's setup, MIT
licensed, source: github.com/cathrynlavery/diagram-design) for use without its reference-file
loader or Python validators. Same visual language, condensed into one file.

## 1. Philosophy

**The highest-quality move is usually deletion.**

- Every node is a distinct idea. Two nodes that always travel together are one node.
- Every connection carries information. If the relationship is obvious from layout, remove the line.
- The accent color is editorial, not a flag — 1–2 focal nodes per diagram, never more.
- A schematic isn't done when everything is added. It's done when nothing can be removed.
- Target density: enough to be technically complete, not so dense it needs a guide. More than
  ~9 nodes usually means it should be two diagrams (overview + detail).

Before drawing, ask: *would the reader learn more from this than from a well-written paragraph
or a short table?* If no, don't draw it — say so instead.

## 2. Visual types

Pick the nearest fit; don't force a type that doesn't match the content:

Architecture, flowchart, sequence diagram, state machine, ER/data model, timeline, swimlane,
quadrant (2×2), radar/spider, loop/flywheel, nested/containment, tree, org chart, layer stack,
Venn, pyramid/funnel, treemap, bar chart, line chart, Gantt, scatter plot, and general process/data-flow
diagrams.

If a 3-column table would communicate the same thing, use the table instead.

## 3. Universal anti-patterns — avoid these

| Anti-pattern | Why it fails |
|---|---|
| Dark mode + cyan/purple glow | Reads as "AI slop," no real design decision behind it |
| Monospace font for everything | Mono is for technical content only (ports, commands, URLs) — names go in a plain sans-serif |
| Identical boxes for every node | Erases hierarchy |
| Legend floating inside the diagram | Collides with nodes — put it in a horizontal strip below |
| Arrow labels with no background mask | Text bleeds through the line underneath it |
| Shadows on any element | Shadows are out; hairline borders are in |
| Heavy rounded corners (`rounded-2xl`) | Max radius 6–10px, or none |
| Accent color on every "important" node | Accent = 1–2 editorial focal points, not a signaling system |
| Diagonal/slanted connectors | Connectors must be rounded right-angle (orthogonal) elbows |
| Two connectors overlapping or sharing a stroke path | Each connection must be independently traceable — offset or bridge them |
| Two connectors sharing one attach point on a box | Fan attach points along the edge, ≥12px apart |

## 4. Design system

Default palette (swap only if Kate gives brand colors for a specific job):

| Role | Hex | Use |
|---|---|---|
| paper | `#f5f5f5` | page/diagram background |
| ink | `#2d3142` | primary text, primary stroke |
| muted | `#4f5d75` | secondary text, default arrows |
| soft | `#7a8399` | sublabels, tertiary text |
| rule | `rgba(45,49,66,0.10)` | hairline borders |
| accent | `#eb6c36` | 1–2 focal elements only |
| link | `#2e5aa8` | HTTP/API calls, external-system arrows |

Node treatment by type:

| Node type | Fill | Stroke |
|---|---|---|
| Focal (1–2 max) | accent tint | accent |
| Normal step/component | white | ink |
| Store/state | ink @5% | muted |
| External/cloud | ink @3% | ink @30% |
| Input/user | muted @10% | soft |
| Optional/async | ink @2% | ink @20%, dashed `4,3` |
| Security/boundary | accent @5% | accent @50%, dashed `4,4` |

Typography:

- **Title** — a serif font (e.g. Georgia, or Instrument Serif if the Google Font is reachable), ~28px — page H1 only.
- **Node name** — a plain sans-serif (e.g. system sans, or Geist), 12px, semibold — human-readable labels.
- **Sublabel** — monospace, 9px — ports, URLs, technical detail.
- **Arrow label** — monospace, 8px, all-caps, ≤14 characters.

Load fonts via Google Fonts `<link>` if network access is available; otherwise fall back to
system serif/sans/mono stacks — the layout rules matter more than the exact typeface.

## 5. Core SVG rules

- **Arrows drawn before boxes**, so z-order puts lines behind nodes.
- Define three arrowhead markers: default (muted), accent, and link-blue.
- **Every connector between nodes not sharing an x/y axis uses a rounded right-angle elbow**
  (quarter-arc radius ~8px). Never a diagonal line.
- **Every arrow label sits on an opaque mask rect** (fill = paper color) with a 6–10px visible
  gap above the connector line — the label must never touch or cover the arrow it's labeling.
- **No two connectors overlap or share a path.** If two must cross, offset them or route one
  around; if several connectors touch the same edge of a box, space their attach points ≥12px apart.
- Node box pattern: opaque background rect first (prevents bleed-through), then the styled box
  (fill/stroke per §4), then the node name (sans-serif) and optional sublabel (mono) centered
  inside it.
- Legend — a horizontal strip below the diagram with a hairline top border, never floating inside
  the diagram area.
- Keep coordinates, font sizes, gaps, and padding on a 4px grid where practical (e.g. 8, 12, 16,
  20, 24, 32 — not 7, 13, 19).

## 6. Complexity budget

Keep diagrams readable, not exhaustive:

- Max ~9 nodes, ~12 connectors per diagram.
- Max 2 accent-colored elements.
- If the content needs more, split into an overview diagram + a detail diagram rather than
  cramming one dense diagram.

## 7. Output format

Always produce **one self-contained `.html` file**:

- Inline `<style>` (no external CSS files) and inline `<svg>` (no external images).
- Static by default — no JavaScript unless motion is explicitly requested.
- The `<svg>` should carry `role="img"` and a `<title>` (first child, before any `<defs>`) plus a
  one-sentence `<desc>` describing what the diagram shows in plain language — not a shape-by-shape
  narration.
- Page structure: eyebrow label → serif title → the diagram → optional short summary underneath.

## 8. Before finishing — quick check

- [ ] Could a table or a short paragraph say this just as well? (If yes, don't draw.)
- [ ] Accent color used on 2 elements or fewer?
- [ ] Every connector orthogonal (no diagonals), every label has a visible gap above its line?
- [ ] No two connectors overlapping or sharing an attach point?
- [ ] Legend (if any) is a horizontal strip below the diagram, not floating inside it?
- [ ] Node count within budget, or split into overview + detail?
- [ ] `<title>`/`<desc>` filled in on the `<svg>`?
