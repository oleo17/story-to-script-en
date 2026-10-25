# 03 — Script Doctor

Diagnosis of an existing script. The job here is not to rewrite — it is to tell the writer, precisely and in priority order, what is wrong and what it costs.

A doctor who rewrites for you has taken your script away. A doctor who tells you scene 4 is doing the work of scene 3 and scene 5 has given you something you can use on the next draft too.

---

## 1. Diagnostic order

Never diagnose top-to-bottom in script order. Diagnose in **damage order** — the order in which a problem destroys everything downstream.

| Priority | Layer | Why first |
|---|---|---|
| 1 | Budget (runtime, words, shots, scenes) | An over-budget script cannot be fixed by editing lines |
| 2 | Grain spine | If the story has no events, no dialogue rewrite saves it |
| 3 | Structure | Wrong shape for the runtime means scenes are in the wrong order |
| 4 | Scene function | Scenes that do nothing cannot be improved, only cut |
| 5 | Character logic | Motivation gaps read as bad acting, but they're writing |
| 6 | Dialogue | The most visible layer and the least important |
| 7 | Line polish | Last, always last |

Writers almost always want to start at 6. Start at 1.

---

## 2. Layer 1 — Budget audit

Run the numbers before reading for quality. An over-length script read for line quality wastes everyone's time.

```text
[DOCTOR: BUDGET]
Runtime actual:      X s   (budget Y)
Script words:        n     (+/- %)
Dialogue words:      n     (+/- %, ceiling)
Scenes:              n     (budget n)
Shots:               n     (budget n)
Speaking characters: n     (cap n)
Locations:           n
Verdict:             within / over by X% / structurally overscaled
```

**Structural overscale** is the diagnosis when the script is 60% over budget. That is not a trim — the writer has written a different format. Say so plainly: "This is a 3-minute short wearing a 90-second spec."

---

## 3. Layer 2 — Grain spine

Extract the grains the script actually contains, in order, as a list. Then compare against what the story needs.

```text
[DOCTOR: GRAINS]
1. 0:03  reveal   — she opens the door, he recognizes her
2. 0:14  shift    — she pretends not to know him
3. 0:31  ???      — long dialogue, no state change (0:31–0:52)
4. 1:02  decision — he decides to keep the package
5. 1:18  reveal   — she already knows what's inside
```

Three diagnoses come out of this list:

- **Drought** — a gap of 20+ seconds with no grain. The audience feels this as "slow," even when there's dialogue. The fix is a grain, not a trim.
- **Cluster** — three grains in eight seconds. The audience can't register them. Space them or cut one.
- **Missing terminal grain** — the last grain resolves, but the *question* raised by the hook is never answered. The script ends and the audience feels cheated without knowing why.

**Grain is not the same as a beat.** A beat is a moment; a grain is a change. A script can have forty beats and two grains and feel completely inert.

---

## 4. Layer 3 — Structure

### 4.1 Shape check

| Check | Failure symptom | Note |
|---|---|---|
| Hook within first 2 s (social formats) | Opening is setup or establishing | The single most expensive failure |
| Turn exists and is placed | Piece has no reversal — it's a situation | Situation ≠ story |
| Turn lands in the last third | Turn at 0:15 of a 90 s piece → 75 s of aftermath | Aftermath is not story |
| Ending type is chosen | Ends because the words ran out | Resolve / loop / cliff must be a decision |
| Scene count matches structure | Three-act shape in a 60 s piece | Produces a synopsis, not a scene |

### 4.2 Where the story actually starts

Mark the first line that cannot be cut. Everything before it is pre-roll. In short-form, pre-roll is the enemy — it is usually 10–25% of the runtime doing no work.

---

## 5. Layer 4 — Scene function

For each scene, force a one-word function from a closed list:

```text
hook / establish / escalate / reveal / react / decide / transition / payoff
```

Then:

- **Two adjacent scenes with the same function** → one of them is redundant. Usually the second.
- **Any scene labelled "establish" after the first 15 seconds** → cut or merge.
- **Any scene labelled "transition"** → check whether the transition is doing emotional work. Usually a cut does it faster.
- **Any scene with no label** → cut it and see if the script breaks. It usually doesn't.

### 5.1 The deletion test

Remove the scene entirely in your head. Read what's left.

- Story still works → the scene was decoration. Cut.
- Story breaks in a way you can name → the scene has a function. Keep, and label it.
- Story breaks in a way you *can't* name → the scene carries theme or mood. Keep only if the piece is long enough to afford mood.

---

## 6. Layer 5 — Character logic

The audience experiences character problems as performance problems. Six of them, in order of how often they occur:

| Problem | Symptom | Fix |
|---|---|---|
| **Passive lead** | Things happen *to* them for the first half | Give them a decision in the first 15 s |
| **No cost** | Their choices are free | Attach a loss to the choice the story turns on |
| **Idiot ball** | They fail to notice something obvious so the plot can proceed | Change the obstacle, not their intelligence |
| **Unexplained knowledge** | They know something the audience never saw them learn | Add the source, or cut the knowledge |
| **Uniform voice** | Everyone talks like the writer | See `04-dialogue.md` — voice fingerprints |
| **Motivation stated** | A character announces why they're doing it | Convert to action; if it can't be converted, the motivation is thin |

### 6.1 The "why now" test

For the inciting action, ask: *why does this happen today and not last week?* If the answer is "because the script starts today," there is no pressure. A ticking element — a deadline, a departing flight, a closing window — is the cheapest and most reliable fix.

---

## 7. Layer 6 — Dialogue

Do not line-edit here. Diagnose, and route detailed work to `04-dialogue.md`.

Scan for these five patterns:

1. **On-the-nose** — a character states their feeling or intention directly. `"I'm angry because you lied."`
2. **Exposition delivery** — two people telling each other things both already know, for the audience's benefit. `"As you know, our father left the company to you."`
3. **Repeated information** — the same fact delivered twice because the writer didn't trust it the first time.
4. **Interchangeable voices** — cover the character names; if you can't tell who's speaking, the lines are the writer's, not the characters'.
5. **Dead-end lines** — lines that answer a question and close the scene, leaving nothing open.

Give one concrete rewrite per pattern found, not a full rewrite. The goal is to teach the diagnosis, then hand back the pen.

---

## 8. Issue report format

Deliver in this shape. Severity first, because a writer with an hour can only fix three things.

```text
[SCRIPT DOCTOR REPORT]
Script: <title>   Tier: <X>   Runtime: X s / budget Y s
Verdict: <one sentence, honest>

CRITICAL (must fix before production)
  1. <issue> — where: <scene/page> — cost if unfixed: <specific>
     Fix: <action, concrete>
  2. ...

MAJOR (fix in next draft)
  ...

MINOR (polish)
  ...

KEEP (do not touch — these are working)
  1. <element> — <why it works>
  ...

BUDGET DELTA AFTER SUGGESTED FIXES
  runtime: X → Y s   words: n → n   scenes: n → n
```

**Always include a KEEP section.** A report that is 100% negative is unusable: the writer doesn't know what to protect while cutting, and cuts the thing that was working.

---

## 9. Severity definitions

| Level | Test | Examples |
|---|---|---|
| **CRITICAL** | The piece cannot be produced or understood as-is | Over budget by >30%, no turn, hook missing, contradictory plot fact |
| **MAJOR** | The piece works but fails its promise | Passive lead, grain drought, resolution without payoff, interchangeable voices |
| **MINOR** | Craft | Adverb-heavy action lines, repeated slugline wording, weak final image |

Resist inflating MINOR to MAJOR. If everything is critical, nothing is.

---

## 10. When the answer is "rewrite, don't repair"

Say this plainly when it's true. Repair is the wrong tool when:

- The logline has no obstacle (it's a premise, not a story)
- The grain count implies a runtime more than double the spec
- The format is wrong (a short film submitted as a 30-second ad)
- The lead has no decision anywhere in the script

In those cases, deliver the diagnosis **plus** a one-paragraph alternative approach. Not a full rewrite — just enough that the writer can see the door.

---

## 11. Handoff

```text
[HANDOFF]
Stage: Diagnosis complete
Pace profile: (unchanged, or corrected)
Locked so far: issue list, severity ranking, keep list
Main risks: <e.g. fixing the grain drought adds runtime and re-breaks the budget>
Next step:
- Suggested module: 02-script-drafting (revision) or 04-dialogue (if only dialogue)
- Materials needed: writer's decision on CRITICAL #1 and #2
- Copy-paste invocation: "Revise per doctor report; fix CRITICAL only, keep the KEEP list intact."
```
