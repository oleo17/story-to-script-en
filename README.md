# story-to-script-en

**A screenwriting skill that refuses to let a 60-second script become three minutes.**

[![License: MIT](https://img.shields.io/badge/license-MIT-2ea44f?style=flat-square)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/format-agent%20skills-6e4aff?style=flat-square)](https://agentskills.io)
[![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20·%20Codex%20·%20Cursor%20·%20Gemini%20CLI%20·%20Copilot-1f2328?style=flat-square)](#install)
[![Discussions](https://img.shields.io/badge/discussions-open-0969da?style=flat-square)](https://github.com/oleo17/story-to-script-en/discussions)

Vertical drama, TikTok/Reels narrative, branded shorts, cinematic shorts, animated and motion-comic scripts, AI-video storyboards, and per-model video prompts — for Claude Code, OpenAI Codex, Cursor, Gemini CLI, GitHub Copilot, and WorkBuddy.

Plain Markdown. No scripts, no dependencies, no API keys.

---

## The failure it fixes

Ask an AI for "a 60-second vertical drama" and you get three minutes of material. Scene count doubles, the hook lands at second eight, and nobody notices until the edit.

This skill front-loads a **Spec Card** — a hard budget for runtime, scenes, shots, words, and spoken dialogue — computed before a single line is written. Everything downstream spends against it. Being "more complete" is not a valid reason to exceed it.

Runtime itself isn't chosen from the prompt. It's derived from how much story actually happens:

```text
Event grain G = one visible change of state.
Cost counted: a decision that costs someone, a reveal, a relationship shift, an irreversible change.
Not counted: atmosphere, internal feeling, repeated action, another angle on the same beat.

T_max = G × 20s      T_min = G × 8s
```

Four grains means an 80-second ceiling. That number gets decided before the draft, not discovered in the edit.

---

## Quick start

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/.claude/skills/story-to-script-en
```

Restart the session, then describe the job — "write me a 60-second vertical drama about The long-lost sister turned out to be my ex" — or name the skill directly with `/story-to-script-en`.

Other tools and multi-agent setups: [Install](#install).

---

## Calibrated for English, not translated

Chinese drama budgets in characters per second. English doesn't work that way, and a direct translation produces numbers that make actors race the clock.

| Measure | Value |
|---|---|
| Conversational delivery | 2.5 words/sec (150 wpm) |
| Fast delivery ceiling | 3.0 words/sec (180 wpm) |
| Full script body | 2.2 words/sec |
| Screenplay page | ≈ 1 minute, ~190 words |

Which is why **a 60-second script is about 130 words**, with at most **150 spoken words**. If a generator hands you 400 words for a 60-second piece, it wrote a three-minute script and mislabeled it.

| Tier | Runtime | Grains | Scenes | Shots | Script words |
|---|---|---|---|---|---|
| **S** Micro | 15–120 s | 1–6 | 1–3 | 5–15 | 30–260 |
| **M** Short | 2–8 min | 7–25 | 3–8 | 25–50 | 260–1,050 |
| **L** Mid | 10–30 min | 26–90 | 8–20 | 60–150 | 1,300–3,950 |
| **XL** Long | ≥40 min / series | ≥90 | per ep | per ep | per ep |

---

## What it covers

| Stage | Module | Output |
|---|---|---|
| Genre | `09-genres-tropes` | Trope dossier: promise, engine, cost, specificity, minimum grains, payoff obligations |
| Spec | `00-scale-control` | Spec Card: tier, runtime, grains, scenes, shots, word and dialogue ceilings |
| Development | `01-development` | Logline, grain spine, character cards, pace profile, project bible |
| Drafting | `02-script-drafting` | Script (screenplay or vertical short-form format), hook placement |
| Diagnosis | `03-script-doctor` | Prioritized issue list, budget audit, keep list |
| Dialogue | `04-dialogue` | Subtext fixes, voice fingerprints, line rewrites |
| Assets | `05-assets-continuity` | Character/location/prop bibles, `@img` reference map, continuity ledger |
| Storyboard | `06-storyboard` | Blocked shot list, eleven fields per shot, cross-block state |
| Action | `06b-action-direction` | Clip contracts, spatial grammar, fight and chase shot rhythm |
| Prompts | `07-video-prompts` | Per-model prompts for Veo 3.1, Sora 2, Runway Gen-4.5, Kling, Seedance, MiniMax |
| Sound | `08-post-sound` | BGM curve, cue sheet, library search terms, AI music briefs, mix targets |

`SKILL.md` only routes. A 60-second script never pulls 400 pages of craft into context — it reads the two modules the request actually needs.

---

## Install

Standard [Agent Skills](https://agentskills.io) format: `SKILL.md` with `name` + `description` frontmatter, everything else plain Markdown. The same folder works in every compatible tool without modification.

| Tool | User-level | Project-level |
|---|---|---|
| **Universal** (Codex, Cursor, Gemini CLI, Copilot all read it) | `~/.agents/skills/` | `.agents/skills/` |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| Cursor | `~/.cursor/skills/` | `.cursor/skills/` |
| Gemini CLI | `~/.gemini/skills/` | `.gemini/skills/` |
| GitHub Copilot / VS Code | `~/.copilot/skills/` | `.github/skills/` |
| WorkBuddy | `~/.workbuddy/skills/` | `.workbuddy/skills/` |

### Multiple agents at once

`~/.agents/skills/` is read by most tools, so one copy covers Codex, Cursor, Gemini CLI, and Copilot:

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/.agents/skills/story-to-script-en
```

Claude Code reads only `.claude/skills/`, and Codex reads only `.agents/skills/`. For both, install two copies or symlink.

### Symlink (recommended — one copy, no drift)

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/skills/story-to-script-en
ln -s ~/skills/story-to-script-en ~/.claude/skills/story-to-script-en
ln -s ~/skills/story-to-script-en ~/.agents/skills/story-to-script-en
```

**Model strength matters.** The load-bearing rules here are hard constraints — count grains first, never pad to fill runtime. Strong models hold them; small models with short context tend to skip Step 0 and start writing. If yours does, that's worth reporting.

---

## Usage

```text
Using story-to-script-en, turn this into a 60-second vertical drama:

A courier delivers a package in a rainstorm on his last run of the night.
The recipient is the ex who left him three years ago, and she doesn't know
he's been paying her rent.
```

What happens: it counts four event grains (80-second ceiling), files a Spec Card at Tier S, and asks whether to cut a grain for 60 seconds or run at 80. Then it drafts in vertical short-form format, doctors itself against the budget, and only then builds the shot list and the video prompts.

Ask in any order. Jump straight to "build me the shot list" and it will warn once about the missing asset bible, then do the work.

---

## Structure

```text
story-to-script-en/
├── SKILL.md                          # router, global rules, Step 0 spec lock
├── references/
│   ├── 00-scale-control.md           # English calibration, tiers, budget audits
│   ├── 01-development.md             # logline, grain spine, bible
│   ├── 02-script-drafting.md         # screenplay + vertical short-form formats
│   ├── 03-script-doctor.md           # diagnosis in damage order
│   ├── 04-dialogue.md                # subtext, voice fingerprints, EN pitfalls
│   ├── 05-assets-continuity.md       # bibles, @img map, continuity ledger
│   ├── 06-storyboard.md              # blocks, 11 shot fields, 9:16 staging
│   ├── 06b-action-direction.md       # fight/chase contracts and rhythm
│   ├── 07-video-prompts.md           # per-model prompt dialects
│   ├── 08-post-sound.md              # BGM curve, cue sheet, mix targets
│   └── 09-genres-tropes.md           # 7 trope families, combination rules, payoff audit
└── agents/openai.yaml                # display name and default prompt
```

---

## Design notes

Three choices that will look odd until they save you a draft.

**Refusing the runtime is a feature.** Ask for 45 seconds of revenge and you'll be told that a revenge promise needs six grains, so 45 seconds is the floor and every grain gets 7.5 seconds. That's a compression job, and the skill says so instead of quietly writing a 90-second script.

**Talking about cost instead of theme.** "This story is about forgiveness" is not actionable. "She has to give up the only witness to win" is. Every module asks for the cost in units the audience can see.

**Refusing to choose an upscale on your behalf.** When the budget is blown, the skill stops with a red light and two options: cut a specific thing, or upscale to the next tier with new numbers. It recommends one and waits, because upscaling changes what you're delivering.

---

## Questions, ideas, corrections

- **Questions and craft argument** → [Discussions](https://github.com/oleo17/story-to-script-en/discussions). Ask about a trope, post a script that blew its budget, disagree with a rule. That's what the space is for.
- **Bugs** → [Issues](https://github.com/oleo17/story-to-script-en/issues). Skipping Step 0, blowing the word ceiling, inventing a third character on shot 12 — all bugs. Include the tool, the model, and the exact prompt.
- **Model versions go stale.** The prompt dialects in `07` are current as of late 2026. If a vendor changed its prompt structure, open an issue with a link to their docs.

No support SLA. It's one person's working toolkit, published because it was useful.

---

## Related

**[story-to-script](https://github.com/oleo17/story-to-script)** — the Chinese-language edition. Separate body of work, not a source this was translated from: different speech rates, different formats, different trope pool. The two share principles, not text.

---

## License

MIT — use it, fork it, ship it, sell what you make with it.
