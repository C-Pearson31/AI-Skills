# CP's Teams Meeting Recap Prompt

A custom Microsoft Teams Copilot summary template that replaces the default AI meeting summary with a structured, citation-backed, decision-grade recap.

---

## Why This Is Better Than the Default

Microsoft Teams Copilot's built-in meeting summary is a paragraph or a short bullet list of topics discussed. It does not tell you:

- **What was actually decided** (not just discussed)
- **Who owns what** and when it is due
- **What is blocking progress**
- **What questions are still unresolved**
- **What got deferred** and why

This prompt fixes all of that. Every section is structured for action, not just recall.

### What You Get

| Section | What It Captures |
|---|---|
| **Executive Outcomes** | The 3–5 things that materially changed direction, risk, or next steps — with a "Why selected" justification |
| **Decisions** | Only things that were explicitly agreed or confirmed — not things that were just talked about |
| **Action Items** | Owner, due date, done criteria, and dependencies — structured like a real task |
| **Risks & Blockers** | Severity rating, impact, likelihood, mitigation, and owner |
| **Open Questions** | What is unresolved, who owns the answer, and when it is needed |
| **Dependencies & Handoffs** | What one team or person needs from another, and why it matters |
| **Parking Lot** | Topics that got deferred, why, and what happens next |
| **Next Checkpoint** | Date, purpose, and prep required — only if explicitly stated |

### Key Design Principles

- **Citations only on substantive content.** Every outcome, decision, and action item includes a (Speaker, HH:MM:SS) timestamp so you can verify it in the transcript.
- **Silence rule.** If a section has nothing, it says "None captured." — no filler, no noise.
- **Evidence-based only.** The prompt explicitly instructs Copilot not to invent details.
- **Decisions are earned.** Something only appears as a Decision if a choice was explicitly confirmed in the transcript.

---

## How to Install It in Microsoft Teams

This is a one-time setup. After that, it works automatically on every meeting.

### Step 1 — Open a Teams Meeting

Go to any past meeting in your Teams calendar. Click on it to open the meeting details.

### Step 2 — Go to the Recap Tab

Inside the meeting, click the **Recap** tab at the top (it may also appear as **Notes** depending on your version).

### Step 3 — Click "AI Summary"

You will see tabs along the top: Notes, AI summary, Custom summary, Mentions, Transcript. Click **Custom summary**.

### Step 4 — Create a New Template

Click **+ Create template** on the left side of the Custom summary screen.

### Step 5 — Open the Prompt File

Open the file `teams-meeting-recap-prompt.txt` (included in this repo). Select all the text and copy it.

### Step 6 — Paste the Prompt

In the "Describe your summary format" dialog box that appears, paste the full prompt text into the text area.

### Step 7 — Save and Apply

Click **Save and Apply**. Teams will name it and save it as a reusable template.

### Step 8 — Run It

Click your saved template from the Custom summary tab. Copilot will regenerate the meeting summary using your prompt format.

---

## Tips

- **Re-run anytime.** You can apply this template to any meeting that has a transcript, not just new ones.
- **It only works if there is a transcript.** Make sure transcription is enabled before your meetings. In Teams, the meeting organizer can start transcription from the meeting controls.
- **The output quality depends on the transcript quality.** If speakers are mislabeled or the transcript is garbled, citations may be off.
- **You can edit the template.** Go back to Custom summary, click the template name, and edit the prompt text if you want to adjust sections.

---

## Files in This Repo

| File | What It Is |
|---|---|
| `teams-meeting-recap-prompt.txt` | The full prompt — copy and paste this into Teams |
| `README.md` | This file — setup instructions and context |

---

## Credit

Built by Chris Pearson. Designed for use with Microsoft Teams Copilot's Custom Summary feature.
