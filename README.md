# 🧠 AI-Skills

A personal collection of Claude Skills I've built, tested, and use in active production workflows.

Each skill is an installable `.skill` file that extends Claude's native capabilities — invoking specialized behaviors on demand without needing to re-explain context or paste long prompts every session.

---

## What Is a Claude Skill?

Claude Skills are structured instruction sets that Claude loads automatically when it recognizes a relevant request. Instead of copy-pasting the same prompt over and over, you install a skill once and invoke it naturally — just describe what you want and Claude recognizes the pattern and executes the full workflow.

Skills in this repo follow the [Claude Skills architecture](https://www.anthropic.com) and are packaged as `.skill` files ready for direct install.

---

## Skills in This Collection

| Skill | What It Does | Trigger |
|-------|-------------|---------|
| [optimize-instructions](./optimize-instructions/) | Analyzes your correction history across all conversations and rewrites your Project instructions into a smarter, more precise version | *"review your instructions"*, *"run instruction audit"*, *"improve how you respond"* |

---

## How to Install a Skill

1. Download the `.skill` file from the skill's folder
2. In Claude, go to **Settings → Claude Skills → Install from file**
3. Select the downloaded `.skill` file
4. Start a conversation — Claude will invoke the skill automatically when relevant

---

## How These Were Built

These skills emerged from real workflows — identifying a repetitive, high-value task, abstracting the logic into a portable instruction set, and iterating based on actual usage. Each one is documented with its full reasoning so you can understand, fork, and adapt them.

---

## Contributing / Forking

Feel free to fork and adapt any skill for your own context. If you build an improved version, PRs are welcome.

---

*Built by [@C-Pearson31](https://github.com/C-Pearson31)*
