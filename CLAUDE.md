# ezPay Design Hub — context for Claude

## What this repo is
A personal design sandbox for ezPay, an internal claims and expense system. Prototypes here are
for exploring and testing design ideas, not production code. Keep them easy for a designer to
read and change.

## Prototypes
- `prototypes/ai-checker/index.html` — checking officer (CO) view of the AI Checker.
  Source of truth is Figma: file `L0DJ6cw857R3z29OoUpsQg`, frame `CO`, node `103:25013`.
- `prototypes/requestor-form/index.html` — requestor view: a new, empty claim form to submit a claim.
  No Figma design; based on the AI checker (same shell, sidebar and tokens) so the two read as one product.
- `prototypes/lovable/` — planned; claim submission flow exported from Lovable.

The prototypes link to each other through the sidebar with relative paths: "Checking Tasks" →
`../ai-checker/index.html#tasks` (the list of claims to check), "New C. Requests" → `../requestor-form/index.html`.
In the AI checker, `#tasks` shows that list and `#claim/<claim number>` opens a claim; with no hash it opens
the first claim. Other nav links
show a "not wired up" toast. The sidebar markup is copied into each file, so change it in both.

## Design system
`design-system/` is the shared source for tokens and components: `tokens.css`, `components.css`,
a living style guide in `index.html`, and `differences.md` (old → new lookup of where the prototypes differ).
- `tokens.css` has two layers: a **palette** (raw colours like `--teal-700`) and **semantic aliases**
  (`--text-muted`, `--border`, `--accent`, `--success-bg` …). Components use semantic aliases only, never a
  palette step or a hex code. If a component needs a colour that has no alias, add an alias in `tokens.css`.
- Before adding a new colour, check whether a slate or teal step is close; only add a token if nothing is.
- Brand roles: `--brand` is identity (brand bar, active nav, total banner), `--brand-dark` is the selected tab,
  `--action` is primary actions, `--danger` is destructive actions (text and outline only).
- Spacing is a 4px scale with no 10px step; row heights come from `--size-*` tokens.
- Every status pairs its colour with an icon or words. Interactive components style hover, focus-visible,
  disabled and error; `.is-hover` / `.is-focus` exist only so the style guide can show those states.
- Class names are neutral (`.btn-primary`, not `.btn-verify`). Base rules sit inside `:where(.ez)` so any
  component class wins over them.
- The prototypes haven't adopted the design system yet. When changing a prototype, prefer design system names
  and tokens, and update `differences.md` when a row is fixed. When adding a component, add it to
  `components.css` and show it with its states in `index.html`.

## Conventions
- Each prototype is a single self-contained HTML file: inline CSS and JS, no build step, no frameworks.
- Colours, radii and fonts live as CSS custom properties in `:root`. Reuse them; don't hardcode new hex values.
- Mock data lives at the top of the script. Change content there, not in the render functions.
  - AI checker: the `CLAIMS` array, one entry per claim with its basic info, officers, totals, files and
    line items (`FILES` and `ITEMS` point at the open claim's). Receipt previews are in `SHEETS`, keyed by
    file id. DIP2025171622 is the Figma claim; DIP2025171688 is an invented second sample: a Claude software subscription
    billed in USD, with an invoice and bank slip as proof of purchase and an approved AOR as the supporting
    document (all mock documents, marked as such). It's a non-PT claim, so it has `policyChecks: false`: the
    Finance & policy checks panel is hidden and its checks don't count as issues, because those checks
    haven't been decided for non-PT claims. Remove the flag to show them again.
    Entries marked `placeholder: true` were invented to fill counts the Figma shows (e.g. "3/10 flagged").
    Review progress (resolved flags and checks, comments) is kept per claim while you stay on the page.
  - Requestor form: dropdown values in `OPTIONS`; the form's fields (labels, required/optional, error
    text, when a field shows) in `BASIC_FIELDS`, `OFFICER_FIELDS` and `ITEM_GROUPS`. The mock AI
    extraction doesn't read files: each proof of purchase takes the next entry in `EXTRACTS`.
    The form is three steps (`STEPS`, `state.step`): claim details, workflow officers, review. Each
    step's errors only show once you've tried to leave it (`state.triedSteps`). Line items are built for
    40+: one open at a time (`state.openLine` in step 1, `state.rvOpen` on the review), the rest as compact
    rows (`lineRow`), with search and filters from `LIST_TOOLS_FROM` lines. A collapsed line's fields aren't
    on the page, so open it (`openLine`) before focusing one of its fields.
    Attachments come first in step 1 because extraction fills in the line items; the AI extraction
    toggle (`aiExtract`) turns it off. The right-hand viewer shows the attachment of the active line item
    (`state.activeItem`, set by focusing or clicking a line) from a local blob: URL. Since extraction is
    mocked, the filled-in values won't match a real receipt you upload. Sample finance coding templates are in `TEMPLATES`; saved ones
    are added there for the session.
- The UI renders from a `state` object; after changing state, call the matching `render*()` function.
- Icons are inline SVG `<symbol>`s in the sprite at the top of `<body>`. They are stand-ins for the
  Figma icon assets, so match the Figma icon when replacing one.
- Font is Inter (Google Fonts) with a system fallback.
- Keep keyboard focus visible and controls as real `<button>`s.

## Writing in the UI
- Sentence case, plain verbs, active voice. Buttons say what happens ("Mark resolved", "Reject claim").
- Never set copy in all capitals: no `text-transform: uppercase` on headings, labels or titles, and
  no Title Case headings ("Line items", not "LINE ITEMS" or "Line Items"). Acronyms and codes stay as
  they are (GST, SGD, AOR, PDF). The AI checker still uses uppercase from its Figma frame.
- Error and empty states say what happened and how to fix it. Never use the word "mapping" in error messages.

## ezPay vocabulary
- CO = checking officer; the person reviewing claims in this screen.
- Supporting officer, approving officer, proxy officer = later steps in the approval workflow.
- CC = cost centre, FC = fund centre, GL = general ledger account, AOR = area of responsibility, IO = internal order.
- Advance = money paid out before a trip, cleared later by a claim.
