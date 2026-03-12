---
name: slide-deck
description: >
  Generates professional Microsoft PowerPoint (.pptx) decks using a mandatory
  ASCII blueprint + theme approval phase before any file is built. Use when the
  user asks to "build a deck," "create a PowerPoint," "make a presentation,"
  "generate slides," or any request that results in a .pptx file. Fully
  separate from the gamma-transformer skill — different tool, different process,
  different output. Always read /mnt/skills/public/pptx/SKILL.md before
  generating the file.
---

# Slide Deck Skill

## Overview

This skill builds professional PowerPoint decks in three phases:

1. **Blueprint + Theme** — ASCII structural map and recommended visual style, presented together for human approval
2. **Content Specification** — Apply density, layout, and voice rules to approved structure
3. **File Generation** — Build the `.pptx` using the pptx skill

**The blueprint is mandatory.** Do not generate content or build a file until the
user approves (or explicitly says "skip blueprint"). The blueprint exists because
structural corrections cost nothing before generation and everything after.

---

## Phase 1: ASCII Blueprint + Theme Recommendation

### What to present

Present the following together in a single response before asking for approval:

1. The **ASCII structural blueprint** (slide map)
2. The **theme recommendation block** (palette, typography, motif)

Both are subject to user edits. Once approved, proceed to Phase 2.

---

### Blueprint Format

```
+==================================================================+
|  DECK BLUEPRINT -- [Presentation Title]                          |
|  Total slides: X  |  Audience: [inferred]  |  Est. build: ~Y min |
+==================================================================+

 #  | Slide Title                      | Layout Type    | Content Approach
----|----------------------------------|----------------|--------------------------------
 1  | [Title]                          | TITLE          | Deck name + subtitle/tagline
 2  | [Slide 2 Title]                  | BIG STATEMENT  | Single stat or provocative hook
 3  | [Slide 3 Title]                  | TWO-COLUMN     | Before/after contrast
 4  | [Slide 4 Title]                  | PROCESS        | 3-step numbered flow
 5  | [Slide 5 Title]                  | DATA CALLOUT   | Key metric + 2 supporting points
 6  | [Slide 6 Title]                  | FULL IMAGE     | Visual metaphor + caption only
 7  | [Slide 7 Title]                  | COMPARISON     | Side-by-side case study stats
 8  | [Slide 8 Title]                  | BULLETS        | 4-point diagnostic list
 9  | [Slide 9 Title]                  | TIMELINE       | 4-phase milestone view
10  | [Slide 10 Title]                 | CLOSING CTA    | Single ask, white space dominant

Layout variety check:  PASSED  (no 3 consecutive identical layouts)
Bullet density check:  PASSED  (BULLETS = 10% of deck, under 30% cap)
Title length check:    PASSED  (all titles <= 8 words)
Idea-per-slide check:  PASSED  (no titles contain "and" joining two concepts)

Reply with:
  "Approved" to proceed
  Specific edits (e.g., "Swap slides 4 and 6" / "Change slide 3 to TIMELINE")
  "Skip blueprint" to bypass this phase entirely
```

**Validation checks to run before showing blueprint:**
- Flag any slide title over 8 words and shorten proactively
- Flag any title containing "and" joining two distinct concepts and suggest a split
- Flag 3+ consecutive slides with same layout type and reorder before presenting
- Flag if BULLETS layout exceeds 30% of total slides and redistribute
- Flag if deck has 8+ slides and contains zero FULL IMAGE or BIG STATEMENT slides and add one

---

### Theme Recommendation Block

Present immediately below the blueprint, before asking for approval.

**Selection logic -- choose the theme that best matches the presentation context:**

| Context Signals | Recommended Theme |
|---|---|
| Corporate / executive / board | Midnight Executive or Charcoal Minimal |
| Healthcare, education, nonprofit | Teal Trust or Sage Calm |
| Sales, pitch, competitive | Cherry Bold or Coral Energy |
| Financial, legal, professional services | Midnight Executive or Berry & Cream |
| Technology, innovation, AI | Ocean Gradient or Charcoal Minimal |
| Sustainability, environment, wellness | Forest & Moss or Sage Calm |
| General business (no strong signal) | Teal Trust or Charcoal Minimal |

**Theme block format:**

```
+==================================================================+
|  RECOMMENDED THEME                                               |
+==================================================================+

Theme Name:   [e.g., Midnight Executive]
Rationale:    [1 sentence -- why this fits the audience/topic]

  Primary    [######]  #1E2761  (navy)       -- backgrounds, dominant surfaces
  Secondary  [######]  #CADCFC  (ice blue)   -- content areas, supporting elements
  Accent     [######]  #FFFFFF  (white)      -- headlines, callouts, key numbers

Typography:
  Headers    [Font Name] Bold, 36-44pt
  Body       [Font Name], 14-16pt
  Captions   [Font Name] Light, 10-12pt

Visual motif: [1-2 sentences describing the repeating design element and
               dark/light slide structure -- e.g., "Icons in small accent-colored
               circles next to section headers. Dark navy title and closing slides,
               light content slides (sandwich structure)."]

Alternatives if you prefer a different feel:
  - [Theme B name] -- [one-line description of vibe difference]
  - [Theme C name] -- [one-line description of vibe difference]

Reply with "Approved" or specify changes (e.g., "Use Coral Energy instead" /
"Keep the palette but change headers to Georgia").
```

**Available palettes:**

| Theme Name | Primary | Secondary | Accent |
|---|---|---|---|
| Midnight Executive | #1E2761 navy | #CADCFC ice blue | #FFFFFF white |
| Forest & Moss | #2C5F2D forest | #97BC62 moss | #F5F5F5 cream |
| Coral Energy | #F96167 coral | #F9E795 gold | #2F3C7E navy |
| Warm Terracotta | #B85042 terracotta | #E7E8D1 sand | #A7BEAE sage |
| Ocean Gradient | #065A82 deep blue | #1C7293 teal | #21295C midnight |
| Charcoal Minimal | #36454F charcoal | #F2F2F2 off-white | #212121 black |
| Teal Trust | #028090 teal | #00A896 seafoam | #02C39A mint |
| Berry & Cream | #6D2E46 berry | #A26769 dusty rose | #ECE2D0 cream |
| Sage Calm | #84B59F sage | #69A297 eucalyptus | #50808E slate |
| Cherry Bold | #990011 cherry | #FCF6F5 off-white | #2F3C7E navy |

**Typography pairings (safe system fonts):**

| Header | Body | Character |
|---|---|---|
| Georgia | Calibri | Classic authority |
| Arial Black | Arial | Bold impact |
| Calibri | Calibri Light | Clean modern |
| Cambria | Calibri | Formal credibility |
| Trebuchet MS | Calibri | Approachable modern |

---

## Phase 2: Content Rules

Apply silently once blueprint and theme are approved. Do not narrate these to
the user -- just enforce them.

### Text Density

- Target: 25-40 words of text per slide
- Maximum: 50 words per slide (hard limit)
- If a slide exceeds 50 words: split into two slides and note the split in the build summary
- Exception: User-specified leave-behind or reading decks -- must be explicitly stated by user

### Bullet Rules

- Maximum 5 bullets per slide
- Maximum 5-6 words per bullet line
- Maximum 2 nesting levels -- no exceptions
- When layout type is BIG STATEMENT, DATA CALLOUT, FULL IMAGE, or CLOSING CTA:
  do not use bullets -- use the layout's native content format instead

### One Idea Per Slide

- One title, one message per slide
- Slide title containing "and" joining two distinct concepts: flag and split before building

### Metrics and Numbers

- Preserve exact figures -- never round, never generalize
- Format key numbers prominently (large callout size, accent color)
- Specific always beats vague: "40 minutes saved daily" not "significant time savings"
- "Many" / "most" / "significant" are forbidden when a real number exists or can be sourced

### Speaker Notes Extraction

When working from source content that includes speaker notes or presentation scripts:

Discard: Delivery cues, timing notes, filler transition phrases, "welcome everyone"
openers, apologies, and conversational throat-clearing.

Surface to slide content: Powerful stats cited only in notes, key objections
addressed, strong audience questions, specific examples that ground abstract points.

---

## Phase 3: Layout Library

### The 10 Layout Types

Every slide in the blueprint is assigned exactly one layout type. The type
drives the content structure -- bullets are not the default.

| Layout | Best For | Avoid For |
|---|---|---|
| TITLE | Opening slide, section dividers | Content-heavy slides |
| BIG STATEMENT | Single key insight, provocative hook, one large stat | Multiple concepts |
| BULLETS | Lists, criteria, features (3-5 items minimum) | Fewer than 3 items |
| TWO-COLUMN | Comparisons, before/after, problem/solution | More than 2 categories |
| PROCESS | Numbered steps, phases, workflows | Non-sequential content |
| TIMELINE | Chronological milestones, implementation phases | Non-time-based content |
| DATA CALLOUT | ROI figures, research stats, single large numbers | Narrative or conceptual content |
| FULL IMAGE | Emotional anchors, metaphors, section transitions | Data-heavy content |
| COMPARISON | Case studies, competitor contrast, option evaluation | More than 3 items per side |
| CLOSING CTA | Final ask, next steps, single decision | Middle-of-deck placement |

### Visual Pacing Rules (Mandatory)

1. No 3 consecutive slides with the same layout type
2. BULLETS capped at 30% of total deck slides -- if exceeded, redistribute to DATA CALLOUT,
   TWO-COLUMN, or PROCESS as appropriate for the content
3. Every 8-slide deck gets at least 1 FULL IMAGE or BIG STATEMENT slide -- visual pacing requirement
4. TITLE and CLOSING CTA are exempt from variety counting (structural slides, not content slides)
5. Dark/light contrast structure preferred: dark background for TITLE and CLOSING CTA, lighter
   backgrounds for content slides ("sandwich" structure) -- unless user specifies a fully dark deck

### Layout-Specific Content Notes

**BIG STATEMENT:** One headline, max 12 words. One supporting stat or subline, max 10 words.
Nothing else. White space does the work.

**TWO-COLUMN:** Left column label + 2-3 tight points. Right column label + 2-3 tight points.
Total words across both columns <= 40.

**DATA CALLOUT:** The number is the hero -- 60-72pt display size. Unit label below in small
text. 2 supporting bullet points maximum underneath.

**PROCESS:** Numbered 1-N. Each step gets a title (3-5 words) and one supporting line
(max 8 words). Arrows or connectors between steps.

**TIMELINE:** Phase name + date/timeframe + one-line deliverable. Max 5 phases per timeline
slide. If more phases needed: split into two slides.

**FULL IMAGE:** Image occupies 80-100% of slide. Any text overlaid must be short (title +
optional 6-word subline) with strong contrast against image.

**COMPARISON:** Two labeled columns. Parallel structure -- same number of comparison points
on each side. Avoid mixing sentence lengths.

**CLOSING CTA:** Single ask stated as an action ("Schedule the discovery call" not
"Questions?"). Date or deadline if applicable. Contact info if appropriate. Generous white
space -- do not fill it.

---

## Phase 4: Professional Voice Standards

Apply to all generated slide content. These hold in professional contexts regardless
of industry or audience.

### Language Rules

- Concrete before abstract -- the example, stat, or before/after lands before the principle
- Specific over vague -- "57% of employees" not "many employees"; "6 weeks" not "quickly"
- Active construction -- "Your team uses AI daily" not "AI adoption is achieved by teams"
- No em dashes -- use commas, periods, or parentheses instead
- No AI-sounding filler -- forbidden constructions:
    "It is worth noting"
    "It is important to remember"
    "In conclusion"
    "Notably"
    "Certainly"
    "Leveraging [X] to optimize [Y]"
    "Incredibly powerful, highly effective" (stacked superlatives -- pick one or cut both)

### Slide Title Rules

- Written as outcomes or statements where possible, not topic labels
    Good: "What 57% of Your Staff Are Already Doing"
    Avoid: "Staff AI Usage Statistics"
- Maximum 8 words
- Sentence case, not Title Case For Every Word
- No punctuation at end of titles except when a question is intentional

### Closing Slide Rule

End with forward momentum -- a specific next action. Not "Thank You." Not an open-ended
question. The closing slide tells the audience what happens next, not what just happened.

---

## Phase 5: File Generation

Once blueprint and theme are both approved:

1. Read /mnt/skills/public/pptx/SKILL.md -- follow its creation, design, and QA
   instructions in full
2. Apply approved theme (palette, typography, visual motif) to all slides
3. Apply layout types from approved blueprint to each slide
4. Apply Phase 2 content rules during content writing
5. Apply Phase 4 voice rules to all generated text
6. Run the pptx skill's mandatory QA loop -- visual inspection is required before delivery
7. Output file to /mnt/user-data/outputs/[descriptive-deck-name].pptx
8. Deliver via present_files tool

### Build Summary

Include a brief summary after file delivery:

  Build complete.
    Slides:         X total (note any splits made from original blueprint)
    Theme applied:  [Theme Name] -- Primary #XXXXXX / Secondary #XXXXXX / Accent #XXXXXX
    Layout spread:  [e.g., 2x TITLE, 1x BIG STATEMENT, 3x TWO-COLUMN ...]
    Voice flags:    [Any em dashes caught / vague metrics replaced / titles shortened]
    QA cycles:      [Number of fix-and-verify rounds completed]

---

## Separation from gamma-transformer

| | gamma-transformer | slide-deck |
|---|---|---|
| Input | Fully-specified slide content | A goal, topic, or raw content |
| Process | Format conversion to markdown | Blueprint + approval + file build |
| ASCII role | None | Mandatory Phase 1 |
| Theme selection | Not included | Phase 1, user-approved |
| Output | Markdown for Gamma's AI | .pptx file |
| Design control | Gamma's AI decides layout | Skill assigns and enforces layout |
| Triggered by | "transform for Gamma" | "build a deck / make a PowerPoint" |

---

## Pre-Delivery Checklist

Before delivering any deck, confirm:

- [ ] Blueprint was shown and approved (or user explicitly skipped)
- [ ] Theme was shown and approved (or user explicitly skipped)
- [ ] No slide exceeds 50 words
- [ ] No 3 consecutive slides share a layout type
- [ ] BULLETS layout is 30% or less of total slides
- [ ] All exact metrics preserved with original numbers
- [ ] No em dashes anywhere in slide text
- [ ] No AI filler constructions anywhere in slide text
- [ ] All slide titles are 8 words or fewer
- [ ] Closing slide ends with a forward action, not "Thank You"
- [ ] pptx skill QA loop completed with visual inspection
- [ ] Build summary delivered alongside the file
