# 00 — Runtime, Word, and Shot Budgets (English Calibration)

Everything in this file exists to answer one question: **for X seconds of screen time, how many words, scenes, and shots am I allowed?**

Get this wrong and nothing downstream can be saved. The script will be over-length, the shot list will be over-built, the voice track will be rushed, and the edit will be a salvage operation.

---

## 1. Where the numbers come from

Three separate rates are in play, and confusing them is the most common budgeting error.

### 1.1 Speaking rate

English conversational speech runs **140–160 words per minute**, or roughly **2.3–2.7 words per second**. That is normal dramatic delivery with room to breathe.

Push to **180 wpm (3.0 wps)** and you get urgency, trailers, panic, and sports commentary. Actors can do it, but not for long, and the listener gets tired.

Beyond 3.0 wps you are no longer writing dialogue. You are writing a disclaimer that must be read aloud at speed — legal, medical, end-card. It does not act.

### 1.2 Script body rate

A finished script is not all dialogue. It is dialogue *plus* action description, and action lines describe stretches of screen time that contain no words at all.

Blend the two and the full script settles at about **2.2 words per second** of screen time.

This is the number you use for "how long should my script file be."

### 1.3 Page rate

In standard US screenplay format — Letter paper, Courier 12pt, 1-inch margins, dialogue blocks single-spaced with a blank line between — **one page runs about one minute** and contains roughly **190 words**.

The page rule survives because it is robust: it holds across genre, across dialogue-heavy and action-heavy material, and across most production realities. Use it when someone talks in pages instead of minutes.

### 1.4 Which rate to use when

| Question asked | Use | Example |
|---|---|---|
| "How many words should the script be?" | 2.2 wps | 90 s → ~200 words |
| "Can this line fit?" | 2.5 wps, 3.0 max | 8 s of dialogue → ≤ 20–24 words |
| "How many pages?" | 1 page ≈ 1 min | 12 min → ~12 pages |
| "Is my VO over-length?" | 2.7 wps | 30 s VO reading at 55 words = fine; 90 words = too long |

---

## 2. Reference tables

### 2.1 Runtime → content ceiling

| Runtime | Script words (2.2 wps) | Dialogue words (max) | Shots @3.5 | Scenes (guide) |
|---|---|---|---|---|
| 15 s | 33 | 38 | 4 | 1 |
| 30 s | 66 | 75 | 8 | 1 |
| 45 s | 99 | 113 | 13 | 1–2 |
| 60 s | 132 | 150 | 17 | 2 |
| 90 s | 198 | 225 | 26 | 2–3 |
| 2 min | 264 | 300 | 34 | 3–4 |
| 3 min | 396 | 450 | 51 | 4–5 |
| 5 min | 660 | 750 | 86 | 5–7 |
| 8 min | 1,056 | 1,200 | 137 | 7–8 |
| 10 min | 1,320 | 1,500 | 171 | 8–12 |
| 20 min | 2,640 | 3,000 | 343 | 14–18 |
| 30 min | 3,960 | 4,500 | 514 | 18–20 |

Treat the scene column as texture, not law — a 90-second piece can be one continuous take or three locations. The word and shot columns are the hard ones.

### 2.2 Dialogue density by format

Different formats tolerate very different amounts of talk.

| Format | Typical runtime | Dialogue share | Why |
|---|---|---|---|
| Vertical drama (ReelShort / DramaBox) | 60–120 s per ep | 55–70% | Drama is carried by confrontation; silence reads as a freeze on a phone |
| TikTok / Reels / Shorts narrative | 20–60 s | 30–50% | Retention depends on visual change; long talk loses the thumb |
| Narrative ad / brand film | 30–90 s | 25–45% | Product needs screen time; VO carries the argument |
| Cinematic short | 5–20 min | 35–55% | Room for silence, but not for empty dialogue |
| Animated / motion comic | 1–10 min | 50–70% | Static frames need voice to stay alive |
| Explainer / VO-led | 60–180 s | 80–100% | The words are the product |

If a format's dialogue share is exceeded, the piece will feel like a podcast with pictures.

### 2.3 Shot density by pace profile

| Profile | Sec/shot | Feels like |
|---|---|---|
| Cinematic | 5.0 | Deliberate. Lets a face hold. Punishes weak material. |
| Short-form medium-high | 3.5 | The default for social narrative. Cuts before boredom, not before comprehension. |
| High-density action | 2.5 | Fights, chases, montage, panic. Below 2.0 s it becomes noise. |
| Slow-but-dense | 4.5 | Single takes, long holds, information arriving through what's said |

Do not average profiles across a piece. A 60-second vertical drama might open at 2.5 s/shot for the hook, settle to 3.5, and close at 2.5 again. Budget total shots from the *weighted* average and state it.

---

## 3. Event grains — the derivation

Runtime is not chosen. It is *earned* by how much story occurs.

### 3.1 Definition

An **event grain** is one visible change of state. Count exactly one for each of:

- **(a) Decision with cost.** A character chooses, and the choice takes something from them. "She decides to lie" is a grain. "She feels conflicted" is not.
- **(b) Information reveal.** Something becomes known that changes how the audience reads the scene. A photograph, a name, a date, a door that was supposed to be locked.
- **(c) Relationship shift.** Two characters end the beat in a different configuration than they started: trust → suspicion, stranger → protector, equal → debtor.
- **(d) Irreversible physical change.** A prop breaks, a place burns, a document is signed, a body falls.

### 3.2 What never counts

- Atmosphere and mood, however beautifully rendered
- Internal states with no visible behavior
- Repeated action (the third punch is not a third grain)
- Additional camera angles on the same event
- Exposition that confirms what the audience already knows
- Transitions, establishing shots, montage filler

### 3.3 The formula

```text
T_max = G × 20 seconds
T_min = G × 8 seconds
```

Twenty seconds per grain is the ceiling because each grain needs setup, execution, and a reaction. Below eight seconds per grain the audience cannot register the change at all — it becomes a sequence of events with no consequence.

**Worked example.** Premise: a courier delivers a package, discovers the recipient is the ex who left him three years ago, and has to decide whether to hand it over.

Count: he arrives and the door opens (no grain yet — setup). He recognizes her **(b)**. She recognizes him **(c)**. He has to choose to hand it over **(a)**. That's G = 3 → T_max 60 s, T_min 24 s. So a 60-second vertical episode is right at the ceiling — which is exactly the format this premise belongs to.

Add: she opens the box and it's his own returned letters **(b)**. Now G = 4, T_max 80 s. If the client wants 60 s, they must cut a grain.

### 3.4 When the grain count and the requested runtime disagree

| Situation | Do this |
|---|---|
| G gives 80 s, client wants 60 s | Name the grain to cut. Do not compress delivery. |
| G gives 40 s, client wants 60 s | Add a grain, or extend one beat's reaction time honestly. Do not add description. |
| G gives 200 s, client wants a 30 s ad | The premise is a short film, not an ad. Say so. |

---

## 4. Propagation to downstream modules

The Spec Card numbers are not advisory. Each module spends them differently.

### 4.1 To the shot list

```text
Shots = T ÷ density
```

Each shot must carry a function from a closed list: **hook, establish, action, reaction, reveal, transition, payoff**. A shot with no assignable function gets deleted, not shortened. Shortening a functionless shot to 0.8 s just makes it a flash frame.

### 4.2 To dialogue

Dialogue has a double cost: it occupies screen time *and* it requires a performance that has to land on the first take. When over budget:

1. Cut redundant dialogue first
2. Convert dialogue to action second (show the line instead of saying it)
3. Cut whole beats last, and tell the user which ones

Never solve a dialogue overrun by speeding up delivery. That is how you get a track that sounds like a terms-of-service read.

### 4.3 To image generation

Every shot with characters or hero props becomes image-generation cost. For a Tier S piece, budget **6–10 generated keyframes** for a 15-shot list — not one image per shot. Reuse angles, reuse lighting setups, reuse the same keyframe with different crops.

### 4.4 To sound

Tier S and M pieces usually need **3–5 music cues** maximum. More cues than that in under three minutes reads as a montage of unrelated scenes, even when the picture is continuous.

---

## 5. Platform-specific realities

### 5.1 Vertical drama (ReelShort / DramaBox / GoodShort)

- Episode 60–120 s; season 40–80 episodes
- Hook must be **visible and legible in the first 1–2 seconds** — no logo, no slow fade
- Every episode ends on a cliff or a reversal. A clean resolution kills the next-episode tap.
- Talk-heavy by design: the phone screen is small, faces are large, and confrontation is the product
- Subtitle-safe: dialogue must survive being muted, so the dramatic information belongs in the image too

### 5.2 TikTok / Reels / Shorts

- 20–60 s for narrative; 7–15 s for pure hook tests
- First frame is the thumbnail — design it
- Assume sound-off for the first watch: text on screen must carry the premise
- Loops are free retention; if the last frame cuts back to the first, the view counts twice

### 5.3 Narrative ads

- Product must appear before 40% runtime or the ad gets skipped as a short film
- The product is usually the *solution to the grain*, not a decoration
- 15 s and 30 s cuts need separate Spec Cards — they are not trims of each other

### 5.4 YouTube long-form narrative

- Pacing can breathe; 5.0 s/shot is fine
- The retention problem moves from "hook" to "first 30 seconds" and "mid-roll dips"
- Chapter boundaries are natural scene boundaries; plan them

---

## 6. Budget audit — run this before delivering

```text
[SPEC CHECK]
Runtime:            X s
Script words:       n  / budget      (±10% is fine)
Dialogue words:     n  / budget      (hard ceiling)
Scenes:             n  / budget
Shots:              n  / budget
Shot functions:     all assigned?   (list any orphans)
Props/characters:   n  (any invented mid-script?)
Hook position:      0:0X
Deliverable:        within budget / needs red light
```

If the audit fails, deliver the red light instead of the script. A script that is 40% over budget is not a first draft — it is a different project.

---

## 7. Common budget failures

| Symptom | Real cause | Fix |
|---|---|---|
| Script reads long but story is thin | Description padding | Delete description, not story |
| Shot list balloons past 40 for 60 s | Density set to 2.5 for a dialogue scene | Split the piece into two pace profiles |
| Dialogue track rushes | Dialogue written at script-body rate (2.2) but performed at 3.0+ | Re-budget dialogue at 2.5 wps |
| Every scene has three locations | Scene count never budgeted separately | Add a scene ceiling to the Spec Card |
| Episode 5 has a character nobody introduced | No prop/character ledger | Maintain one in the asset bible from episode 1 |
| Hook lands at 0:07 | Opening treated as story instead of price of admission | Budget 2 s separately, before the story starts |
