# ezPay Design Hub — context for Claude

## What this repo is
A personal design sandbox for ezPay, an internal claims and expense system. Prototypes here are
for exploring and testing design ideas, not production code. Keep them easy for a designer to
read and change.

## Prototypes
- `prototypes/ai-checker/index.html` — checking officer (CO) view of the AI Checker.
  Source of truth is Figma: file `L0DJ6cw857R3z29OoUpsQg`, frame `CO`, node `103:25013`.
- `prototypes/lovable/` — planned; claim submission flow exported from Lovable.

## Conventions
- Each prototype is a single self-contained HTML file: inline CSS and JS, no build step, no frameworks.
- Colours, radii and fonts live as CSS custom properties in `:root`. Reuse them; don't hardcode new hex values.
- Mock data lives in the `FILES` and `ITEMS` objects at the top of the script. Change content there,
  not in the render functions. Entries marked `placeholder: true` were invented to fill counts the
  Figma shows (e.g. "3/10 flagged") and aren't in the design.
- The UI renders from a `state` object; after changing state, call the matching `render*()` function.
- Icons are inline SVG `<symbol>`s in the sprite at the top of `<body>`. They are stand-ins for the
  Figma icon assets, so match the Figma icon when replacing one.
- Font is Inter (Google Fonts) with a system fallback.
- Keep keyboard focus visible and controls as real `<button>`s.

## Writing in the UI
- Sentence case, plain verbs, active voice. Buttons say what happens ("Mark resolved", "Reject claim").
- Error and empty states say what happened and how to fix it. Never use the word "mapping" in error messages.

## ezPay vocabulary
- CO = checking officer; the person reviewing claims in this screen.
- Supporting officer, approving officer, proxy officer = later steps in the approval workflow.
- CC = cost centre, FC = fund centre, GL = general ledger account, AOR = area of responsibility, IO = internal order.
- Advance = money paid out before a trip, cleared later by a claim.
