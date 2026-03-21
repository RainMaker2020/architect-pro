# architect-pro

A professional System Architect plugin for Claude Code. Transforms feature requests into high-fidelity technical specifications using an Expert Panel of two specialized subagents.

## What it does

When you give it a feature request, `architect-pro` runs a 5-phase Expert Panel:

1. **Clarify** — asks 2-3 targeted questions (skips if your request is already specific)
2. **Analyze** — the `system-architect` agent fingerprints your codebase architecture and confirms your tech stack
3. **Research** — the `trend-scout` agent finds modern (2025-2026) packages and patterns that fit your stack
4. **Discovery Report** — a scannable summary of architecture findings and tech recommendations
5. **Enhanced Prompt** — a structured technical specification ready for implementation

## Installation

```bash
claude plugin install architect-pro
```

Or clone and install locally:

```bash
git clone https://github.com/alogaili/architect-pro
claude plugin install --local ./architect-pro
```

## Usage

### Option 1: `/architect` command (formal)

```
/architect add a payment gateway with Stripe
```

### Option 2: `:enhanceprompt` suffix (shorthand)

```
add a payment gateway with Stripe:enhanceprompt
```

Both triggers run the identical 5-phase Expert Panel flow.

## After the Expert Panel

The plugin ends with:
> "The Expert Panel has finalized the design. Ready to implement? (yes/adjust/cancel)"

- `yes` — proceed with the Enhanced Prompt
- `adjust` — describe changes; the Enhanced Prompt regenerates
- `cancel` — stop; the Enhanced Prompt stays in the conversation

## Agents

| Agent | Role |
|-------|------|
| `system-architect` | Fingerprints codebase architecture and confirms tech stack |
| `trend-scout` | Finds modern 2025-2026 packages and patterns for your stack |

## License

MIT
