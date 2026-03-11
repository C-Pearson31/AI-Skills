# flow-review

> **Performs a structured, evidence-based quality gate review of Salesforce Flow definitions — returning a prioritized audit report with severity ratings, concrete fixes, and a ranked remediation plan.**

---

## What It Does

Salesforce Flows fail in production for predictable, preventable reasons: DML inside loops, missing fault handlers, recursion with no guard, hard-coded IDs, wrong run context. Most of these are invisible until they cause a governor limit error or corrupt data at scale.

This skill applies a **PMD-inspired rule catalog** across 20 quality gates — P0 blockers, P1 majors, and P2 hygiene items — producing a structured markdown audit report that reads like a senior architect's code review. Evidence-based only. No invented findings.

Accepts **Metadata API XML, JSON, element tables, screenshots, or narrative descriptions** of a flow and returns a ranked finding report with severity, evidence, risk, fix, and a prioritized remediation plan.

---

## How to Invoke It

Provide a flow definition in any supported format and describe what you want:

- *"Review this flow XML for production readiness"*
- *"Audit this flow for bulk safety issues"*
- *"Check this flow's fault handling and recursion guard"*
- *"Does this flow have any P0 blockers?"*
- *"Review my flow for naming and governance issues"*

Or use slash commands directly:

| Command | What It Does |
|---------|-------------|
| `/review` | Full review — all rules, full report |
| `/summary` | Scope summary + top fixes only |
| `/q` | Minimum follow-up questions only |
| `/redo` | Rerun with updated evidence |
| `/more` | Expand rationale and alternatives on any finding |
| `/links` | Add 2–5 official Salesforce documentation links |
| `/alt` | Propose an alternative flow design |
| `/arg` | Argue both sides of a borderline rule call |
| `/help` | Explain what inputs work and what output to expect |

---

## Accepted Input Formats

| Format | Notes |
|--------|-------|
| **Metadata API XML** | Highest fidelity — treated as source of truth |
| **Tool/custom JSON** | Full review supported |
| **Element table** | Partial review — element inventory without connectors |
| **Screenshots converted to text** | Supported; certainty lowered for wiring evidence |
| **Narrative description** | Supported; metadata export requested when verdict matters |

Multiple flows can be provided — the skill reviews one at a time unless you explicitly ask for portfolio-level triage.

---

## Rule Catalog Summary

Rules are applied in P0 → P1 → P2 order. Every finding includes evidence, risk, violation example, and recommended fix.

### 🔴 P0 — Blockers (must fix before production)

| Rule | What It Checks |
|------|---------------|
| `FLOW-P0-001` | Flow description present and useful |
| `FLOW-P0-002` | Selective start criteria + correct "When to Run" |
| `FLOW-P0-003` | No DML operations inside loops |
| `FLOW-P0-004` | No Get Records inside loops |
| `FLOW-P0-005` | Fault paths on all risky elements |
| `FLOW-P0-006` | Explicit fail-closed vs fail-open strategy |
| `FLOW-P0-007` | Recursion / re-entry guard present |
| `FLOW-P0-008` | No hard-coded IDs or org-specific constants |
| `FLOW-P0-009` | Security/run context justified (user mode vs system mode) |
| `FLOW-P0-010` | Testability gate — evidence of flow or Apex test coverage |
| `FLOW-P0-011` | Trigger order governance across flows on same object |

### 🟠 P1 — Majors (fix or justify with documented mitigation)

| Rule | What It Checks |
|------|---------------|
| `FLOW-P1-101` | Complexity budget — branching and readability |
| `FLOW-P1-102` | Nested loops |
| `FLOW-P1-103` | High element/limit footprint |
| `FLOW-P1-104` | Unused resources removed post-refactor |
| `FLOW-P1-105` | Screen flow DML between screens |
| `FLOW-P1-106` | API version currency |
| `FLOW-P1-107` | Flow type/timing context mismatch |
| `FLOW-P1-108` | Parallel/async race and lock risk |
| `FLOW-P1-109` | Naming and readability against org naming guide |

### 🟡 P2 — Minors (hygiene and governance)

| Rule | What It Checks |
|------|---------------|
| `FLOW-P2-201` | Modularization via subflows |
| `FLOW-P2-202` | Externalized configuration (no hardcoded thresholds) |
| `FLOW-P2-203` | Inline documentation on complex nodes |
| `FLOW-P2-204` | Versioning hygiene and change log |

---

## Output Format

Every review returns this structure:

1. **Scope summary** — flow name, type/timing, object, status, API version, top conclusion
2. **Context table** — reviewer roles and categories assessed
3. **Results table** — Rule / Severity / Status (✅ ⚠️ ❌) / Evidence / Risk + Violation example / Fix
4. **Prioritized fix plan** — grouped P0 → P1 → P2 with concrete retest notes
5. **Optional Mermaid diagram** — only when it clarifies a risky execution path
6. **Follow-up questions** — maximum 8, only when source gaps block a verdict

---

## Evidence Standards

This skill never invents findings. Evidence discipline is strict:

- **✅ Pass** — source clearly evidences compliance
- **⚠️ Warning** — source shows a risk, or rule cannot be proven from input
- **❌ Fail** — source clearly shows a violation

If a rule cannot be proven from the input, it is flagged **⚠️ Needs info** — not assumed to pass or fail. User-confirmed context is explicitly distinguished from source evidence in every finding.

---

## Naming Convention Support

The skill applies the `{ALL_CAPS_VERB} {Target Description} [BusinessUnit] [Trigger Context]` naming pattern for `FLOW-P1-109` readability findings, with an approved verb set and rename examples built in.

Example rename suggestions:
- `KSD Multi Event Submission Handler` → `CREATE KSD Multi Events [MS] After Insert`
- `Update Case fields based on web form` → `UPDATE Case Fields from Web Form [SVC]`
- `Is Picture Day Coordinator V.009` → `DETECT Picture Day Coordinator [YBK] After Insert`

---

## Files

```
flow-review/
├── SKILL.md                          ← Full execution logic (install this)
└── references/
    ├── rule-catalog.md               ← All 20 rules with evidence and fix guidance
    ├── output-template.md            ← Strict output formatting spec
    └── naming-style-guide.md         ← Flow naming convention and approved verb set
```

📦 **[Download flow-review.zip](../flow-review.zip)** — ready to install directly into Claude

---

## Changelog

| Version | Notes |
|---------|-------|
| 1.0 | Initial release — 20-rule catalog, P0/P1/P2 severity, slash commands, evidence discipline |

---

*Part of the [AI-Skills](https://github.com/C-Pearson31/AI-Skills) collection*
