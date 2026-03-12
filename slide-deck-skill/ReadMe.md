# slide-deck

**A Claude Projects skill for building professional Microsoft PowerPoint decks.**

This skill enforces a mandatory planning phase before generating a single slide: an overview blueprint table, per-slide ASCII wireframes that visually picture each layout, and a recommended color theme — all reviewed and approved before any file is built.

---

## What This Skill Does

When you ask Claude to build a PowerPoint deck, this skill runs a structured four-phase process:

1. **Blueprint** — A quick-scan overview table showing every slide's title, layout type, and content approach. You approve the structure before any content is written.
2. **Per-Slide Wireframes** — ASCII drawings that actually picture the spatial layout of every non-trivial slide. You see where the headline sits, how the content flows, what SmartArt shape is recommended, and where images and overlays land — before the build starts.
3. **Theme Recommendation** — Color palette, typography pairing, and visual motif. Presented alongside the wireframes for a single approval.
4. **File Generation** — Claude builds the `.pptx`, runs a mandatory visual QA inspection, and delivers the finished deck.

Nothing gets built until you approve the plan. You can edit the blueprint, adjust wireframe layouts, swap SmartArt shapes, or change the theme before a single slide is constructed.

---

## Why the Wireframe Step Exists

Most AI presentation tools jump straight to output. The problem: spatial errors — wrong SmartArt shape, a layout that doesn't fit the content, a DATA CALLOUT where the number isn't actually the hero — are trivial to catch in an ASCII picture and time-consuming to fix in a built deck.

The wireframes give Claude a visual contract to build against, not just a category label. "PROCESS slide" is a label. A chevron with three boxes and arrows between them is a picture.

---

## Installation

### In Claude Projects (recommended)

Place the skill file at:

```
/mnt/skills/user/slide-deck/SKILL.md
```

The folder name (`slide-deck`) is what Claude registers as the skill name. The file must be named `SKILL.md`.

### Dependency

This skill depends on the public pptx skill at:

```
/mnt/skills/public/pptx/SKILL.md
```

That skill handles `.pptx` file construction, QA tooling, and visual inspection. The `slide-deck` skill handles planning, wireframes, content rules, and voice — and delegates file generation to the pptx skill.

---

## Trigger Phrases

The skill activates on:

- "Build a deck about..."
- "Create a PowerPoint for..."
- "Make a presentation on..."
- "Generate slides for..."
- "Turn this into a presentation"
- Any request that results in a `.pptx` file

---

## The Four-Phase Process in Detail

### Phase 1: Overview Blueprint

A table showing the full deck structure. The user confirms slide order, layout types, and content approach before wireframes are drawn.

```
+====================================================================+
|  DECK BLUEPRINT -- Why Generic AI Training Fails                   |
|  Total slides: 10  |  Audience: Mid-market executive  |  ~15 min  |
+====================================================================+

 #  | Slide Title                        | Layout Type    | Content Approach
----|------------------------------------+----------------+--------------------------------
 1  | Why generic AI training fails      | TITLE          | Deck name + tagline
 2  | What your staff are already doing  | BIG STATEMENT  | 57% stat as hook
 3  | Generic training vs. discovery     | COMPARISON     | Side-by-side contrast
 4  | How the discovery phase works      | PROCESS        | 3-step linear chevron
 5  | What we find in every org          | DATA CALLOUT   | Key time-savings metric
 ...
```

### Phase 2: Per-Slide Wireframes

After blueprint approval, Claude draws an ASCII wireframe for every non-trivial slide. Trivial layouts (TITLE, BULLETS, CLOSING CTA) remain as table rows — their structure needs no picture.

**Example: PROCESS (Linear)**
```
+----------------------------------------------------------+
|  How the discovery phase works                           |
+----------------------------------------------------------+
|                                                          |
|  +----------+      +----------+      +----------+       |
|  |          |  ->  |          |  ->  |          |       |
|  | Attend   |      | Collect  |      | Pre-build|       |
|  | meetings |      | documents|      | agents   |       |
|  +----------+      +----------+      +----------+       |
|                                                          |
|  4-6 weeks inside your organization before training     |
|                                                          |
+----------------------------------------------------------+
  SmartArt:  Chevron Process (PowerPoint: Process > Chevron Process)
```

**Example: DATA CALLOUT**
```
+----------------------------------------------------------+
|  The number your board is asking about                   |
+----------------------------------------------------------+
|                                                          |
|               +-----------------+                        |
|               |      57%        |  <- 60-72pt, accent    |
|               +-----------------+                        |
|                                                          |
|       of employees already use AI at work                |
|            (KPMG / University of Melbourne, 2024)        |
|                                                          |
|   • Most are hiding it from their managers               |
|   • Without policy, risk compounds daily                 |
|                                                          |
+----------------------------------------------------------+
```

**Example: COMPARISON**
```
+----------------------------------------------------------+
|  Generic training vs. the discovery approach             |
+----------------------------------------------------------+
|                          |                              |
|  +--------------------+  |  +--------------------+     |
|  |  GENERIC TRAINING  |  |  |  DISCOVERY-FIRST   |     |
|  +--------------------+  |  +--------------------+     |
|  | • Shows up, leaves |  |  | • 4-6 wks discovery|     |
|  | • Generic prompts  |  |  | • Pre-built agents |     |
|  | • One-day workshop |  |  | • 90-day support   |     |
|  +--------------------+  |  +--------------------+     |
|                          |                              |
+----------------------------------------------------------+
```

**Example: FULL IMAGE**
```
+----------------------------------------------------------+
|:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::|
|::::::  IMAGE FILLS ENTIRE SLIDE CANVAS  ::::::::::::::::::|
|::  [empty conference room, chairs facing blank screen]  ::|
|:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::|
|                                                          |
|  The training happened. Nothing changed.                 |
|  [dark overlay band behind text]                         |
|                                                          |
+----------------------------------------------------------+
  Text position: Bottom-left
```

### Phase 3: Theme Recommendation

Presented alongside wireframes. Includes palette, typography, visual motif, and two alternatives.

### Phase 4: File Generation

Claude builds the deck, runs visual QA inspection, and delivers a build summary with the file.

---

## SmartArt Selection Logic

For PROCESS slides, the shape is chosen based on how the process actually works:

| Process Behavior | SmartArt Shape | PowerPoint Location |
|---|---|---|
| Steps in order, left to right | Chevron/Arrow Chain | Process > Chevron Process |
| Steps repeat or loop | Cycle/Circle | Cycle > Basic Cycle |
| Volume narrows at each stage | Funnel | Relationship > Funnel |
| Each step builds on the last | Staircase | Process > Step Up Process |
| One hub connects to outputs | Radial/Hub-Spoke | Relationship > Basic Radial |

---

## Available Color Themes

| Theme | Primary | Secondary | Accent | Best For |
|---|---|---|---|---|
| Midnight Executive | #1E2761 navy | #CADCFC ice blue | #FFFFFF white | Corporate, board, executive |
| Charcoal Minimal | #36454F charcoal | #F2F2F2 off-white | #212121 black | Corporate, general business |
| Ocean Gradient | #065A82 deep blue | #1C7293 teal | #21295C midnight | Technology, AI, innovation |
| Teal Trust | #028090 teal | #00A896 seafoam | #02C39A mint | Healthcare, education, nonprofit |
| Sage Calm | #84B59F sage | #69A297 eucalyptus | #50808E slate | Wellness, sustainability |
| Forest & Moss | #2C5F2D forest | #97BC62 moss | #F5F5F5 cream | Environment, nonprofit |
| Cherry Bold | #990011 cherry | #FCF6F5 off-white | #2F3C7E navy | Sales, pitch, competitive |
| Coral Energy | #F96167 coral | #F9E795 gold | #2F3C7E navy | Sales, marketing, energy |
| Berry & Cream | #6D2E46 berry | #A26769 dusty rose | #ECE2D0 cream | Financial, legal, professional |
| Warm Terracotta | #B85042 terracotta | #E7E8D1 sand | #A7BEAE sage | Lifestyle, culture, consulting |

---

## Content Rules (Enforced Silently)

| Rule | Value |
|---|---|
| Target words per slide | 25–40 |
| Hard word maximum | 50 (exceeded = slide splits) |
| Max bullets per slide | 5 |
| Max words per bullet | 5–6 |
| Max nesting levels | 2 |
| Slide title max length | 8 words |
| BULLETS layout cap | 30% of deck |
| Consecutive same layout | Never 3 in a row |

---

## Voice Standards

- No em dashes — commas, periods, or parentheses instead
- Specific over vague — "57%" not "many"
- Outcomes as slide titles, not topic labels
- No AI filler: "It is worth noting," "Notably," "Certainly," "In conclusion," stacked superlatives
- Closing slide: forward action, not "Thank You"

---

## Pre-Delivery Checklist

- [ ] Blueprint shown and approved
- [ ] Per-slide wireframes shown and approved for all non-trivial slides
- [ ] SmartArt shape specified in wireframe for every PROCESS slide
- [ ] Theme shown and approved
- [ ] No slide exceeds 50 words
- [ ] No 3 consecutive slides share a layout type
- [ ] BULLETS layout is 30% or fewer of total slides
- [ ] All exact metrics preserved
- [ ] No em dashes in slide text
- [ ] No AI filler in slide text
- [ ] All titles 8 words or fewer
- [ ] Closing slide ends with forward action
- [ ] pptx skill QA loop completed with visual inspection
- [ ] Build summary delivered with the file

---

## Repository Structure

```
slide-deck/
├── README.md    ← This file
└── SKILL.md     ← The skill file Claude reads and executes
```

---

*Developed for ChatCPT, LLC — AI adoption consulting, Houston TX.*
*Part of the ChatCPT Claude Skills toolkit.*
