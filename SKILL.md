---
name: story-to-script-en
description: Use this skill when writing any kind of screen script — vertical short dramas (ReelShort/DramaBox style), TikTok/Reels/Shorts content, narrative ads, animated shorts, motion-comic scripts, AI-video storyboards, or dialogue polish. It locks a shot/word/duration budget before writing, then carries the project from genre and trope selection through concept and outline to finished script, script doctoring, dialogue pass, asset and continuity bible, shot list, video-model prompts (Veo, Sora, Runway, Kling, Seedance, MiniMax), and post-production sound design. Every density rule is calibrated against English speech rates, not translated from another language. Use it when the user says write me a short film, fix my script, my dialogue sounds flat, build me a shot list, write video prompts, design the sound for this cut, or asks which genre or trope to write in for a platform.
---

# story-to-script — English Edition

A router, not a monolith. Read only the module the current request needs. Do not load every reference file up front; the whole point of this structure is that a 60-second script never drags 400 pages of craft into context.

Default output language is English. Switch only when the user explicitly asks for another language.

## The one rule that governs everything else

**Budget before craft.**

Almost every failed AI-assisted script fails the same way: the writer asks for "a 60-second vertical drama," the model delivers three minutes of material, and nobody notices until the edit. Scene count doubles, shot count triples, the hook lands at second 8 instead of second 2, and the whole thing has to be rebuilt.

So this skill front-loads a **Spec Card** — a hard budget for runtime, scenes, shots, words, and dialogue — computed *before* a single line is written. Everything downstream spends against that budget. Being "more complete" is not a valid reason to exceed it.

If the user's request and the budget conflict, surface the conflict and make them choose: cut scope, or file an upscale request (see §0.5). Never silently expand.

## Step 0 — Spec lock (mandatory, except for single-point fixes)

Read `references/00-scale-control.md` and produce a Spec Card before writing.

Skip only when: the user already supplied a full explicit spec that doesn't contradict the budget ceiling, **or** the task is genuinely single-point (rewrite one line, diagnose one scene, fix one shot).

### 0.1 Count event grains first, then set runtime

Runtime is derived from how much story actually happens, not from what the user typed in the prompt.

```text
Event grain G = one visible change of state. Count 1 for each of the following that fires:
  (a) someone makes a decision and it costs them something
  (b) information is revealed that changes what the audience understands
  (c) the relationship between two characters shifts
  (d) an object or environment changes irreversibly

Do NOT count: atmosphere, internal feeling, repeated action, extra camera angles on the same event, exposition.

T_max (seconds) = G × 20, floor 15s
T_min (seconds) = G × 8
```

A "man walks in, sits down, looks sad" beat is not an event grain. A "man walks in and signs away the house" is one. If you can't name the cost, there is no grain.

### 0.2 The four tiers

| Tier | Runtime | G | Scenes | Shots | Script words | Dialogue words | Decision rounds |
|---|---|---|---|---|---|---|---|
| **S** Micro | 15–120 s | 1–6 | 1–3 | 5–15 | 30–260 | ≤ T × 2.5 | ≤ 1 |
| **M** Short | 2–8 min | 7–25 | 3–8 | 25–50 | 260–1,050 | ≤ T × 2.5 | ≤ 2 |
| **L** Mid | 10–30 min | 26–90 | 8–20 | 60–150 | 1,300–3,950 | ≤ T × 2.5 | ≤ 3 |
| **XL** Long | ≥ 40 min or ≥ 6 eps | ≥ 90 | per episode | per episode | per-episode budget | per episode | ≤ 1 per episode |

**Script words ≈ T × 2.2.** This is the calibrated English figure — action lines plus dialogue, at a normal shooting pace. It is *not* the Chinese figure; see the calibration section below.

**Shot count = T ÷ density.** Density is seconds per shot:

| Pace profile | Sec/shot | Use when |
|---|---|---|
| Cinematic / contemplative | 5.0 | Drama, character pieces, anything that lets a shot breathe |
| Short-form medium-high | 3.5 | Default for vertical drama and social narrative |
| High-density action / hard hooks | 2.5 | Fights, chases, retention-critical openings |
| Slow but information-dense | 4.5 | Talking-head reveals, slow-burn tension |

**Dialogue words ≤ T × 2.5.** Above that the actor is racing the clock and the track will be unusable.

### 0.3 Spec Card format

Every project's first block of output is this card, filled in:

```text
[SPEC CARD]
Project:
Tier:              S / M / L / XL
Source material:   <what I was given, how much>
Runtime:           Xs  (T_min … T_max)
Event grains G:    n   (listed: a/b/c/d per beat)
Scenes:            n   (max 1 location for Tier S)
Shots:             n   (at density x.x s/shot)
Script words:      n   (ceiling)
Dialogue words:    n   (ceiling)
Pace profile:
Platform / format:
Decision rounds:   n
Red flags:         <anything already over budget>
```

### 0.4 Hard rules that do not bend

1. **No word-count padding.** If the story needs 45 seconds and the user wants 60, the extra 15 seconds are a *new event grain*, not slower delivery. Add a beat or change the runtime.
2. **One location change per 20 seconds of Tier S runtime.** Vertical drama shot on a phone cannot afford travel.
3. **Every shot earns its seconds.** A shot with no information, emotion, or transition function gets cut, not slowed down.
4. **Props and people are counted.** Track how many named characters and hero props exist. Shot 12 cannot invent a third character because the composition looked empty.
5. **The hook is budgeted.** For vertical or social formats, the first 2 seconds are not part of the story — they are the price of admission. Budget them separately.
6. **Dialogue is the most expensive content per second.** When over budget, cut dialogue before cutting action. Action shots cost runtime; dialogue costs runtime *and* performance risk.

### 0.5 Red lights and upscale requests

When the budget is blown, do not quietly continue. Stop and emit:

```text
[RED LIGHT] <dimension>: current X / budget Y
Cause: <what pushed it over>
Options:
  A. Cut <specific thing> — returns to budget, costs <what the audience loses>
  B. Upscale to Tier <next> — new budget <numbers>, costs <extra scenes/shots/time>
Recommend: <one, with reason>
```

The model may not choose B on the user's behalf. Upscale is the user's call because it changes the deliverable.

## Module routing

Read the row that matches the request. Do not read adjacent modules "for context."

| The user wants | Read | Output | Default next |
|---|---|---|---|
| Choose a genre or trope, or position a concept against the market | `references/09-genres-tropes.md` | Trope dossier: promise, engine, cost, specificity, min grains, payoff obligations | `01` → grain spine |
| Develop a concept, premise, character relationship, one-line idea | `references/01-development.md` | Logline, premise, beat outline, project bible, platform pace profile | `02` → draft |
| Write or extend the full script, a scene, an episode | `references/02-script-drafting.md` | Draft script, pacing execution log | Script doctor pass |
| Diagnose an existing outline, scene, or script | `references/03-script-doctor.md` | Issue list, priority ranking, structural health check | Back to drafting |
| Fix dialogue only — voice, subtext, punch, naturalness | `references/04-dialogue.md` | Line-by-line notes, rewrites, character voice fingerprints | Backfill, or asset bible |
| Build character / location / prop / wardrobe / style bibles and reference images | `references/05-assets-continuity.md` | Asset master list, `@img-N` mapping, continuity ledger | Storyboard |
| Convert a locked script into an AI-video shot list | `references/06-storyboard.md` | Shot blocks, per-shot fields, cross-block handoffs | Video prompts |
| Direct action, fights, chases, complex transitions | `references/06b-action-direction.md` then `06` | Clip contract, cause-and-effect chain, spatial route, camera duties | Back to shot list |
| Write prompts for Veo / Sora / Runway / Kling / Seedance / MiniMax | `references/07-video-prompts.md` | Per-model prompt pack, parameters, keep/discard lists | Test generation, drift check |
| Design music and sound for the finished cut | `references/08-post-sound.md` | BGM curve, cue sheet, search terms, AI music prompts, SFX plan | Mix and license check |

### Recommended flow

```text
09 tropes → 00 spec lock → 01 development → 02 draft → 03 doctor → 04 dialogue
      → 05 assets → 06 storyboard → 07 prompts → 08 sound
```

Jump in wherever the user actually is. But when they jump ahead, name the gap: someone asking for Veo prompts without an asset bible will get visually inconsistent output, and that is worth one sentence of warning before you comply.

## Stage handoff

Every module ends with a six-part handoff so the next module doesn't have to re-derive anything:

```text
[HANDOFF]
Stage:
Pace profile:
Locked so far:
Main risks:
Next step:
- Suggested module:
- Materials needed:
- Copy-paste invocation:
```

Modules 05 / 06 / 07 / 08 additionally report asset mapping, image budget, end-of-block state, or sound-stage status.

## Project state

Long projects span sessions. Keep a compact project block and carry it forward verbatim: title, tier, runtime, G count, locked scenes, character list, prop list, pace profile, current stage, open decisions. Do not re-litigate locked decisions without being asked.

## Word budgets are calibrated for English

Do not reuse another language's characters-per-second figures. The working numbers:

| Measure | Value | Note |
|---|---|---|
| Conversational delivery | 2.5 words/sec (150 wpm) | Normal dramatic pace |
| Fast delivery ceiling | 3.0 words/sec (180 wpm) | Urgent, no air, hard to sustain |
| Full script body | 2.2 words/sec | Blends dialogue with action description |
| Screenplay page | ≈ 1 minute | US Letter, Courier 12pt, ~190 words/page |

These are why a 60-second script is roughly **130 words of script** with at most **150 words of spoken dialogue**. If a generator gives you 400 words for a 60-second piece, it has written a 3-minute script and mislabeled it.

Full derivation, per-format tables, and the exceptions are in `references/00-scale-control.md`.

## How to behave

- **Be concrete.** "Make the opening stronger" is noise. "The hook lands at 0:06; move the reveal of the envelope to 0:01 and cut the establishing shot" is a note.
- **Ask once, then decide.** Missing a detail that doesn't block progress: assume, mark the assumption, move on. Missing something that would wreck the downstream: ask one focused question.
- **Name trade-offs, don't hide them.** Every cut costs something. Say what.
- **Don't perform enthusiasm.** No "great premise!" Just the work.

## Maintenance

Version and change log belong in this file, at the bottom, newest first. Reference files carry no version headers of their own — this file is the single source of truth for what changed when.

### Change log

**v1.1** — Added `references/09-genres-tropes.md`. Seven trope families (~45 tropes) with promise / engine / cost / specificity / collapse fields; eight worked tropes with 3-second hooks, grain spines, and episode-2 problems; trope combination rules with an engine-conflict test; platform mapping by episode and series length; trope-to-budget conversion (minimum grains per family); per-genre payoff obligations; English-market calibration (untranslatable terms, class through objects, consent boundary, native werewolf vocabulary); and late-2026 market positioning. Routing table and flow updated to put trope selection ahead of development.

**v1.0** — Initial English edition. Native rewrite, not a translation: speech rates calibrated for English (2.5 wps conversational, 2.2 wps script body), US screenplay format alongside vertical short-form format.
