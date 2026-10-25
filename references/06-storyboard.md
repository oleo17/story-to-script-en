# 06 — Shot List and Storyboard

Turning a locked script into something a camera — or a video model — can execute.

The unit here is the **shot**, and every shot must answer five questions before it's written down: what do we see, from where, how does it move, what do we hear, and why does it exist.

---

## 1. Block structure

Never write a flat list of 40 shots. Group into **blocks** of 4–8 shots that share a location, a lighting setup, and an emotional register.

```text
[BLOCK 2] 0:08–0:24  · INT. HALLWAY · night · 3.5 s/shot
```

Why blocks matter:

- Generated images and prompts can be batched within a block
- Continuity state only has to be tracked at block boundaries
- A block is the smallest unit a model can regenerate without breaking the whole piece
- Human crews schedule by setup, which is what a block is

---

## 2. The eleven fields

Every shot carries these. Missing fields become improvisation on set — or hallucination in the model.

| # | Field | Content |
|---|---|---|
| 1 | **ID** | `2.3` — block.shot |
| 2 | **Duration** | seconds |
| 3 | **Shot size** | EWS / WS / MWS / MS / MCU / CU / ECU / OTS / POV / insert |
| 4 | **Subject** | who or what is in frame, in one phrase |
| 5 | **Action** | what changes within the shot — one verb |
| 6 | **Camera** | angle + movement, one of each |
| 7 | **Lens / DOF** | focal equivalent and depth behavior |
| 8 | **Light** | source, direction, quality |
| 9 | **Audio** | dialogue line, SFX, or silence |
| 10 | **Function** | hook / establish / action / reaction / reveal / transition / payoff |
| 11 | **Assets** | `@char` `@loc` `@prop` `@img` handles |

### 2.1 Shot list format

```text
[BLOCK 2] 0:08–0:24 · INT. HALLWAY · night · 3.5 s/shot

2.1  2.0s  CU      Chain slides. Locked off. 50mm, shallow. Practical only. | SFX: chain
              func: reveal      @loc:loc_hall_a @img-06

2.2  3.0s  MCU     Dana in a 4-inch gap. Slow push 10%. 85mm, very shallow.
              Key: spill from ceiling fluorescent, left. | no line
              func: reaction    @char:dan_01 @img-01

2.3  3.5s  OTS     Marcus, box at chest, rain in hair. Locked.
              35mm. Practical behind him, rim on shoulders.
              | MARCUS: "It's addressed to you."
              func: action      @char:mar_01 @prop:prop_box_01 @img-02 @img-09

2.4  2.0s  ECU     The label. Her name. His handwriting beneath.
              Macro, no movement. Hard side light to catch the ink relief.
              | SFX: rain, muffled
              func: reveal      @prop:prop_box_01 @img-09
```

---

## 3. Shot size — what each one is for

Shot size is not decoration. Each size does one job well and others badly.

| Size | Frame | Best at | Worst at |
|---|---|---|---|
| **EWS** | Figure tiny in environment | Isolation, scale, dread | Emotion — face is unreadable |
| **WS** | Full body + surroundings | Geography, blocking, entrances | Intimacy |
| **MWS** | Knees up | Two people in conversation | Detail |
| **MS** | Waist up | Standard dialogue, gesture | Subtle reaction |
| **MCU** | Chest up | Emotion with context | Anything requiring hands |
| **CU** | Head and shoulders | Reaction, decision | Action, geography |
| **ECU** | Eye, mouth, or object detail | The grain of a reveal | Anything in motion |
| **OTS** | Over a shoulder | Power relation between two people | Solo moments |
| **POV** | Through the character's eyes | Subjectivity, threat | Establishing who's where |
| **Insert** | A thing, tightly | Information, exposition | Emotion |

### 3.1 The vertical-frame problem

9:16 changes everything. The frame is 1.78× taller than it is wide.

- **Two-shots are nearly impossible.** Either crop both people badly or stagger them in depth.
- **MS becomes MCU.** What was a medium in 16:9 is a close-up in 9:16.
- **Horizontal action reads as noise.** Crowds, car chases, and wide landscapes lose meaning.
- **Vertical staging works best:** face, then face + hands, then object in foreground.

**Practical rule for 9:16:** count MCU and CU as your default, treat WS as a deliberate opening or closing choice, and never plan a two-shot in profile.

---

## 4. Camera movement

Movement must have a reason. "Dynamic" is not a reason.

| Move | Does | When to use |
|---|---|---|
| **Locked** | Nothing — lets performance carry | Default for dialogue and reveals |
| **Push in** | Increasing pressure, narrowing world | A decision forming; a lie landing |
| **Pull out** | Revealing context, abandoning the subject | Endings; isolation |
| **Pan** | Connecting two things in one space | Revealing who else is present |
| **Tilt** | Scale, or revealing height | Entrances, threat, corpses |
| **Handheld** | Instability, immediacy | Chase, panic — almost never in dialogue |
| **Whip pan** | Collision, comedy, violence | Transitions that hit |
| **Crane / drone** | Establishing scale | Openers and closers, or the vertical-drop reveal |

### 4.1 Movement rules

1. **One move per shot.** Push *and* pan is two shots badly fused.
2. **Movement ends where the frame should rest.** A push that keeps going past the subject looks like an error.
3. **Never move during a line that must be heard.** Movement competes with dialogue for attention.
4. **Three moving shots in a row and the audience stops noticing movement.** Use them sparingly enough to mean something.

---

## 5. Light

Three fields, always: **source, direction, quality.**

```text
BAD   — "moody lighting"
GOOD  — "single ceiling fluorescent, top-left, flickering, green cast"
```

| Quality | Feel | Typical source |
|---|---|---|
| Hard | Interrogation, threat, style | Bare bulb, direct sun, phone flashlight |
| Soft | Intimacy, safety, memory | Window bounce, diffused practicals |
| Motivated | Realism | Whatever the room actually contains |
| Unmotivated | Stylization | Glowing fog, unexplained backlight — use once |

**Rule for AI generation:** name the light source in the prompt every time. Video models default to flat, even, source-less lighting unless told otherwise, and flat light is the fastest way to make generated footage look generated.

---

## 6. Audio per shot

Even in a silent piece, note the audio state. Silence is a decision.

| Type | Notation |
|---|---|
| Dialogue | `| NAME: "line"` |
| SFX | `| SFX: chain, rain (muffled)` |
| Ambience | `| AMB: corridor hum, distant TV` |
| Music | `| MUS: cue in — cold piano` |
| Silence | `| SILENT` (explicit, not omitted) |

If the shot is meant to be silent, write `SILENT`. An empty audio field reads as "not decided yet," and by block 4 it becomes an inconsistency.

---

## 7. Coverage strategy

How many angles per beat you need depends on what the beat does.

| Beat type | Coverage | Why |
|---|---|---|
| Dialogue exchange | Master + 2 singles + 1 insert | Editing flexibility, and AI generation needs alternates |
| Decision | 1 MCU + 1 CU on hands or eyes | The decision is internal; don't cut away |
| Reveal | 1 WS for context + 1 ECU on the thing | Context then detail, in that order |
| Action | 1 wide + 2–3 tight | Wide for geography, tight for impact |
| Transition | 1, and only if it earns its place | Most transitions are a cut with extra steps |

**For AI-generated work, coverage is cheaper than for live action** — but it is not free. Every alternate is another generation and another continuity risk. Budget alternates only where the edit genuinely needs them.

---

## 8. Cross-block handoff

The most common failure in shot-list production is drift at block boundaries. Written state fixes it.

```text
[BLOCK 3] 0:24–0:40 · INT. HALLWAY → INT. APARTMENT · continuous · 3.0 s/shot

IN FROM BLOCK 2:
  Dana: coat dry, hair tied, no injury
  Marcus: soaked, holding closed box
  Door: 3B open, Dana standing in gap
  Light: fluorescent flicker, unchanged
OUT TO BLOCK 4:
  Dana: coat off, on the couch; right hand bleeding
  Marcus: still soaked, box now on the table, unopened
  Location: apartment, one lamp, blinds half down
  Light: tungsten, warm, low
PROP STATE: box unopened; letter still inside
```

---

## 9. Shot count audit

```text
[SHOT AUDIT]
Runtime:            X s
Shots:              n   (budget n)
Weighted density:   X.X s/shot
Functions assigned: n / n   (list orphans)
Blocks:             n
Assets mapped:      n / n shots
Silent shots:       n
Moving shots:       n   (% of total — over 40% is usually a mistake)
Alternates budgeted: n
```

**Orphans** — shots with no function — get cut, not fixed. If you can't name what a shot does in one word, it does nothing.

---

## 10. Handoff

```text
[HANDOFF]
Stage: Shot list complete
Pace profile: (as locked, with per-block density)
Locked so far: blocks, per-shot fields, continuity state at each boundary
Main risks: <e.g. three costume states in 16 seconds; the door detail is unshootable at 9:16>
Next step:
- Suggested module: 07-video-prompts (or 06b-action-direction first, if the piece has fights/chases)
- Materials needed: model choice, aspect ratio confirmation, image budget
- Copy-paste invocation: "Convert Block N of the shot list into <model> prompts, keeping @img handles and continuity state."
```
