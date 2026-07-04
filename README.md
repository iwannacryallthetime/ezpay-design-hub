# ezPay Design Hub

A monorepo for ezPay UI design prototypes. Two parallel implementations for designer collaboration and testing.

## Prototypes

### `/prototypes/claude-design/`
Standalone HTML prototype — a single, self-contained ezPay claim form artifact. Open `index.html` in a browser or use with Claude Code.

**Setup:**
```bash
cd prototypes/claude-design
# Open index.html in a browser, or
claude --open .
```

### `/prototypes/lovable/`
Full React + Vite application exported from Lovable. Complete ezPay claim submission flow with all components.

**Setup:**
```bash
cd prototypes/lovable
npm install
npm run dev
```

## For Designers

Clone this repo and open either prototype in Claude Code:

```bash
git clone https://github.com/lwannacrytlithetime/ezpay-design-hub.git
cd ezpay-design-hub

# Option 1: Quick HTML prototype
cd prototypes/claude-design
claude --open .

# Option 2: Full React app
cd prototypes/lovable
npm install
claude --open .
```

Both prototypes work with the Claude Code VS Code extension for collaborative editing.

## Architecture

- **Monorepo structure**: Each prototype is independent and self-contained
- **No shared dependencies**: Simplifies setup and avoids version conflicts
- **Claude Code ready**: `.claudeignore` and `CLAUDE.md` at root for context

## Project Context

See `CLAUDE.md` for architecture, coding conventions, and ezPay-specific context.
# ezpay-design-hub
