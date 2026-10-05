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
- Expand any line item; item 2 carries the AI findings
- Accept an AI-extracted value with **Update** (and undo it)
- Filter policy checks by All / Fail / Pass / Not Applicable, open a failed check, mark it resolved
- Pick a file under Proof of Purchase or Supporting Documents to preview it on the right
- Zoom the document viewer, collapse the sidebar, save a line-item comment
- **Verify** warns when AI issues are still open; **Reject** asks for a reason

### `prototypes/lovable/` (planned)
The ezPay claim submission flow exported from Lovable (React + Vite).

## Working on it with Claude Code

```bash
git clone https://github.com/lwannacrytlithetime/ezpay-design-hub.git
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
└── prototypes/
    └── ai-checker/
        └── index.html
```
