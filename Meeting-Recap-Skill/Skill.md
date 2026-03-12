---
name: meeting-recap
description: >
  Generates structured, citation-backed meeting recaps from transcripts. Invoke whenever a user
  pastes a meeting transcript, uploads a transcript file, or uses phrases like: recap this meeting,
  generate meeting notes, summarize this call, process my Teams transcript, pull action items from
  this meeting, create meeting minutes, what were the decisions from this meeting, or any variation
  of turning a transcript into structured notes. This skill produces 8 structured sections including
  executive outcomes, decisions, action items, risks, open questions, dependencies, parking lot, and
  next checkpoint - all with timestamped speaker citations. Use this skill aggressively: if a
  transcript is present in the conversation and the user asks for any kind of summary, notes, or
  follow-up, this skill applies.
---

# Meeting Recap Skill

Generate a structured, citation-backed meeting recap from any transcript. Produces 8 sections with timestamped speaker citations. Evidence-based only — never invent details.

## Input Handling

**Accepted input forms:**
- Pasted transcript text directly in chat
- Uploaded .txt, .docx, or .pdf transcript file
- Microsoft Teams Copilot transcript export
- Zoom, Webex, or Google Meet transcript

**Required:**
- Transcript content (any format above)

**Optional (extract from transcript if not provided):**
- `meeting_title` — infer from transcript content if not stated
- `meeting_date` — extract from transcript header if present
- `attendees` — extract speaker names from transcript

**If transcript is missing:** Ask the user to paste or upload it before proceeding.

---

## Execution Protocol

### Phase 1: Transcript Intake

1. Confirm transcript is present and readable
2. Identify speakers and timestamp format
3. Note transcript quality issues (mislabeled speakers, gaps, poor audio indicators) — flag at top of output if present
4. Extract meeting metadata: date, attendees, duration if available

### Phase 2: Analysis Pass

Before writing any section, do a single full read of the transcript to identify:

- Moments where direction, scope, or risk materially changed
- Explicit confirmations ("we will", "agreed", "decided", "approved")
- Named commitments with or without owners/dates
- Unresolved questions left hanging
- Topics explicitly deferred or tabled
- Dependencies stated between people or teams
- Any stated next meeting or checkpoint

**Do not begin writing output until this pass is complete.**

### Phase 3: Section Generation

Generate all 8 sections in order. Follow the formatting rules exactly. Read `references/output-rules.md` for complete formatting spec and citation rules before writing.

### Phase 4: Quality Check

Before delivering output, verify:

- [ ] All 8 sections present (even if "None captured.")
- [ ] Every substantive bullet has at least one citation
- [ ] No invented details — everything traceable to transcript
- [ ] "None captured." used (not explained) for empty sections
- [ ] Decisions pass the explicit confirmation test
- [ ] Action items have Owner, Due, Done means, Dependencies

---

## Section Order (Always Output All 8)

1. Executive outcomes (top 3 to 5)
2. Decisions (explicitly made)
3. Action items (commitments)
4. Risks and blockers
5. Open questions (unresolved)
6. Dependencies and handoffs
7. Parking lot (deferred topics)
8. Next checkpoint

---

## Reference Files

- `references/output-rules.md` — Complete formatting spec, citation rules, silence rule, unknown rule, and all quality guards. **Read before writing any output.**
- `references/example-output.md` — Annotated example of a well-formatted recap. **Use as calibration target when uncertain about format.**

---

## Critical Constraints

- **Evidence-based only.** Do not invent details not present in the transcript.
- **Decisions are earned.** Only use the Decision label if a choice was explicitly confirmed in the transcript.
- **Silence over filler.** Empty sections get "None captured." — no explanations, no timestamps.
- **Citations only on substance.** Do not add citations to "None captured." lines or Unknown reason phrases.
