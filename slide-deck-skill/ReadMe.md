# slide-deck

**A Claude Projects skill for building professional Microsoft PowerPoint decks.**

This skill enforces a mandatory planning phase — an ASCII structural blueprint plus a recommended color theme — before generating a single slide. The result is decks that are structurally sound, visually varied, and content-appropriate from the first build rather than after multiple revision cycles.

---

## What This Skill Does

When you ask Claude to build a PowerPoint deck, this skill takes over and runs a structured three-phase process:

1. **Blueprint + Theme** — Claude generates an ASCII map of every slide (title, layout type, content approach) alongside a recommended color palette and typography, and presents both for your review and approval before touching any content.
2. **Content Generation** — After approval, Claude writes slide content against enforced rules: word density limits, bullet constraints, layout-specific formatting, and professional voice standards.
3. **File Generation** — Claude builds a `.pptx` file, runs a mandatory visual QA inspection, and delivers the finished deck.

Nothing gets built until you approve the plan. You can edit the blueprint — swap layouts, reorder slides, split or merge — before any content is written.

---

## Why the Blueprint Step Exists

AI presentation tools typically jump straight to output. The problem: structural errors are expensive to fix after generation. Wrong slide order, a layout that doesn't fit the content, a section that should have been split — these are trivial to catch in a text blueprint and time-consuming to fix in a built deck.

The ASCII blueprint makes structure visible before it's executed. The diagram is deliberately low-fidelity — boxes and labels, not polished slides — which means you'll catch structural problems instead of getting distracted by how professional the output looks. This is a deliberate application of the principle that planning before generating produces significantly better outputs.

---

## Installation

### In Claude Projects (recommended)

Place the skill file at:

```
/mnt/skills/user/slide-deck/SKILL.md
```

The folder name (`slide-deck`) is what Claude registers as the skill name. The file must be named `SKILL.md`.

### Dependency

This skill depends on the public pptx skill being available at:

```
/mnt/skills/public/pptx/SKILL.md
```

That skill handles the actual `.pptx` file construction, QA tooling, and visual inspection process. The `slide-deck` skill handles planning, structure, content rules, and voice — and delegates file generation to the pptx skill.

---

## Trigger Phrases

The skill activates on any of the following (and similar variations):

- "Build a deck about..."
- "Create a PowerPoint for..."
- "Make a presentation on..."
- "Generate slides for..."
- "Turn this into a presentation"
- Any request that results in a `.pptx` file

---

## The Three-Phase Process in Detail

### Phase 1: Blueprint + Theme

Claude presents both of the following in a single response and halts until you approve.

**ASCII Blueprint** — a structured slide map:

```
+==================================================================+
|  DECK BLUEPRINT -- [Presentation Title]                          |
|  Total slides: 10  |  Audience: Executive  |  Est. build: ~15 min|
+==================================================================+

 #  | Slide Title                      | Layout Type    | Content Approach
----|----------------------------------|----------------|--------------------------------
 1  | The Problem With Generic Training| TITLE          | Deck name + tagline
 2  | What most AI training misses     | BIG STATEMENT  | Single provocative stat
 3  | Why generic fails every time     | TWO-COLUMN     | Before/after contrast
 4  | A different approach             | FULL IMAGE     | Visual metaphor + caption
 5  | Discovery phase: what we find    | PROCESS        | 3-step numbered flow
 6  | What custom agents actually do   | DATA CALLOUT   | Key time-savings metric
 7  | Results from similar engagements | COMPARISON     | Side-by-side case stats
 8  | What the 90-day runway covers    | TIMELINE       | 4-phase milestone view
 9  | What you get on day one          | BULLETS        | 4-point deliverable list
10  | The next conversation            | CLOSING CTA    | Single ask, white space

Layout variety check:  PASSED
Bullet density check:  PASSED (10% of deck, under 30% cap)
Title length check:    PASSED (all titles <= 8 words)
Idea-per-slide check:  PASSED
```

**Theme Recommendation** — presented immediately below the blueprint:

```
+==================================================================+
|  RECOMMENDED THEME                                               |
+==================================================================+

Theme Name:   Midnight Executive
Rationale:    Authoritative feel appropriate for executive-level sales context.

  Primary    [######]  #1E2761  (navy)       -- backgrounds, dominant surfaces
  Secondary  [######]  #CADCFC  (ice blue)   -- content areas, supporting elements
  Accent     [######]  #FFFFFF  (white)      -- headlines, callouts, key numbers

Typography:
  Headers    Calibri Bold, 36-44pt
  Body       Calibri, 14-16pt
  Captions   Calibri Light, 10-12pt

Visual motif: Icons in small accent-colored circles next to section headers.
              Dark navy title and closing slides, light content slides (sandwich).

Alternatives:
  - Charcoal Minimal -- same authority, more neutral/less corporate feel
  - Ocean Gradient  -- similar gravitas, slightly warmer blue tone
```

You respond with "Approved," edit instructions, or "Skip blueprint" to override the phase entirely.

---

### Phase 2: Content Rules

Applied silently after approval. Claude enforces these without narrating them.

#### Text Density

| Rule | Value |
|---|---|
| Target words per slide | 25–40 |
| Hard maximum | 50 words |
| If exceeded | Split into two slides, noted in build summary |
| Exception | Leave-behind / reading decks (must be explicitly requested) |

#### Bullet Rules

- Maximum 5 bullets per slide
- Maximum 5–6 words per bullet line
- Maximum 2 nesting levels — no exceptions
- No bullets on BIG STATEMENT, DATA CALLOUT, FULL IMAGE, or CLOSING CTA slides — those layouts have their own content format

#### One Idea Per Slide

- One title, one message
- Slide titles containing "and" joining two distinct concepts get flagged and split before building

#### Metrics and Numbers

- Exact figures preserved — never rounded, never generalized
- Key numbers formatted prominently at display size
- "Many" / "most" / "significant" are forbidden when a real number exists or can be sourced

#### Speaker Notes Extraction

When source material includes speaker notes or scripts:

**Discard:** Delivery cues, timing notes, "welcome everyone" openers, transition phrases

**Surface to slides:** Powerful stats buried in notes, key objections addressed, specific examples that ground abstract points

---

### Phase 3: Layout Library

Every slide gets assigned one of 10 layout types. The type determines content structure — bullets are not the default.

| Layout | Best For | Avoid For |
|---|---|---|
| TITLE | Opening slide, section dividers | Content-heavy slides |
| BIG STATEMENT | Single key insight, one large stat, provocative hook | Multiple concepts |
| BULLETS | Lists, criteria, features (3–5 items minimum) | Fewer than 3 items |
| TWO-COLUMN | Comparisons, before/after, problem/solution | More than 2 categories |
| PROCESS | Numbered steps, phases, workflows | Non-sequential content |
| TIMELINE | Chronological milestones, implementation phases | Non-time-based content |
| DATA CALLOUT | ROI figures, research stats, single large number | Narrative content |
| FULL IMAGE | Emotional anchors, metaphors, section transitions | Data-heavy content |
| COMPARISON | Case studies, competitor contrast, option evaluation | More than 3 items per side |
| CLOSING CTA | Final ask, next steps, single decision | Middle-of-deck placement |

#### Visual Pacing Rules

These prevent the "all slides look the same" problem:

1. No 3 consecutive slides with the same layout type
2. BULLETS capped at 30% of total slides — redistributed automatically if exceeded
3. Every 8-slide deck gets at least 1 FULL IMAGE or BIG STATEMENT slide
4. TITLE and CLOSING CTA are exempt from variety counting
5. Preferred structure: dark backgrounds for TITLE and CLOSING CTA, light for content ("sandwich") — unless user requests a fully dark deck

#### Layout-Specific Content Notes

**BIG STATEMENT:** One headline (max 12 words). One supporting subline (max 10 words). White space fills the rest.

**TWO-COLUMN:** Left label + 2–3 tight points. Right label + 2–3 tight points. Total words across both columns ≤ 40.

**DATA CALLOUT:** The number is the hero at 60–72pt display size. Unit label below in small text. 2 supporting bullets maximum.

**PROCESS:** Numbered 1–N. Each step gets a title (3–5 words) and one supporting line (max 8 words). Arrows or connectors between steps.

**TIMELINE:** Phase name + date/timeframe + one-line deliverable. Max 5 phases per slide. More than 5 phases → split into two slides.

**FULL IMAGE:** Image occupies 80–100% of slide. Overlaid text must be short (title + optional 6-word subline) with strong contrast.

**COMPARISON:** Two labeled columns with parallel structure — same number of comparison points per side.

**CLOSING CTA:** Single ask as an action statement. Generous white space — do not fill it.

---

## Professional Voice Standards

These apply to all generated slide content.

### Language Rules

| Rule | Example |
|---|---|
| Concrete before abstract | The example or stat lands before the principle |
| Specific over vague | "57% of employees" not "many employees" |
| Active construction | "Your team uses AI daily" not "AI adoption is achieved" |
| No em dashes | Use commas, periods, or parentheses instead |

**Forbidden constructions** (AI filler — never appears in output):
- "It is worth noting"
- "It is important to remember"
- "In conclusion"
- "Notably" / "Certainly"
- "Leveraging [X] to optimize [Y]"
- Stacked superlatives: "incredibly powerful, highly effective"

### Slide Title Rules

- Outcomes and statements preferred over topic labels
  - ✅ "What 57% of Your Staff Are Already Doing"
  - ❌ "Staff AI Usage Statistics"
- Maximum 8 words
- Sentence case, not Title Case For Every Word
- No end punctuation except intentional questions

### Closing Slide Rule

The closing slide states what happens next — a specific forward action. Not "Thank You." Not an open-ended question.

---

## Available Color Themes

| Theme | Primary | Secondary | Accent | Best For |
|---|---|---|---|---|
| Midnight Executive | #1E2761 navy | #CADCFC ice blue | #FFFFFF white | Corporate, board, executive |
| Charcoal Minimal | #36454F charcoal | #F2F2F2 off-white | #212121 black | Corporate, general business |
| Ocean Gradient | #065A82 deep blue | #1C7293 teal | #21295C midnight | Technology, innovation, AI |
| Teal Trust | #028090 teal | #00A896 seafoam | #02C39A mint | Healthcare, education, nonprofit |
| Sage Calm | #84B59F sage | #69A297 eucalyptus | #50808E slate | Wellness, sustainability |
| Forest & Moss | #2C5F2D forest | #97BC62 moss | #F5F5F5 cream | Environment, nonprofit |
| Cherry Bold | #990011 cherry | #FCF6F5 off-white | #2F3C7E navy | Sales, pitch, competitive |
| Coral Energy | #F96167 coral | #F9E795 gold | #2F3C7E navy | Sales, marketing, energy |
| Berry & Cream | #6D2E46 berry | #A26769 dusty rose | #ECE2D0 cream | Financial, legal, professional services |
| Warm Terracotta | #B85042 terracotta | #E7E8D1 sand | #A7BEAE sage | Lifestyle, consulting, culture |

---

## Quality Assurance

The pptx skill's QA process is mandatory before delivery:

1. Convert generated slides to images
2. Visually inspect for layout problems, text overflow, low contrast, overlapping elements, leftover placeholders
3. Fix all issues found
4. Re-inspect affected slides
5. Repeat until a full pass finds nothing new

A build summary is delivered alongside every deck:

```
Build complete.
  Slides:         10 total (1 split made: slide 7 exceeded 50 words)
  Theme applied:  Midnight Executive -- Primary #1E2761 / Secondary #CADCFC / Accent #FFFFFF
  Layout spread:  2x TITLE, 1x BIG STATEMENT, 2x TWO-COLUMN, 1x FULL IMAGE ...
  Voice flags:    2 em dashes replaced, 1 vague metric made specific
  QA cycles:      2
```

---

## How This Differs from gamma-transformer

| | gamma-transformer | slide-deck |
|---|---|---|
| Input | Fully-specified slide content | A goal, topic, or raw content |
| Process | Format conversion to Gamma markdown | Blueprint + approval + file build |
| ASCII role | None | Mandatory Phase 1 |
| Theme selection | Not included | Phase 1, user-approved |
| Output | Markdown for Gamma's AI renderer | `.pptx` file |
| Design control | Gamma's AI decides layout | Skill assigns and enforces layout |
| Triggered by | "transform for Gamma" | "build a deck / make a PowerPoint" |

These skills are intentionally separate and should never be merged or combined.

---

## Pre-Delivery Checklist

The skill verifies the following before delivering any deck:

- [ ] Blueprint was shown and approved (or user explicitly skipped)
- [ ] Theme was shown and approved (or user explicitly skipped)
- [ ] No slide exceeds 50 words
- [ ] No 3 consecutive slides share a layout type
- [ ] BULLETS layout is 30% or fewer of total slides
- [ ] All exact metrics preserved with original numbers
- [ ] No em dashes anywhere in slide text
- [ ] No AI filler constructions anywhere in slide text
- [ ] All slide titles are 8 words or fewer
- [ ] Closing slide ends with a forward action
- [ ] pptx skill QA loop completed with visual inspection
- [ ] Build summary delivered with the file

---

## Repository Structure

```
slide-deck/
├── README.md       -- This file
└── SKILL.md        -- The skill file Claude reads and follows
```

---

*Developed for ChatCPT, LLC — AI adoption consulting, Houston TX.*
*Part of the ChatCPT Claude Skills toolkit.*
