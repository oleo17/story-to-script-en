# 07 — Video Model Prompts

Turning the shot list into prompts that specific models will actually obey.

The hard truth this module exists to solve: **the same prompt does not work across models.** Veo wants the camera first. Seedance wants the subject first. Runway refuses to understand a negative prompt. A prompt written for one model and pasted into another produces something worse than either.

So the workflow is: build one **shot packet** that captures everything the shot needs, then render it in the target model's dialect.

---

## 1. What every model agrees on

Four rules hold across Veo, Sora, Runway, Kling, Seedance, and MiniMax. Get these wrong and model-specific tuning is pointless.

### 1.1 One subject, one action

A single clip holds **one action with a beginning and an end**. Two actions chained with "then" or "after that" fail on all six models — the clip is too short to fit both, and the model averages them into mud.

> **BAD** — "She picks up the letter, reads it, then starts crying."
>
> **GOOD** — "Her eyes move down the page. Her jaw sets."

The reading and the reacting are two clips.

**Practical ceiling: three beats per clip.** "Lifts the cup, takes a sip, looks out the window" is at the ceiling.

### 1.2 Concrete environment

"Abandoned warehouse at dusk" carries specific information. "Dark building" carries none. Name the place, the time, and one physical detail the light can catch.

### 1.3 One camera move

Two moves in one prompt fight each other and produce warped geometry. Pick one, add a speed modifier.

> **BAD** — "dynamic sweeping camera pushing in while orbiting"
>
> **GOOD** — "slow, steady dolly in, 10%"

### 1.4 Expect multiple takes

Professional practice is **5–10 generations per shot**, keeping one. Build that into the schedule and the budget. A prompt that works on the first try is luck, not craft.

---

## 2. The shot packet

Before choosing a model, fill this in. It is model-neutral.

```text
[PACKET 2.3]
Subject:      Marcus, 34, soaked wool coat, box at chest
Action:       extends the box toward the door; hands stop short of contact
End state:    box held at chest height, six inches from the opening door
Scene:        narrow pre-war corridor, night, rain audible
Light:        single ceiling fluorescent, top-left, green cast, flickering
Camera:       over-the-shoulder from behind Marcus, locked
Lens:         35mm equivalent, shallow, subject sharp, door soft
Style:        desaturated cool shadows, warm practicals only, fine 35mm grain
Aspect:       9:16
Duration:     3.5 s
Audio:        rain (muffled), one line of dialogue
Assets:       @char:mar_01 @prop:prop_box_01 @loc:loc_hall_a
Refs:         @img-02 (Marcus), @img-09 (box), @img-05 (hall)
Constraints:  no text, no watermark, no extra characters, stable hands
```

The packet is the single source of truth. If two models get different content, the packet was under-specified.

---

## 3. Model dialects

| Model | Order | Camera position | Audio | Negative prompt | Prompt length |
|---|---|---|---|---|---|
| **Veo 3.1** | Cinematography → Subject → Action → Context → Style | First | Native synced | One "avoid" sentence | Medium |
| **Sora 2** | Prose scene → Cinematography block → Actions block → Dialogue block | Own labeled block | Native | One "avoid" sentence | Short grants range; long restricts |
| **Runway Gen-4.5** | Camera movement → Scene → Action → Details | First | No native audio | None — phrase positively | Start short, layer detail |
| **Kling 2.6 / 3.0** | Scene → Subject → Motion → Style | After subject | 3.0 only | Separate field | Medium |
| **Seedance 2.0 / 2.5** | Subject → Action → Scene → Light/color → Camera → Style → Quality → Constraints | Fifth of eight | Native | One "avoid" sentence | Up to 1,000 words; be concise |
| **MiniMax Hailuo** | Subject + action, short | Brief | Limited | One sentence | Short |

Model versions and syntax change often. **Check the vendor's current guide before a production run** — the structures above are stable, the version numbers are not.

---

## 4. Veo 3.1

Thinks like a director: the shot comes first.

```text
Cinematography: over-the-shoulder, locked camera, 35mm equivalent, shallow depth of field,
  subject sharp, door soft.
Subject: Marcus, 34, soaked wool coat, brown cardboard box held at chest.
Action: he extends the box toward the opening door; his hands stop six inches short.
Context: narrow pre-war corridor at night, single flickering ceiling fluorescent,
  green cast, rain audible outside.
Style and ambiance: desaturated cool shadows, warm practicals only, fine 35mm grain,
  9:16 vertical.
Avoid: on-screen text, watermarks, additional characters.
```

Notes:
- **Native audio.** You can specify dialogue and ambience directly. Keep spoken lines short — one speaker per shot lip-syncs most reliably.
- Put dialogue in double quotes and name the speaker. Add "no subtitles" if you don't want burned-in text.
- The "Avoid" line is a single sentence. Long negative lists confuse it.

---

## 5. Sora 2

Narrative-driven; strong on physical simulation and cause-and-effect chains.

```text
A narrow pre-war corridor at night. Marcus, 34, in a soaked wool coat, holds a
brown cardboard box at chest height and extends it toward a door that is opening
four inches. His hands stop short of contact. Rain is audible.

Cinematography: over-the-shoulder from behind Marcus, locked camera, 35mm, shallow
  focus, 9:16.
Actions: he raises the box; his arms halt mid-extension; fingers tighten on the edge.
Dialogue: MARCUS (quiet, hoarse): "It's addressed to you."
Avoid: on-screen text, watermarks, extra people.
```

Notes:
- **Describe actions as beats**, not moods. "Takes two steps, stops, looks up" beats "moves hesitantly."
- Camera and action go in **separate labeled blocks** — this is the model's documented preference and it materially improves compliance.
- **Shorter prompts give more creative range; longer ones restrict it.** This is the documented trade-off. When a shot must be exact, be long and specific. When you want the model to surprise you, be short.
- Strong on liquids, fabric, and multi-axis motion. If the shot is about how a material behaves, this is the model.

---

## 6. Runway Gen-4.5

Camera-led, editorially strong, and allergic to negative prompts.

```text
Slow, steady dolly in, ten percent. A narrow pre-war corridor at night, green
fluorescent flicker. Marcus, 34, soaked wool coat, extends a brown cardboard box
toward an opening door; his hands stop short. Shallow focus, 35mm feel, desaturated
cool shadows, warm practicals, fine grain, 9:16 vertical.
```

Notes:
- **No negative prompt.** Phrase everything positively: instead of "no extra people," write "the corridor is empty except for Marcus."
- **Build in layers**: run the first sentence alone, then add camera, then scene motion, then style. This is how the tool is designed to be used.
- Camera movement goes first, and it is the strongest signal in the prompt.
- No native audio — plan sound in post (`08`).

---

## 7. Kling 2.6 / 3.0

Scene and subject first, motion after. Very good on faces, especially Asian features, and priced for iteration.

```text
Scene: narrow pre-war apartment corridor at night, single ceiling fluorescent
  flickering, green cast, brown carpet.
Subject: Marcus, 34, soaked wool coat, brown cardboard box at chest.
Motion: he raises the box toward the opening door, arms halting six inches short,
  fingers tightening on the edge.
Style: desaturated, warm practicals, fine grain, shallow depth, 9:16.

Negative: extra limbs, distorted hands, on-screen text, watermark, duplicate character
```

Notes:
- **Use the separate negative field.** Do not bury constraints in the prose.
- 3.0 supports multi-shot prompting; 2.6 is single-shot.
- Concise, action-focused phrasing works better than long prose.
- Good for rapid iteration — generate a wide set cheaply, then re-run winners on a more expensive model.

---

## 8. Seedance 2.0 / 2.5

Writes like a production brief. Native audio, strong at keeping product labels and printed text intact.

```text
1. Subject: Marcus, 34, soaked wool coat, brown cardboard box with a handwritten
   label held at chest height.
2. Action: he extends the box toward the opening door; his hands stop six inches
   short; fingers tighten on the corner.
3. Scene: narrow pre-war corridor at night, rain audible, single flickering ceiling
   fluorescent, green cast.
4. Lighting and color: cool desaturated shadows, warm practical from the doorway,
   green fluorescent key from top-left.
5. Camera movement: over-the-shoulder from behind Marcus, locked, 35mm feel,
   shallow depth.
6. Visual style: 35mm film grain, muted grade, realistic production still.
7. Image quality: sharp subject, soft background, natural skin texture.
8. Constraints: no on-screen text, no watermark, no extra characters, stable hands.
```

Notes:
- The eight-part structure is the model's documented format. Use all eight even when a part is short.
- **Recommended ceiling is 1,000 English words** — but "as concise as possible" is also in the same guide. Aim for 120–200 words of substance.
- Accepts timestamped multi-shot prompts. For a sequence, write `Shot 1 [0–3s]: … Shot 2 [3–6s]: …`
- **Best at product anchoring**: if a label, package, or printed page must survive, this is the model.
- Native audio supports dialogue, ambience, and music cues.

---

## 9. MiniMax Hailuo

Short prompts, strong stylization, prompt optimizer that will rewrite your text.

```text
Marcus, soaked coat, holds a cardboard box toward an opening door, hands stopping
just short. Narrow corridor, flickering green fluorescent, night. Locked over-the-
shoulder camera, shallow focus, fine grain. No text.
```

Notes:
- **Turn the prompt optimizer off** when exact wording matters. It rewrites silently.
- Keep it short. This model rewards brevity more than any other on the list.
- Good for stylized or non-photoreal looks.

---

## 10. Constraints and what to block

Always block these three, on every model, every prompt:

```text
no on-screen text, no logos, no watermarks
```

Then add the ones the shot actually risks:

| Risk | Constraint |
|---|---|
| Hands breaking | stable hands, five fingers, non-distorted |
| Crowd inventing people | the corridor is empty except for Marcus / no additional characters |
| Face morphing | consistent facial features, identity locked to reference |
| Duplicate characters | one Marcus in frame, no clones |
| Style drift | consistent grade throughout, no style shift |
| Motion stutter | smooth continuous motion, no flicker |
| Audio clipping (models with sound) | natural audio, clean fade, no clipping |

### 10.1 Contradictory pairs to avoid

Some constraints cancel each other and the model picks at random:

| Pair | Result |
|---|---|
| "film grain" + "ultra sharp 4K" | Random pick, usually sharp and sterile |
| "cinematic film look" + "handheld documentary" | Incoherent |
| "slow motion" + "high-speed action" | Neither |
| Three or more named artists/directors | Averaged into mush |

Pick one side of each axis.

---

## 11. Image-to-video and start-frame chaining

Text-to-video drifts. Image-to-video does not, because the reference does the identity work.

### 11.1 The rule

For any shot containing a recurring character, prop, or location, **generate from an image**, not from text alone.

Move only the things that should move. Describe what must stay identical.

```text
Image-to-video prompt:
The figure in the image extends the box toward the opening door; hands stop short.
Camera locked. Rain continues. Nothing else in frame moves.
```

### 11.2 Start-frame chaining

The single most reliable technique for long, consistent sequences:

1. Generate shot 1
2. **Take its last frame as the first frame of shot 2**
3. Describe only the change

This carries wardrobe, light, and geometry across a sequence without re-specifying anything. Chain through a block, then re-anchor with a fresh reference image at the block boundary.

### 11.3 When text-to-video is correct

- Establishing shots with no recurring character
- Style frames and look development
- Shots where you want the model to invent (dream, montage, abstraction)
- Cheap iteration before committing to a locked look

---

## 12. Audio in prompts

Three of the six models generate native audio. Use it deliberately.

```text
Audio: rain on glass (soft, continuous). One line of dialogue, quiet and hoarse.
No music.
```

Guidance:
- **Name the ambience explicitly** — models default to silence or generic hum
- **One speaker per shot** for clean lip-sync
- **Keep spoken lines short.** A long line will be rushed or clipped
- **Say "no music"** if you'll add score in post. Otherwise the model invents a bed you'll have to remove
- Put dialogue in quotes with the speaker named, and add "no subtitles" if text must not be burned in

---

## 13. Drift control during production

| Drift | Cause | Fix |
|---|---|---|
| Face changes between shots | Text-only prompts | Switch to image-to-video with the locked ref |
| Wardrobe changes | State not specified per shot | Add state to the packet: "coat soaked," "sleeve torn" |
| Location geometry moves | Reference image shot from a different angle | Use the same ref, crop differently |
| Grade shifts | Style described differently per prompt | Copy the style line verbatim across all prompts |
| Prop shape changes | Prop not in the reference set | Lock a single-object reference image |

**Copy-paste, don't paraphrase.** The style line, the character description, and the light line should be identical strings across every prompt in a block. Paraphrasing is where drift enters.

---

## 14. Testing protocol

Never generate the whole piece before checking.

1. **Pick the hardest shot** — usually the one with a face, a hand, and a prop together
2. Generate **10 variations** at the cheapest model that supports the shot
3. If none work, the packet is wrong, not the model. Rewrite the packet.
4. Lock the look from the winning frame
5. Only then produce the rest, using the winning frame as reference

This costs 10 generations and saves 200.

---

## 15. Output format

```text
[PROMPT PACK — Block 2]
Model: <target>        Aspect: 9:16        Audio: native / post
Shot count: n          Est. generations: n × 6

2.1  [prompt text]
     refs: @img-06         negative: <list>        duration: 2.0 s
2.2  [prompt text]
     refs: @img-01 @img-02 negative: <list>        duration: 3.0 s
...

CONTINUITY ANCHORS (copy verbatim into every prompt in this block)
  style: "<exact string>"
  light: "<exact string>"
  character: "<exact string>"

PACKET DELTAS FROM SHOT LIST
  <any field where the packet differs from the shot list, and why>
```

---

## 16. Handoff

```text
[HANDOFF]
Stage: Prompt pack complete
Model: <chosen, and why>
Locked so far: packets, anchors, negative lists, reference map
Main risks: <e.g. the label text must survive — Seedance only; faces at 9:16 crop>
Next step:
- Suggested module: 08-post-sound (after generation), or back to 06 on drift
- Materials needed: model credits, generation budget approval
- Copy-paste invocation: "Generate Block 2 at 6 takes per shot; return the winning frame per shot."
```
