# optimize-instructions

> **Analyzes your correction patterns across all accessible conversations and rewrites your Project's instructions into a smarter, more precise version — ready to paste.**

---

## What It Does

Most Claude Project instructions start strong and drift. You correct Claude, it adjusts in the session, but the instructions never get updated. Over time the gap widens between how you want Claude to respond and what the instructions actually enforce.

This skill closes that loop. When invoked, it:

1. **Reads its own current instructions** as a diagnostic baseline — treating every rule as a hypothesis to validate
2. **Searches across your conversation history** using `conversation_search` and `recent_chats` — not just the current session
3. **Reviews your active memory** for behavioral preferences already logged
4. **Classifies every correction signal** found: format violations, tone mismatches, depth errors, missing rules, weak rules, and repeat offenses
5. **Rewrites the full instruction set** — not a diff, not a list of suggestions — a complete replacement ready to paste

---

## How to Invoke It

Speak naturally. The skill triggers on any of these:

- *"Review your instructions and improve them"*
- *"Run an instruction audit"*
- *"Analyze how you've been responding to me"*
- *"What patterns do you notice in how I've been correcting you?"*
- *"Update your project instructions based on our history"*
- *"Optimize your behavior"*

---

## Output Format

The skill produces exactly three things, in this order:

1. **A single fenced codeblock** — the complete rewritten instruction set, ready to select-all and paste over your existing Project instructions
2. **One changelog line** — `[Date] — [# added] — [# changed] — [# removed] — [Top pattern corrected] — [Sessions analyzed]`
3. **A 2–3 sentence plain-English summary** of the most impactful changes and why they were made

No preamble. No "here is your updated instruction set." Just the output.

---

## Pattern Classification System

| Tag | What It Catches |
|-----|----------------|
| `FORMAT` | Length, bullet overuse, header abuse, structural issues |
| `TONE` | Hedging, affirmations, formality level, AI self-reference |
| `DEPTH` | Wrong technical calibration, too shallow, too verbose |
| `ASSUMPTION` | Wrong context inferred, intent misread |
| `MISSING` | Things you consistently add back after receiving output |
| `RULE GAP` | Corrected behavior with no existing rule covering it |
| `WEAK RULE` | Rule exists but was too vague to prevent the violation |
| `⚠️ REPEAT` | Same pattern across 2+ sessions — highest priority, appears first in output |

---

## What Makes This Different from Just Asking Claude

A plain prompt like *"what patterns do you notice in my corrections?"* only looks at the current conversation. This skill:

- Runs **4 targeted `conversation_search` passes** across your full history
- Pulls **15 recent chats** and scans for implicit corrections (redirections, rewrites, repeated questions)
- Cross-references your **active memory** for already-encoded preferences
- Validates every existing rule against the evidence — keeping, strengthening, replacing, or removing each one
- Dynamically infers **domain-specific search terms** from your Project context so retrieval is relevant, not generic

---

## Files

```
optimize-instructions/
├── SKILL.md                        ← Full execution logic (install this)
└── references/
    ├── chatgpt-variant.md          ← Equivalent workflow for ChatGPT Projects
    └── rule-writing-guide.md       ← Principles for enforceable rule writing
```

📦 **[Download optimize-instructions.skill](../optimize-instructions.skill)** — ready to install directly into Claude

---

## Changelog

| Version | Notes |
|---------|-------|
| 1.0 | Initial release — 5-step pipeline, cross-conversation retrieval, full rewrite output |

---

*Part of the [AI-Skills](https://github.com/C-Pearson31/AI-Skills) collection*
