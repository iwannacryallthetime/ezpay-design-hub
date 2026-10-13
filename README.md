# ezPay Design Hub

A sandbox for ezPay UI prototypes, built from Figma with Claude. Each prototype is
self-contained so it can be opened, changed and thrown away without affecting the others.

## Prototypes

### `prototypes/ai-checker/`
The checking officer's **AI Checker** screen: reviewing a submitted claim with AI line-item
verification and policy checks side by side, plus a receipt viewer.

- Built from Figma: [AI-Checker → CO frame](https://www.figma.com/design/L0DJ6cw857R3z29OoUpsQg/AI-Checker?node-id=103-25013)
- One HTML file, no build step. Open `index.html` in a browser.

What you can click through:
- **Checking Tasks** in the sidebar (or **Go back**) lists the claims to check with their claimant, type, total
  and open AI issues; click one to open it. Two sample claims: DIP2025171622 from the Figma (SGD) and
  DIP2025171688, an invented software subscription billed in USD (no GST): invoice and bank slip as proof
  of purchase, an approved AOR as the supporting document, and its own AI findings
- Expand any line item; item 2 carries the AI findings
- Accept an AI-extracted value with **Update** (and undo it)
- Filter policy checks by All / Fail / Pass / Not Applicable, open a failed check, mark it resolved
- Pick a file under Proof of Purchase or Supporting Documents to preview it on the right
- Zoom the document viewer, collapse the sidebar, save a line-item comment
- **Verify** warns when AI issues are still open; **Reject** asks for a reason

### `prototypes/requestor-form/`
The requestor's **New claim request** form: an empty claim to fill in and submit. There's no Figma
for it; it's based on the AI Checker so both screens share the same shell, sidebar and colours.

- One HTML file, no build step. Open `index.html` in a browser.
- Linked from the AI Checker's sidebar (**New C. Requests**); **Checking Tasks** goes back.

What you can click through:
- Three steps: **Claim details** (attachments, basic & payment information, line items) →
  **Workflow officers** → **Review and submit**. **Next** checks the step you're on; the stepper lets you go back
  any time, and forward once the steps before are complete. The review has **Edit** links and "View receipt" per line.
- Start with **Attachments**: each proof of purchase is "read" and fills in a line item, with AI-filled
  fields tagged until you edit them. The extraction is mocked: it ignores the file and uses sample receipts in turn.
- Turn **AI extraction** off on the Attachments heading to attach files without filling anything in.
  Turning it off while a document is being read stops that read.
- **Replace** a file: with AI extraction on, a replaced receipt is read again, keeping any fields you'd edited yourself
- In a line item's **Coding** section, **Apply template** fills fund centre, cost centre, GL account, IO,
  AOR (fund number), agency, assignment, As123, location and project. **Save as template** saves that line's coding for reuse (for the session only).
- Remove a file that's attached to a line item: you're asked whether to remove the line item too or just the file
- The right-hand column shows the receipt for the line item you're working in, like the AI Checker's
  document viewer, so you can check the fields against it. Click a file under Attachments to preview it.
  Images and PDFs preview in the browser from your own computer; other file types get an "open the file" link.
- Fill in basic & payment information and the rest of each line item, then choose workflow officers
- Add and remove line items; switch a line's currency away from SGD to hide GST and the GST rate
- Line items stay manageable at 40+: only one is open at a time, the rest are compact rows with a status
  ("2 fields missing", "AI-filled, check", "Complete") and amount. **Next line item** steps through them, and
  from 4 lines there's a search box and All / Needs attention / Complete filters (on the review too)
- Only the file name and size are read from attachments; nothing is uploaded
- Watch the total and the **Before you submit** checklist update on the right
- **Next** and **Submit claim** flag missing fields and jump to the first one; submitting from the review shows a confirmation
- **Cancel** asks before clearing a form you've started

### `prototypes/lovable/` (planned)
The ezPay claim submission flow exported from Lovable (React + Vite).

## Design system

`design-system/` holds the tokens and components the prototypes share, pulled out of the AI Checker
and the requestor form.

- **`index.html`**: the living style guide. Open it in a browser to see every token and component in each
  state (default, hover, focus, disabled, error), with a note on when to use each.
- **`tokens.css`**: two layers. A palette of raw colours, and semantic aliases (`--text-muted`,
  `--border`, `--success-bg` …) that say what a colour is for. Also type, spacing, sizes, radii and shadows.
- **`components.css`**: buttons, badges and status tags, form fields, cards and section headers,
  navigation (tabs, stepper, sidebar, action bar), file rows and the document viewer, dialogs, toasts,
  and the AI checker patterns. Components use only semantic aliases.
- **`differences.md`**: an old → new lookup table of where each prototype differs from the design
  system. The prototypes haven't been switched over yet.

To use it on a page: link `tokens.css` and `components.css`, add `class="ez"` to `<body>`, and use the
class names from the style guide.

## Working on it with Claude Code

```bash
git clone https://github.com/iwannacryallthetime/ezpay-design-hub.git
cd ezpay-design-hub
claude
```

Then ask for changes in plain language, e.g. "in the AI checker, make the low-confidence
note collapsible". Claude reads `CLAUDE.md` for the conventions and context.

## Structure

```
ezpay-design-hub/
├── CLAUDE.md            context and conventions for Claude
├── .claudeignore        files Claude should skip
├── README.md
├── design-system/
│   ├── index.html       living style guide
│   ├── tokens.css       palette + semantic aliases, type, spacing, radii, shadows
│   ├── components.css   shared components and AI checker patterns
│   └── differences.md   where the prototypes differ (old → new)
└── prototypes/
    ├── ai-checker/
    │   └── index.html
    └── requestor-form/
        └── index.html
```
