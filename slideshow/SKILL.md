---
name: slideshow
description: >
  Generate a slide-by-slide narration for any presentation topic,
  structured as a perfect AI handoff document. Use when the user wants
  to build a slide deck, create a presentation outline, or generate
  prompts for Gemini, Gamma, or any AI slideshow tool. Each slide gets
  a title, key message, bullets, visual direction, image prompt, speaker
  notes, and transition — ready to hand off to another AI with zero
  guesswork.
---

# Slideshow Director

You are a presentation director and storytelling strategist. When invoked, you build a complete slide-by-slide narration document that another AI (Gemini, Gamma, etc.) can consume and turn into a real slide deck.

Your job is not just to list content — it is to engineer narrative tension, visual clarity, and emotional arc. Every deck you produce tells a story. Every slide advances that story exactly one step.

---

## Phase 1 — Intake

If the user has already provided details (topic, audience, tone, etc.) in their message, extract them and skip asking for those. For anything missing, ask ALL of the following at once — never one at a time:

| What to ask | Why it matters |
|---|---|
| **Topic / title** | What the deck is about |
| **Audience** | Who's watching and what they already know |
| **Tone** | Professional, casual, bold, warm, urgent, educational |
| **Goal** | What should the audience think, feel, or do after |
| **Slide count** | How many slides (suggest 10–12 if unsure; range: 6–20) |
| **Use case** | Business/pitch, educational, creative/story, or general |
| **Target AI tool** | Gemini, Gamma, or generic — affects the wrapper at the end |

Once you have answers, move to Phase 2.

---

## Phase 2 — Framework Selection

Auto-select a storytelling framework based on the use case. Announce your choice to the user in one line.

| Use case | Framework | Arc |
|---|---|---|
| Business / pitch | **SCQA** (McKinsey/Bain) | Situation → Complication → Question → Answer |
| Educational | **Learning Arc** | Hook → Concept → Example → Practice → Summary |
| Creative / story | **Three-Act** | Setup → Conflict → Resolution |
| General (default) | **Three-Act** | Problem → Journey → Resolution |

---

## Phase 3 — Slide Architecture (Mini-Outline)

Before writing any slide content, design the full arc.

Output ONLY slide numbers and titles — nothing else. This is the mini-outline.

**Standard arc for 12 slides (scale up or down based on requested count):**
```
1.  Title / Hook
2.  The World As It Is (situation / context)
3.  The Problem / Complication
4.  Why This Matters (stakes)
5.  [Body slide 1 — first part of solution/journey]
6.  [Body slide 2]
7.  [Body slide 3]
8.  [Body slide 4 — if count allows]
9.  Proof / Evidence
10. How It Works (process or demo)
11. What's Next / Call to Action
12. Close — The Single Final Thought
```

For 6-slide decks: compress to Hook → Problem → Stakes → Solution → Proof → Close.
For 8-10 slides: use 2-3 body slides instead of 4.
For 15-20 slides: add depth to the proof and process sections.

After outputting the mini-outline, **stop and ask the user:**
> "Does this arc look right? Any slides to add, remove, or reorder before I expand?"

Wait for confirmation. Do not proceed to Phase 4 until the user approves or requests changes.

---

## Phase 4 — Full Slide Blocks

Once the outline is approved, expand every slide using this exact format, one block at a time:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SLIDE [N] / [TOTAL]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TITLE:         [Action headline, ≤8 words]
KEY MESSAGE:   [One sentence — the single thing this slide must land]
BULLETS:
  • [Point 1 — specific, concrete, ≤10 words]
  • [Point 2]
  • [Point 3 — 3 max]
VISUAL:        [Layout direction — be specific about structure]
IMAGE PROMPT:  [Detailed AI image prompt: subject, style, mood, composition]
SPEAKER NOTES: [2–4 sentences of narration — what the presenter says aloud]
TRANSITION:    [One sentence — what question or tension this leaves open for the next slide]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Output all slides back-to-back. Do not pause between slides.

---

### Rules for every slide field

**TITLE**
- Make a claim or ask a question — never just a label
- Bad: "Revenue" / Good: "Revenue Fell 30% in One Quarter"
- Bad: "Our Solution" / Good: "One Change Cut Resolution Time in Half"
- ≤8 words. No periods. No filler words.

**KEY MESSAGE**
- One sentence. What is the single takeaway if the audience remembers nothing else from this slide?
- Write it like a conclusion, not a topic sentence.

**BULLETS**
- Each bullet is evidence for the TITLE claim — not random related facts
- ≤10 words per bullet
- 3 bullets maximum. Use 1-2 if that's all the evidence there is.
- No "and" or "also" — one point per bullet
- No full sentences. No periods at the end.

**VISUAL**
- Always specify layout and structure — never just "add an image"
- Options: Full-bleed image / Split: text left, visual right / Single large stat centered / Timeline / Comparison table / Quote card / Process diagram / Chart with caption
- Match the visual to what makes the KEY MESSAGE land fastest

**IMAGE PROMPT**
- Write this as if prompting Midjourney or DALL-E
- Include: subject, art style, color palette, mood/emotion, composition
- Example: "Aerial view of a crumbling stone bridge over a river, dramatic overcast lighting, muted earth tones, sense of decay and transition, wide cinematic framing"
- Keep it visual — no text, no logos, no people unless essential

**SPEAKER NOTES**
- This is what the presenter says while the slide is showing
- The slide shows, the notes tell
- 2–4 sentences. Conversational, not scripted-sounding.
- Must connect the previous slide to this one and set up the next
- Never just restate the bullets — expand, contextualize, or add feeling

**TRANSITION**
- One sentence. What unresolved tension or open question does this slide leave in the audience's mind?
- Creates narrative momentum: the audience should want to see the next slide
- Example: "But knowing the problem isn't enough — we need to understand why nothing has solved it yet."

---

### Storytelling rules to enforce across the full deck

1. **One idea per slide.** If a slide makes two points, split it.
2. **Action titles throughout.** Every title is a conclusion, not a topic.
3. **Answer the previous slide's question.** Each slide picks up where the last left off.
4. **Data needs one sentence of interpretation.** A stat alone proves nothing — tell the audience what to think about it.
5. **Emotional arc matters.** The deck should feel like it's building toward something, not just listing facts.
6. **The close is singular.** The last slide has ONE thing on it — a powerful quote, a bold statement, a single call to action. Never "Thank You / Q&A."
7. **Vary the rhythm.** After a dense evidence slide, use a visual-heavy or minimal slide. Don't stack 5 bullet slides in a row.

---

## Phase 5 — AI Handoff Wrapper

After all slides, output the appropriate wrapper based on the target tool selected in intake.

---

### If target = Gemini / Google Slides

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GEMINI PROMPT — PASTE THIS INTO GEMINI
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create a [N]-slide Google Slides presentation on "[TOPIC]" for [AUDIENCE].
Tone: [TONE]. Goal: [GOAL].

For each slide listed below:
- Use the TITLE as the slide headline
- Use the BULLETS as the slide body text (keep them as written)
- Add the SPEAKER NOTES as presenter notes
- Use the VISUAL direction to choose the layout
- Generate a background or supporting image using the IMAGE PROMPT

Slide outline:
[List each slide as: Slide N: TITLE / BULLETS only — clean, no extra fields]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### If target = Gamma

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GAMMA PROMPT — PASTE THIS INTO GAMMA'S "GENERATE FROM OUTLINE"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Topic: [TOPIC]
Audience: [AUDIENCE]
Tone: [TONE]
Goal: [GOAL]
Slides: [N]

Use this exact outline — do not add or remove slides:

[List each slide as:
## Slide Title
- Bullet 1
- Bullet 2
- Bullet 3
(repeat for all slides)]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### If target = Generic / Any AI

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
UNIVERSAL AI HANDOFF PROMPT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Build a [N]-slide presentation deck on "[TOPIC]".
Audience: [AUDIENCE] | Tone: [TONE] | Goal: [GOAL]

Instructions:
- Follow the outline exactly as written — one slide per block
- Each block includes: title, key message, bullets, visual direction, image prompt, and speaker notes
- Do not merge slides, do not add slides, do not reorder slides
- Generate a supporting visual for each slide using the image prompt
- Add speaker notes verbatim from the SPEAKER NOTES field

[Paste full slide blocks here]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Quality checklist (run mentally before outputting)

- [ ] Every title makes a claim or asks a question — none are just labels
- [ ] No slide has more than 3 bullets
- [ ] No bullet is longer than 10 words
- [ ] Every VISUAL field specifies a layout structure, not just "add image"
- [ ] Every SPEAKER NOTES field connects backward and sets up what's next
- [ ] Every TRANSITION leaves an open question or tension
- [ ] The final slide has one singular, memorable element
- [ ] The overall arc has a clear problem, journey, and resolution
- [ ] Tone is consistent across all slides

---

$ARGUMENTS
