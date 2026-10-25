# 06b — Action and Fight Direction

Action is not fast movement. It is **legible cause and effect at speed**. If the audience can't tell who hit whom and what it cost, the sequence is noise with sound design.

Read this before writing any block containing a fight, chase, fall, or physical confrontation.

---

## 1. The clip contract

Before choreographing anything, write a five-line contract. Every subsequent shot must serve it.

```text
[CLIP CONTRACT]
Who wants what:      Marcus needs the box back; Dana needs him out of the hallway
Who has the advantage at start:  Dana — she's inside, door is a barrier
Who has it at end:   Marcus — he's through the door
Cost of the change:  he's bleeding; the box is dropped and opened
Last image:          both looking at the letters on the floor
```

If the contract can't be filled, the sequence has no arc and will read as random.

---

## 2. Spatial grammar

Confusion in action almost always traces to unmapped space, not to bad choreography.

### 2.1 Draw the box

Before shots, fix the geography in words:

```text
[SPACE]
Room:      corridor, 1.2 m wide, door at frame end
People:    Marcus (corridor side, facing door) / Dana (doorway, facing corridor)
Objects:   box at Marcus's chest → falls at his feet, spills toward Dana
Camera axis: corridor centerline, camera stays on Marcus's side for the whole sequence
```

### 2.2 The 180° rule, and when it's allowed to break

Keep the camera on one side of the action line so screen direction stays consistent. If Marcus is screen-left, he stays screen-left until a neutral shot re-establishes the geometry.

Break it deliberately and only for one reason: **to disorient at the moment the character is disoriented.** Break it accidentally and the audience spends the next four shots working out which direction anyone is facing.

### 2.3 The re-establish rule

Every time geography changes — a new person enters, someone is thrown into another room — insert one establishing shot before continuing. The audience can follow a complex fight if it's re-anchored; it cannot follow a simple fight that isn't.

---

## 3. The five-beat action sequence

Action sequences are not one long escalation. They alternate:

```text
1. WANT      — establish the goal in one clear image
2. OBSTACLE  — the first thing that blocks it
3. ESCALATION — two to four attempts, each more costly
4. REVERSAL  — advantage flips
5. COST      — what the win took
```

The **COST** beat is the one amateurs skip and the one that makes action mean anything. A fight where the winner walks away clean is a dance.

### 3.1 Duration by beat

| Beat | Share of sequence |
|---|---|
| Want | 5% |
| Obstacle | 10% |
| Escalation | 55–60% |
| Reversal | 15% |
| Cost | 10–15% |

---

## 4. Shot rhythm

Fights are cut to a rhythm, and the rhythm is the point.

### 4.1 The impact rule

Fast movement needs a longer shot. A blow that lasts 0.3 s on screen is unreadable. Impact shots should be **1.0–1.5 s**, and the pause after the hit is what sells it.

The instinct to cut faster on impact is wrong: it produces a sequence of flashes.

### 4.2 The pattern

```text
wide (geography) → tight (impact) → wide (consequence)
```

Repeat with variation. The wide shot after an impact is not a breather — it's the audience registering what changed.

### 4.3 Duration guide

| Content | Shot length |
|---|---|
| Establishing the space | 2.5–4.0 s |
| Exchange of blows | 1.0–1.5 s per impact |
| Reaction / recoil | 1.5–2.0 s |
| Movement between positions | 2.0–3.0 s |
| Weapon or object detail | 0.8–1.2 s (insert) |
| Cost / aftermath | 3.0–5.0 s |

At 2.5 s/shot average, a 30-second fight is 12 shots — that is already dense. A 60-second fight at 30 shots needs real choreography, not more cuts.

---

## 5. Writing an action shot

Seven fields, no more. Anything extra is unshootable.

```text
4.2  1.2s  MCU   Marcus takes the door edge on the shoulder.
                 Camera: locked, slightly low. 50mm. Hard side light from the doorway.
                 He spins into the wall; the box falls out of frame.
                 | SFX: body on plaster, box hits floor | SILENT under
                 func: action       @char:mar_01 @prop:prop_box_01
```

### 5.1 Verbs, not adjectives

| Weak | Strong |
|---|---|
| "a violent struggle" | "he gets an elbow between them; she loses the door" |
| "they fight" | "she drives him back two steps and the light goes out" |
| "chaotic action" | "his hand finds the frame; the frame gives" |

The reader must be able to count the actions. If they can't, the shot list can't be executed.

### 5.2 One change per shot

Each shot contains exactly one change of state: who has the advantage, what broke, who entered, where they are. Two changes in one shot and the audience misses one.

---

## 6. Fight choreography by type

### 6.1 Unarmed, close quarters

- Distance is the story: who controls the gap controls the fight
- Two or three distinct techniques is enough — a fight with fifteen moves has no shape
- Hands and faces, not whole bodies. Wide shots of grappling read as a hug from the wrong angle

### 6.2 Weapons

- **The weapon must be visible before it's used.** A knife that appears at the moment of the stab is a cheat
- Range determines everything: knives want contact, bats want a swing's worth of distance, guns want distance and stillness
- The most frightening weapon shot is usually the person deciding, not the strike

### 6.3 Group fights

- **The crowd is an environment, not a cast.** Two named fighters plus an unnamed mass
- Attackers must arrive in a way that lets the hero's attention move visibly
- Never let more than two attackers be in contact at once — the audience loses the hero's body in the pile

### 6.4 Chase

- Geography first: the chase is a map the audience learns by running through it
- Every obstacle must be established before it's used as an obstacle
- Alternating wide (where are we) and tight (how close) is the entire grammar

### 6.5 Falls and impacts

- Show the launch, the fall, and the landing as three shots. Collapsing them into one removes the consequence.
- The landing is short and hard; the aftermath is long and held.

---

## 7. Action in AI video generation

Generating action is harder than generating faces, and the failure mode is specific: **limbs multiply, contact has no weight, and motion smears.**

### 7.1 Prompt strategies

| Problem | Fix |
|---|---|
| Limbs multiply | Specify count and position: "two hands, both on the door frame" |
| Contact has no weight | Add the consequence in the same prompt: "his shoulder compresses into the wall" |
| Motion smears | Lower implied speed: "a single step" not "a lunge" |
| Physics float | Name gravity and mass: "heavy, slow, weight forward" |
| Choreography ignored | Shorten the described action to one beat per clip |

### 7.2 Clip length

Generate **2–4 seconds per clip** for action. Longer clips let the model invent choreography you didn't ask for, and the invented part is where physics breaks.

Assemble the sequence in the edit, not in the prompt. The prompt's job is one legible beat.

### 7.3 The action prompt template

```text
<subject + wardrobe> <single action verb> <reaction / consequence>,
camera: <angle> + <move>, <focal feel>,
light: <source, direction, quality>,
physics: <weight, momentum, contact behavior>,
motion: <speed>, <stable / slight handheld>,
negative: extra limbs, warped hands, floating, speed ramp
```

---

## 8. Common action failures

| Failure | Symptom on screen | Cause |
|---|---|---|
| Weightless | Hits land but bodies don't react | No consequence in the same shot |
| Eastern/Western confusion | Choreography mixes incompatible idioms | No style reference chosen |
| Cliffhanger cheat | Someone appears from nowhere | Space not mapped before shooting |
| Costless win | Hero wins, nothing lost | COST beat missing |
| Cut salad | 0.2 s shots | Panic cutting instead of choreography |
| Repeated geography | Same wide shot every 3 shots | No new spatial information |

---

## 9. Handoff

```text
[HANDOFF]
Stage: Action block directed
Contracts: <clip contract attached per sequence>
Space: <mapped, axis chosen>
Cost: <what the sequence took from whom>
Next step:
- Suggested module: 06-storyboard (backfill shots) then 07-video-prompts
- Materials needed: style reference for the action idiom; clip-length decision
- Copy-paste invocation: "Backfill these contracts into the shot list, keeping one change per shot."
```
