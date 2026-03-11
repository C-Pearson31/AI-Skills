# gamma-transformer

> **Converts fully-specified slide deck content into Gamma.app-optimized markdown — ready to paste directly into Gamma's "Paste in text" creation mode and produce a polished, professional presentation.**

---

## What It Does

Gamma.app's AI presentation engine is powerful, but it's particular about input format. Feed it dense paragraphs and speaker notes and you get mediocre output. Feed it optimized markdown with the right structure, word density, visual hints, and emoji anchors and Gamma produces presentations that look professionally designed.

This skill bridges that gap. You provide a slide deck specification in any format — detailed briefs, presentation outlines, existing slide content, raw notes — and the skill transforms it into Gamma-ready markdown following a strict set of formatting rules: 50-word slide caps, correct `---` separators, condensed visual instructions, extracted speaker note value, and strategic emoji usage that guides Gamma's layout engine.

The result is output you paste once. No reformatting, no back-and-forth with Gamma's AI.

---

## How to Invoke It

- *"Transform this slide deck for Gamma"*
- *"Optimize this presentation content for Gamma.app"*
- *"Convert my slides to Gamma format"*
- *"I have a presentation spec, make it work in Gamma"*
- *"Take this deck and make it Gamma-ready"*

---

## Accepted Input Formats

| Format | Notes |
|--------|-------|
| **Detailed slide briefs** | Slide-by-slide specs with content, visuals, and speaker notes |
| **Presentation outlines** | Section/topic structure with bullet content |
| **Existing slide content** | Exported text from PowerPoint, Google Slides, or Word |
| **Raw narrative notes** | Prose descriptions of what each slide should contain |

Multiple slides processed in sequence. Slides exceeding 75 words are automatically split. Thin or similar slides are merged.

---

## Transformation Rules

### 🔢 Word Density
| Target | Limit | Action |
|--------|-------|--------|
| 25–40 words | 50 words max | >75 words → split into 2 slides |

### 📐 Structure
- Every slide separated by exactly `---` (three dashes, own line — critical for Gamma to recognize slide breaks)
- Maximum 2 bullet levels — deeper nesting flattened or split
- Titles in `[Brackets]` or `# H1` format (consistent throughout)

### 🎯 Metrics Preservation
Exact numbers always kept and made prominent:
```
🎯 **83% Time Savings**
📊 67% reduction in administrative costs
⚡ 8 hours → 45 minutes
```

### 👁️ Visual Hints
Detailed visual specs condensed to 1–2 actionable lines:

**Before:**
> Two-column layout with 1px divider in #CCCCCC, left column has red heading with Helvetica Neue 24pt bold, gradient background at 45° angle...

**After:**
> `Visual: Two-column layout. Red heading left, green right. Large 77% callout.`

### 📝 Speaker Notes Handling
| Extract and integrate | Discard |
|----------------------|---------|
| Critical statistics | Timing notes |
| Powerful audience questions | Delivery cues |
| Emphasis cues → bold/emoji | Transition phrases |

---

## Emoji Strategy

Used as visual anchors for Gamma's layout engine — not decoration. Maximum 2–3 per slide.

| Emoji | Use For |
|-------|---------|
| 🎯 | Goals, targets, key points |
| ⚡ | Speed, efficiency, action items |
| 📊 | Data, metrics, analytics |
| ✅ | Benefits, success, completion |
| ⚠️ | Warnings, concerns, risks |
| 💡 | Ideas, insights, innovations |
| 🔧 | Tools, implementation |
| 📅 | Timelines, dates, schedules |
| 💰 | Cost, budget, ROI |

---

## Output Format

Every transformation returns this structure:

**Opening block:**
```markdown
# [PRESENTATION TITLE]

**Gamma Settings Recommendation:**
- Format: 16:9 (Traditional) or Fluid/4:3
- Text per card: Concise / Moderate / Detailed
- Image source: AI-generated / Stock / None
- Theme: Modern / Minimal / Professional / Bold

**Master AI Instructions:**
[2–3 sentences of overall design guidance]

---
```

**Each slide:** Title + content + visual hint + `---` separator

**Closing summary:**
```markdown
**Transformation Complete**
- Total slides: [X]
- Estimated presentation time: [Y minutes at 2.5–3 min/slide]
- Key optimizations: [Summary of major changes made]
```

---

## Transformation in Practice

### Before → After example (151 words → 37 words, 75% reduction)

**Before:**
```
Traditional Approach: Manual data entry requires approximately 6 hours per week per employee...
Report generation involves 4 hours of manual compilation...
Email correspondence consumes 5 hours weekly...
Total time spent: 15 hours per employee per week...
[3 more paragraphs + detailed visual spec + speaker notes]
```

**After:**
```markdown
[Traditional vs. AI-Enhanced Operations]

Traditional → AI-Enhanced

Manual data entry: 6 hrs/week → 30 min/week
Report generation: 4 hrs/week → 1 hr/week
Email responses: 5 hrs/week → 2 hrs/week

**Total:** 15 hours → 3.5 hours

🎯 **77% TIME SAVINGS**

What would your team do with an extra 11.5 hours per week?

Visual: Two-column before/after. Clock icons on each metric.
Large callout box for 77%. Contrasting colors (red → green).

---
```

All exact metrics preserved. Visual spec condensed to two lines. Closing question extracted from speaker notes and promoted to slide content.

---

## Quality Gate

Before delivering output the skill verifies:

- ✅ Every slide ends with `---` (except the final slide)
- ✅ No slide exceeds 50 words
- ✅ All key metrics preserved with exact numbers
- ✅ Maximum 2 bullet levels anywhere
- ✅ Emoji used strategically (2–3 per slide max)
- ✅ Visual hints are concise (under 15 words each)
- ✅ Logical content flow maintained across the deck
- ✅ Slide count appropriate for intended presentation time

---

## Files

```
gamma-transformer/
├── SKILL.md                                  ← Full transformation logic (install this)
├── scripts/
│   └── validate_gamma.py                     ← Optional output format validator
└── references/
    ├── format-spec.md                        ← Complete Gamma markdown rules and edge cases
    └── transformation-examples.md            ← Four full before/after transformation examples
```

📦 **[Download gamma-transformer.zip](../gamma-transformer.zip)** — ready to install directly into Claude

---

## Changelog

| Version | Notes |
|---------|-------|
| 1.0 | Initial release — 6-step transformation workflow, quality gate, validation script, 4 reference examples |

---

*Part of the [AI-Skills](https://github.com/C-Pearson31/AI-Skills) collection*
