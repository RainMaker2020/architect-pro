---
name: architect-pro
description: Use this skill when the user invokes the /architect command with a feature request, or when the user's message ends with the suffix :enhanceprompt (e.g., "add dark mode:enhanceprompt"). Do not activate for general questions or unrelated requests.
version: 1.0.0
---

# Architect-Pro: Expert Panel Orchestrator

## Trigger Validation

If activated via the `:enhanceprompt` suffix:
- Extract feature text: everything before the final `:enhanceprompt` in the message.
- The suffix must be immediately adjacent to the last word (no space before the colon).
- If feature text is empty (user sent only `:enhanceprompt`), respond:
  "Please provide a feature request. Example: `add a payment gateway:enhanceprompt`"
  Then stop and wait.

## Phase 1 — Clarify

Check if the request clearly specifies all three of:
1. **Surface** — UI, backend, or both
2. **Trigger** — user action, scheduled job, or event
3. **Scope** — who it affects

If all three are clear, skip this phase entirely and say: "Your description is clear — skipping clarification questions."

Otherwise, ask up to 3 targeted questions **one at a time**. Wait for the user's answer before asking the next. Stop asking once the request is sufficiently clear.

## Phase 2 — Analyze (System-Architect)

Dispatch the `system-architect` agent. Provide it with the feature request text.

**Wait for the complete fingerprint output** before proceeding. You need:
- Architecture pattern
- Confirmed tech stack
- Integration path (exact files/directories)

## Phase 3 — Research (Trend-Scout)

Dispatch the `trend-scout` agent. Provide it with:
- The feature request
- The full system-architect output from Phase 2 (architecture pattern + confirmed stack)

**Wait for its recommendations** before proceeding.

## Phase 4 — Discovery Report

Print the following summary. Omit any category that has no meaningful findings.

```
## 🔍 Discovery Report

**🔍 Architecture:** [detected pattern + integration point from system-architect]
**🚀 Modern Tech:** [recommended package/pattern from trend-scout]
**💡 Best Practice:** [key convention or pattern to follow]
```

## Phase 5 — Enhanced Prompt

Generate the following structured specification:

```
## 🚀 Enhanced Prompt: [Feature Title]

### Context
[What the feature is, which part of the codebase it lives in, and why it matters]

### Technical Approach
- **Architecture fit:** [which layer/pattern this belongs to]
- **Files to create:** [exact relative paths]
- **Files to edit:** [exact relative paths]
- **Packages to install:** [exact package names and install commands]
- **Patterns to follow:** [existing conventions from system-architect]

### Acceptance Criteria
- [ ] [specific, testable criterion]
- [ ] [specific, testable criterion]
- [ ] [specific, testable criterion]

### Out of Scope
- [explicit boundary — what this feature does NOT include]
- [explicit boundary]
```

End with this exact line:
**"The Expert Panel has finalized the design. Ready to implement? (yes/adjust/cancel)"**

## Confirmation Loop

- **`yes`** — Your role is complete. The user will proceed with the Enhanced Prompt.
- **`adjust`** — Ask what should change. Then regenerate the Enhanced Prompt entirely with adjustments applied. Re-print the Discovery Report only if it changed. Always end with the canonical confirmation line. This loop repeats unlimited times.
- **`cancel`** — Respond: "Cancelled. The Enhanced Prompt above is preserved in this conversation." Stop.
