# 08 — Post Sound and Music

The last 20% that decides whether the piece feels finished.

Sound does work that picture cannot: it tells the audience how to feel about what they're seeing, and it hides the seams in generated footage. A mediocre cut with good sound reads as intentional. A good cut with bad sound reads as amateur.

---

## 1. The sound layers

Five layers, always in this order of priority. If you can only afford two, afford the first and the third.

| Layer | Content | Priority |
|---|---|---|
| **1. Dialogue** | Voice, ADR, vocal texture | Non-negotiable |
| **2. Ambience** | Room tone, location bed | Non-negotiable — silence reads as broken |
| **3. SFX** | Action sounds, impacts, transitions | High — this is where weight lives |
| **4. Music** | Score, cues, needle drops | Medium — can be sparse |
| **5. Design** | Textures, risers, sub-bass, abstractions | Optional — adds signature |

### 1.1 The most common mistake

**No ambience.** A generated clip with only dialogue and music sounds like a phone call from an empty room. Every location has a bed: a corridor hums, a kitchen has a fridge, a street has distance. Ambience is what makes a place exist.

---

## 2. The BGM curve

Music is not a bed laid under the whole piece. It is a curve with entries, exits, and one moment of restraint.

### 2.1 Curve format

```text
[BG CURVE] Title · runtime X s
0:00–0:03   IN     low sub drone, no melody — under the hook
0:03–0:12   HOLD   drone + single sustained cello note
0:12–0:28   RISE   pulse enters at 92 BPM, strings build
0:28–0:34   DROP   everything out except room tone — the reversal
0:34–0:52   BUILD  pulse returns, one octave up
0:52–1:04   PEAK   full arrangement, no drums yet
1:04–1:18   BREAK  drums out, piano alone
1:18–1:26   END    single note, natural decay, no resolve
```

### 2.2 The rules that matter

1. **Music must not enter on frame 1** unless the piece is a montage or a trailer. A drone under the hook is fine; a melody is not.
2. **The drop at the reversal is worth more than any amount of build.** Cutting music out at the turn is the single most effective sound decision in short-form.
3. **Never resolve the final chord** if the piece ends on a cliff. Resolution tells the audience it's over.
4. **Music competes with dialogue.** If a line must land, cut the music under it or thin the arrangement.
5. **Three cues per 90 seconds is the ceiling.** More than that and it reads as a montage.

---

## 3. Cue sheet

```text
[CUE SHEET]
| # | In     | Out    | Duration | Type      | Mood / function            | Source        |
|---|--------|--------|----------|-----------|----------------------------|---------------|
| 1 | 0:00.0 | 0:11.5 | 11.5 s   | Score     | Dread, held, no release    | AI-generated  |
| 2 | 0:11.5 | 0:28.0 | 16.5 s   | Score     | Pressure building          | AI-generated  |
| 3 | 0:28.0 | 0:33.5 |  5.5 s   | Silence   | Reversal — everything out  | —             |
| 4 | 0:33.5 | 1:18.0 | 44.5 s   | Score     | Return, higher register    | Library       |
| 5 | 1:18.0 | 1:26.0 |  8.0 s   | Sting     | Unresolved final note      | AI-generated  |
```

**Silence gets its own cue.** If it doesn't appear on the sheet, an editor will fill it.

---

## 4. Writing music briefs for AI generation

AI music models respond to genre, instrumentation, tempo, energy, and *reference points* — not to emotion words alone.

### 4.1 Brief structure

```text
Genre:          neo-noir underscore
Instrumentation: muted cello, sub drone, felt piano, no percussion first half
Tempo:          60 BPM feels half-time; pulse enters at 92
Key / mode:     D minor, no resolution
Production:     close-mic'd, roomy, tape saturation, no bright highs
Reference feel: <one composer or track, plus what specifically to borrow>
Duration:       28 s
Must not:       melody in the first 8 s, drums, major cadence, vocals
Ending:         cut on a held note, no fade
```

### 4.2 What to avoid in briefs

| Weak | Why | Better |
|---|---|---|
| "emotional and sad" | No actionable information | "felt piano, single note repeated, D minor, no resolution" |
| "epic trailer music" | Generates a cliché | "low brass swell at 0:20, no drums until 0:24" |
| "like Hans Zimmer" | Model imitates the wrong era | "sustained strings, no melody, sub-bass pulse, 2010s thriller underscore" |
| "build up" | Unmeasurable | "add strings at 0:12, add pulse at 0:20, drop everything at 0:28" |

### 4.3 Library search terms

When using a library instead of generation, search by **texture and function**, not mood.

| Instead of | Search |
|---|---|
| "sad music" | "solo cello, sustained, sparse, 60 BPM, minor" |
| "tension" | "sub drone, pulse, no melody, dark underscore" |
| "happy ending" | "warm piano, resolve, major, mid-tempo" |
| "action" | "percussive, 140 BPM, distorted low end, no melody" |

Then filter by **duration** and **edit points**. A track that needs to end at 0:28 and runs 2:40 is not usable — pick stems or a loopable cue.

---

## 5. SFX

### 5.1 Where weight comes from

Impacts don't sound like impacts. They sound like three things layered:

| Layer | Content | Without it |
|---|---|---|
| **Foley** | The literal sound — knuckle on wood | Feels fake and thin |
| **Impact** | Low-frequency thump, 40–80 Hz | No weight |
| **Tail** | Room response, reverb | No space; sounds like a library sample |

A punch with only foley sounds like a tap. A punch with all three sounds like it hurt.

### 5.2 Sound bridges

Carry a sound across a cut to hide the edit. The most useful ones:

- A door closing that continues over the next scene
- Rain that starts before the cut to exterior
- A music tail that runs under the following dialogue
- A voice from the next scene heard faintly in the current one

Every hard cut in a short piece should either be motivated by a sound bridge or be deliberately abrupt. An unmotivated cut is the tell of a slideshow.

### 5.3 The silence rule

Cut *everything* for half a second at the most important moment. The absence of sound is louder than any impact. Do it once per piece, or it stops working.

---

## 6. Mix targets

Practical levels for social and web delivery:

| Element | Target | Note |
|---|---|---|
| Dialogue | −6 to −3 dBFS peak | Loudest element, always |
| Music bed | −18 to −15 dBFS | Should sit clearly under dialogue |
| SFX | −12 to −6 dBFS, impacts to −3 | Impacts may briefly match dialogue |
| Ambience | −30 to −24 dBFS | Barely audible, but its absence is obvious |
| Master peak | −1 dBFS true peak | Leave headroom |
| Loudness | −14 LUFS integrated | Platform norm for social; −16 for some |

**Phone speaker check.** Play the mix on a phone speaker at 30% volume. If dialogue survives and music doesn't dominate, it will work everywhere. This is the only test that matters for vertical content.

---

## 7. Subtitles and captions

Most first watches are muted. Captions are not accessibility — they are the primary text channel.

| Rule | Reason |
|---|---|
| Burn in for social; use platform auto only if you check it | Auto-captions mangle names and break the read |
| Max 2 lines, max 32 characters per line | Beyond that the eye gives up |
| Position bottom-third, never over faces | Faces carry the drama |
| High contrast: white with a shadow, or a solid bar | Busy backgrounds eat thin type |
| Time to speech, not to the cut | Captions that lag read as broken |
| One caption per speech burst | Word-by-word karaoke only if the platform style demands it |

For vertical drama, the convention is bold, centered, and often with the speaker's name — because the audience is half-watching.

---

## 8. Delivery

```text
[SOUND DELIVERY]
Runtime:        X s
Layers:         dialogue / ambience / SFX / music / design
Cues:           n
Silence points: n   (positions listed)
Bridges:        n   (which cuts)
Mix:            −14 LUFS, −1 dBFS peak, phone-checked
Captions:       burned / sidecar / both
Licensing:      all cues cleared? (list sources and licences)
```

**Licensing is a real risk, not a formality.** AI-generated music has terms that vary by provider and plan; library music has usage tiers. If the piece will be used commercially, note the source and licence per cue.

---

## 9. Handoff

```text
[HANDOFF]
Stage: Sound design complete
Locked so far: BGM curve, cue sheet, mix levels, caption strategy
Main risks: <e.g. cue 4 is library and not cleared for paid ads>
Next step:
- Suggested module: none — delivery. Or back to 02 if the sound reveals a pacing problem.
- Materials needed: final picture lock; any licence confirmations
- Copy-paste invocation: "Build the final mix per cue sheet; verify LUFS and caption timing."
```

---

## 10. The last check

Play the finished piece once, on a phone, muted, at arm's length.

Ask one question: **can I tell what happened?**

If yes, the piece works. If no, the problem is not the sound — it's that the story was told entirely in dialogue and music, and the picture was carrying decoration instead of information.
