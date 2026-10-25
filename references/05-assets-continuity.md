# 05 — Asset and Continuity Bible

A visual reference system. Its purpose is simple: shot 40 must look like it belongs to shot 1, even if shot 40 was generated a week later by a different prompt.

Every asset entry has to earn its slot by being **referenced by a shot**. An asset nothing uses is documentation, not production material.

---

## 1. Why this module exists

AI video generation drifts. The same character prompt produces a different face on the second run. A coat changes color between scenes. A room's window moves.

Two mechanisms control drift:

1. **A locked reference image per entity** — the generator sees the same face and the same room every time
2. **An explicit continuity ledger** — state carried forward between blocks, written down rather than remembered

Without both, a 40-shot piece becomes 40 unrelated films.

---

## 2. Asset taxonomy

| Type | Code | What's locked | Image needed |
|---|---|---|---|
| Character | `@char` | Face, hair, build, wardrobe per scene | Yes — 1 hero ref + 1 alt angle |
| Location | `@loc` | Architecture, light sources, palette | Yes — 1 wide + 1 detail |
| Hero prop | `@prop` | Shape, material, wear, markings | Yes — 1 single-object ref |
| Wardrobe | `@ward` | Only if it changes within the story | Yes, if it changes |
| Style | `@style` | Film stock, grade, grain, lens character | Yes — 1 style frame |
| Motion | `@motion` | Camera behavior per block | No — text only |

### 2.1 What is a "hero" prop

A prop is hero if **a grain depends on it**: the letter that reveals the truth, the ring that proves the marriage, the phone that shows the message. Hero props get locked images and appear in the continuity ledger.

A prop that's just set dressing — a coffee cup, a chair — needs no entry. Trying to lock every object kills the schedule.

---

## 3. Image budget

Do not generate one image per shot. That's how a 15-shot piece costs 15 generations and still drifts.

| Tier | Runtime | Keyframe budget | Rule |
|---|---|---|---|
| S | 15–120 s | 6–10 | 1 per character, 1 per location, 1 per hero prop, 1 style frame |
| M | 2–8 min | 12–20 | Add alt angles for the lead and the main location |
| L | 10–30 min | 25–40 | Add per-scene wardrobe and state variants |
| XL | series | Lock a season bible | Per-episode reuse; only new entities get new images |

**Reuse is the technique.** One character keyframe, cropped differently, covers a wide, a medium, and a close. The generator only needs a new image when the entity's *state* changes — wet, wounded, dressed differently.

---

## 4. Entry formats

### 4.1 Character

```text
@char: DANA / dan_01
Age / build:      32, slim, 5'7"
Face:             narrow, high cheekbones, dark circles, no makeup
Hair:             dark, shoulder-length, pushed back behind left ear
Wardrobe:         grey wool coat over black turtleneck (SC 1-4);
                  same coat, soaked (SC 5-9)
Distinguishing:   small scar on right eyebrow
Ref images:       @img-01 (front, neutral), @img-02 (3/4, night light)
Do not change:    eyebrow scar, hair length, coat color
```

### 4.2 Location

```text
@loc: HALLWAY / loc_hall_a
Architecture:     narrow pre-war corridor, 4 doors, one at frame end
Light:            single ceiling fluorescent, flickering; no daylight
Palette:          green-grey walls, brown carpet, black doorframes
Key detail:       number 3B is missing its final character
Ref images:       @img-05 (wide, eye level), @img-06 (door detail)
Do not change:    door count, flicker, missing character on 3B
```

### 4.3 Hero prop

```text
@prop: PACKAGE / prop_box_01
Material:         brown corrugated cardboard, water-stained corner
Size:             shoebox, 30 × 20 × 12 cm
Markings:         handwritten label, blue ink, her name; sender field blank
State changes:    dry (SC 1-3) → soaked (SC 4-6) → opened (SC 7+)
Ref images:       @img-09 (closed), @img-10 (open, contents visible)
```

### 4.4 Style

```text
@style: SERIES_LOOK / style_a
Format:           9:16 vertical
Lens:             35mm equivalent, shallow depth, slight edge falloff
Grade:            desaturated cool shadows, warm practicals only
Grain:            fine, 35mm-like
Movement:         locked, or slow push; no handheld in dialogue
Reference:        <one film or photographer, plus what specifically to borrow>
```

---

## 5. The `@img-N` mapping

Every shot in the shot list references images by handle, not by re-description.

```text
SHOT 1.3  OTS Marcus, box in frame
          @char:dan_01 @char:mar_01 @prop:prop_box_01 @loc:loc_hall_a
          images: @img-01 @img-02 @img-05 @img-09
```

The prompt for this shot is then assembled from the handles plus the shot-specific delta. This is the entire mechanism that keeps a cast looking like a cast.

**Rule:** if a shot references a character and no `@img` handle, the shot will drift. Flag it rather than generating.

---

## 6. Continuity ledger

State carried between blocks. Written down, not remembered.

```text
[CONTINUITY @ 0:48 / end of Block 2]
Dana:      coat soaked, hair down, right hand bleeding (cut at 0:41)
Marcus:    dry, box now empty — box left in hallway at 0:44
Location:  hallway door 3B now open; corridor light still flickering
Props:     box open and discarded; letter removed and in Dana's coat pocket
Time:      continuous night, no time jump
Open:      who closed the door at 0:39 — not yet addressed
```

Six fields, always in this order. Any shot in the next block that contradicts a field is a continuity error, regardless of how good it looks.

### 6.1 Most common continuity breaks

| Break | Cause |
|---|---|
| Wetness resets | Each generation starts from a dry reference |
| Handedness flips | Left/right not specified per shot |
| Prop vanishes | Prop not in the shot's `@prop` list |
| Wardrobe changes | Wardrobe locked per scene but not per state |
| Light direction changes | Location ref shot at a different time of day |
| Injury heals | State change not carried into the next block |

---

## 7. Asset master list

The single table everything else reads from. Deliver at the end of this module.

```text
[ASSET MASTER]
Characters:  n   (@char handles)
Locations:   n
Hero props:  n
Wardrobe states: n
Style:       1

IMAGES GENERATED: n / budget n
  @img-01 … @img-NN  (handle → entity → purpose)

UNMAPPED SHOTS: n  (shots referencing an entity with no handle)
RISK: <highest-drift entity, and why>
```

**UNMAPPED SHOTS should be zero before moving to the shot list.** A non-zero count is a prediction of visual failure.

---

## 8. Text-only productions

If there will be no image generation — a radio drama, a VO-led explainer, a prose-format story — this module still applies, minus the images.

Keep: character voice cards (from `04`), prop logic, continuity of fact (who knows what, who has what), and the time ledger. Those are continuity of *story*, which drifts just as badly as continuity of image.

---

## 9. Handoff

```text
[HANDOFF]
Stage: Asset bible complete
Locked so far: character/location/prop refs, style frame, `@img` map, continuity ledger
Main risks: <e.g. Dana's coat changes state three times in 90 s — expensive>
Next step:
- Suggested module: 06-storyboard
- Materials needed: image budget approval, style reference confirmation
- Copy-paste invocation: "Build the shot list from the locked script; map every shot to @char/@loc/@prop and @img handles."
```
