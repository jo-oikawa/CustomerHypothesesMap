# Hypotheses Map
Interactive local map relating Customers, Motivations, and Jobs To Be Done.
Created initially for research conversations within the VS Code development and design team.

## Overview
This project visualizes relationships between three conceptual layers:
- Customers (C* identifiers)
- Motivations (M* identifiers)
- Jobs To Be Done (J* identifiers)

Edges (triples) are defined as Customer -> Motivation -> Job with a justification. The visualization groups these implicitly (Customer→Motivation and Motivation→Job links) and lets you inspect supporting rationales.

Key UI features now include:
- Category browsing (List all Customers / Motivations / Jobs)
- Expandable hypothesis cards (justification + full generated sentence)
- Hover highlight of hypothesis triples
- Two-level upstream highlighting when selecting a Job (shows related Motivations and their Customers)
- Search + clear selection
- Accessible pastel color system with tooltips for full labels

## Files
- `customers.md` – customer segments & associated motivation / job references
- `motivations.md` – descriptive motivations (M1–M19) with color mapping
- `jobs.md` – descriptive JTBD list (J1–J32)
- `connections.md` – canonical list of triples (Customer -> Motivation -> Job : Justification)
- `Hypotheses Framework.md` – template for deeper customer / problem / concept / feature hypotheses framing
- `index.html` – D3-based interactive map
- `LICENSE` – MIT

## Quick Start
Clone the repository then:
```bash
python -m http.server 5500
# OR
npx serve . -l 5500
```
Visit: http://localhost:5500/REFERENCES/HypothesesMap/index.html

## Why a Local Static Approach?
All content is plain markdown to encourage lightweight edits (PRs) and transparent review. The single-page visual layers on top without a build step.

## Usage
Open the index in a modern browser. If you open by double‑click (file://) and see an error about loading markdown, start a local server as above (browsers block fetch for local file URIs).

### Interactions
- Click a node to focus; related nodes stay visible, others fade.
- Use the category buttons (List all:) to browse all Customers, Motivations, or Jobs; clicking an item selects it.
- Sidebar lists all hypotheses (triples) involving the selected node; each shows justification (summary) and can expand to a full sentence.
- Hover a hypothesis card to temporarily highlight its Customer–Motivation–Job chain in the graph.
- Selecting a Job highlights upstream Motivations and the Customers feeding those Motivations (two-level context).
- Search box filters nodes by ID or name; Clear Selection resets state.
- Tooltips (hover) reveal full labels where truncated.

## Data Model
Each triple in `connections.md` encodes a rationale for why a customer segment cares about a motivation in the context of a job.
Format:
```
C1 -> M1 -> J4 : Short justification sentence.
```
From this, two graph edges are derived at runtime: `C1–M1` and `M1–J4`.

## Adding / Editing Content
1. Add or edit entries in `customers.md`, `motivations.md`, or `jobs.md` following existing bullet patterns (`- M1 ...`). Keep descriptive phrasing.
2. Introduce new IDs sequentially (e.g., M20, J33). Avoid reusing IDs.
3. Add supporting triple(s) to `connections.md` with a mechanism-focused justification (why this Motivation drives this Job for this Customer segment).
4. (Optional) Add a color for new motivation IDs in `index.html` (`colorMap` object). Provide a pastel (fill) + saturated (stroke) pair; ensure AA contrast for stroke against white.
5. (Optional) Extend hypotheses into structured form using `Hypotheses Framework.md` (copy / adapt a section) for deeper validation planning.
6. Refresh the map to verify.

### Hypothesis Grammar
Full sentences are auto-generated from triples using:  
`Because <Customer Segment> seeks <Motivation phrase>, they need to <Job phrase>.`  
Ensure motivation and job descriptions read naturally after removal of leading verbs if any.

## Color System
Motivation colors reside in the `colorMap` constant in `index.html`.
Guidelines:
- Pastel ~15–30% saturation, high lightness (L* ~75–90)
- Stroke color: same hue, stronger saturation, slightly lower lightness
- Maintain perceptible contrast between adjacent hues

## Accessibility Notes
- Current contrast favors structural differentiation over AAA text contrast. For long-form labels or export needs, consider a high-contrast mode.
- Possible enhancement: add a toggle to dark outline all nodes and show full names as tooltips.

## Contributing
1. Fork the repo & create a branch (`feat/add-segment-X`).
2. Make markdown edits (no build step needed).
3. Validate locally via the quick start server.
4. Submit PR describing rationale for additions or changes.

### Review Checklist
- IDs unique and sequential
- Justification is specific & mechanism-oriented (avoid vague "improves" without cause)
- Motivation color added if new & perceptually distinct
- Generated hypothesis sentence reads naturally (check in UI)
- No trailing whitespace / formatting anomalies

## Customization Ideas
- Add weights: Extend `connections.md` format to `: (strength=High, evidence=Moderate) justification...` and parse key-value pairs.
- Filter panel: Add checkboxes for customer segment toggling.
- Export: Add an SVG export button (`svg.outerHTML` to file download).
- Evidence links: Allow markdown links in justification text.

## Troubleshooting
| Symptom | Cause | Fix |
|---------|-------|-----|
| Blank page | Markdown fetch blocked | Use local HTTP server |
| No colors on new motivation | Missing entry in colorMap | Add `M#:[pastel,strong]` pair |
| Overlapping nodes | Force sim settling | Click-drag nodes or refresh |
| 404 on markdown file | Wrong relative path | Ensure all files in same folder |

## Roadmap Ideas
Updated / potential:
- Export graph / filtered hypotheses (SVG/PNG)
- Evidence & weighting metadata parsing
- Filter panel (toggle customer segments)
- Inline editing / live reload

## License
MIT – See `LICENSE`.

