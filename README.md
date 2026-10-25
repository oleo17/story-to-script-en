# story-to-script-en — Screenwriting Skill

A skill for AI coding agents that writes screen scripts: vertical short dramas, TikTok/Reels/Shorts narrative, narrative ads, cinematic shorts, animated and motion-comic scripts, AI-video storyboards, and video-model prompts.

Built on one principle: **budget before craft.** Most AI-assisted scripts fail the same way — you ask for 60 seconds and get three minutes. This skill locks runtime, scene, shot, word, and dialogue budgets *before* writing, then spends against them.

**This is not a translation.** Every rate is calibrated against English speech, and every convention is the one the English-language industry actually uses — US screenplay format, 9:16 staging, ReelShort-style conflict rhythm, English prompt dialects for each video model.

Works in **Claude Code, OpenAI Codex, Cursor, Gemini CLI, GitHub Copilot, and WorkBuddy** — standard Agent Skills format, plain Markdown, no scripts, no dependencies.

---

## The calibration that makes it work

Chinese drama budgets in characters per second. English doesn't work that way, and a direct translation produces numbers that make actors race the clock.

| Measure | Value |
|---|---|
| Conversational delivery | 2.5 words/sec (150 wpm) |
| Fast delivery ceiling | 3.0 words/sec (180 wpm) |
| Full script body | 2.2 words/sec |
| Screenplay page | ≈ 1 minute, ~190 words |

Which is why **a 60-second script is about 130 words** with at most **150 spoken words**. If a generator hands you 400 words for a 60-second piece, it has written a three-minute script and mislabeled it.

Runtime itself isn't chosen — it's derived from **event grains**: one visible change of state per grain, `T_max = G × 20s`, `T_min = G × 8s`.

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

### Claude Code

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/.claude/skills/story-to-script-en
```

Invoke explicitly with `/story-to-script-en`, or just describe the task and let the description match.

### Multiple agents at once

`~/.agents/skills/` is read by most tools, so one copy covers Codex, Cursor, Gemini CLI, and Copilot:

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/.agents/skills/story-to-script-en
```

Note: **Claude Code reads only `.claude/skills/`** and Codex reads only `.agents/skills/`. For both, install two copies or symlink.

### Symlink (recommended — one copy, no drift)

```bash
git clone https://github.com/oleo17/story-to-script-en.git ~/skills/story-to-script-en
ln -s ~/skills/story-to-script-en ~/.claude/skills/story-to-script-en
ln -s ~/skills/story-to-script-en ~/.agents/skills/story-to-script-en
```

Restart the session, then either name the skill or describe the task.

---

## Usage

```text
Using story-to-script-en, turn this into a 60-second vertical drama:

A courier delivers a package in a rainstorm on his last run of the night.
The recipient is the ex who left him three years ago, and she doesn't know
he's been paying her rent.
```

What happens: the skill counts event grains (4 → 80-second ceiling), files a Spec Card at Tier S, and asks whether to cut a grain for 60 seconds or run at 80. Then it drafts in vertical short-form format, doctors itself against the budget, and only then builds the shot list and the video prompts.

---

## Structure

```text
story-to-script-en/
├── SKILL.md                          # router, global rules, Step 0 spec lock
├── references/
│   ├── 00-scale-control.md           # English calibration, tiers, budget audits
│   ├── 01-development.md             # logline, grain spine, bible, trope map
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

`SKILL.md` only routes. It tells the agent which reference to read for the current request, so a 60-second script never pulls 400 pages of craft into context.

---

## Related

The Chinese-language edition lives at [story-to-script](https://github.com/oleo17/story-to-script). It is a separate body of work, not a source this was translated from — the craft conventions differ enough that the two share principles but not text.

---

## License

MIT
