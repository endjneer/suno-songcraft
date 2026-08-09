# Sliders and Iteration Reference

The sliders and the post-generation tools. Everything here is about *refining* an output, not producing the first one.

## Contents
- [What the sliders do](#what-the-sliders-do)
- [Weirdness](#weirdness)
- [Style Influence](#style-influence)
- [Audio Influence](#audio-influence)
- [Interaction effects](#interaction-effects)
- [Prompt problem or slider problem](#prompt-problem-or-slider-problem)
- [Iteration discipline](#iteration-discipline)
- [Song Editor](#song-editor)
- [Extending](#extending)
- [Stem extraction](#stem-extraction)
- [Suno Studio](#suno-studio)
- [Known limitations](#known-limitations)

---

## What the sliders do

The sliders sit *on top of* the style prompt. They don't change **what** Suno makes — the prompt does that. They change **how hard Suno commits** to it and **how far it may wander**.

Suno's own descriptions are deliberately terse: Weirdness runs **Safe → Chaos**, where **50% is the normal expected result**; Style Influence runs **Loose → Strong**; Audio Influence appears only when audio has been uploaded. Everything below is a working refinement of that, not official doctrine.

Positions below are on a 0.00–1.00 scale, matching the API's `styleWeight` and `weirdnessConstraint`. If the interface shows 0–100, read `0.70` as `70`. These bands are starting points: generate once at the 50/50 baseline, then dial in by ear.

---

## Weirdness

How experimental Suno's choices are — melody, harmony, arrangement quirks, structural surprises.

| Position | Behavior |
|---|---|
| **Low** `0.00–0.30` | Predictable, hooky, familiar. Conventional song shapes. The safe zone for radio-style results |
| **Mid** `0.30–0.55` | Mostly conventional with occasional pleasant surprises |
| **High** `0.55–1.00` | Odd chord moves, unusual textures, less predictable structure. Rewarding, but drift and misfires increase |

Raise it when output is too safe or generic. Lower it when you need a dependable hook.

High Weirdness increases **variance between generations** — expect to generate more takes and cherry-pick.

---

## Style Influence

How tightly output adheres to the style prompt — genre hallmarks, named instruments, mood words.

| Position | Behavior |
|---|---|
| **Low** `0.00–0.40` | Prompt treated as a suggestion. Blends influences freely, fills gaps its own way. Good for fusions and happy accidents |
| **Mid** `0.40–0.60` | Honors the prompt while leaving room to breathe |
| **High** `0.60–1.00` | Tags enforced hard. Strong genre purity |

Raise it when output drifts off-genre or ignores tags. Lower it for fusions, for surprises, or when a dominant Persona is over-processing the mix.

**Caution:** very high Style Influence on a thin or self-contradictory prompt produces a rigid, wooden result — the engine is enforcing tags that fight each other. Fix the prompt before pushing the slider further.

---

## Audio Influence

How much uploaded reference audio shapes the output. **Appears only when audio is uploaded** — via Cover, Upload Audio, Sample to Song, or Voices.

| Position | Behavior |
|---|---|
| **Low** `0.00–0.40` | The upload is a loose seed; the prompt leads |
| **Mid** `0.40–0.65` | Output carries the reference's character while following the prompt |
| **High** `0.65–1.00` | Output hews closely to the upload's melody, feel, and arrangement |

Raise it when a cover doesn't resemble the source enough. Lower it for more transformation.

**With Voices (cloning), keep it fairly high — ~0.70–0.85** — or Suno drifts toward a generic vocal.

---

## Interaction effects

| | **Low Style Influence** | **High Style Influence** |
|---|---|---|
| **High Weirdness** | **Wild card** — maximum surprise, genre may dissolve. Good for idea-mining; expect drift and many regenerations | **Adventurous within the lane** — unexpected choices that still read as the genre. The sweet spot for keeping a familiar genre fresh |
| **Low Weirdness** | **Loose and smooth** — Suno fills gaps its own way but stays tame. Good for gentle fusions | **Safe and on-genre** — faithful, predictable, release-ready. The risk is a generic result |

**High Weirdness + a specific genre tag** is the reliable "interesting but not chaotic" combination — the genre tag anchors the surprises. Pushing both sliders to extremes is a deliberate wild card, not a fine-tuning move.

**Audio Influence interactions:**
- *High Audio + Low Weirdness* — tracks the reference closely. Safest for faithful covers
- *High Audio + High Weirdness* — a tug-of-war; striking reinterpretations or incoherent mud. Move one slider at a time
- *High Audio + High Style Influence* — two adherence pulls competing. If the reference and the prompt describe different things, decide which is the source of truth and relax the other

---

## Prompt problem or slider problem

The single most useful habit: diagnose *before* touching anything.

The **prompt** decides what the track is — genre, instruments, mood, tempo, vocal identity. A slider cannot add a banjo, fix a mispronunciation, or change the tempo. The **sliders** decide how strictly Suno commits and how far it may wander.

| Symptom | First move |
|---|---|
| Generic / too safe | Raise Weirdness slightly **or** lower Style Influence slightly — one at a time |
| Drifts off-genre, ignores tags | Raise Style Influence; if still off, sharpen the genre tag |
| Chaotic / incoherent | Lower Weirdness, keep Style Influence mid–high |
| Rigid / wooden | Lower Style Influence slightly **or** simplify the prompt |
| Wrong instruments, mood, tempo | **Prompt.** Not a slider issue |
| Mispronunciation, wrong words | **Lyrics + phonetics.** Not a slider issue |
| Vocal character wrong | **Prompt** — concrete range and texture words |
| Cover doesn't resemble source | Raise Audio Influence |
| Cover too close | Lower Audio Influence and/or raise Weirdness |

---

## Iteration discipline

1. Write a clear, focused prompt first
2. **Generate at default slider positions.** Don't pre-adjust blind
3. Listen, then diagnose — prompt problem or slider problem
4. Move **one thing, one small step**, regenerate
5. **Log every attempt** — the value changed and what it did

**The golden rule:** adjusting a slider *and* rewriting the prompt in the same pass makes it impossible to know which move helped.

Generate several takes per prompt rather than one, and pick the closest to intent before refining. When a descriptor combination works, save it — a personal library of proven style boxes compounds faster than any general guide.

Suno's own guidance is worth repeating: **don't rerun old V4/V4.5 prompts on V5.** V5 listens differently and needs less instruction. Rewrite rather than port.

---

## Song Editor

Section-level editing without regenerating the whole track. If ~80% of a take is right, edit the rest rather than rolling the dice again.

| Action | What it does |
|---|---|
| **Remake** | Regenerate a section with the same prompt |
| **Rewrite** | Change lyrics/melody for a section, preserving its role |
| **Extend** | Append bars at the tail of a section |
| **Reorder** | Move sections within the arrangement |
| **Delete** | Remove weak sections; transitions are engine-handled |

Workflow: generate a full song → identify weak sections → Remake/Rewrite them individually → extend 1–2 bars into or out of a chorus for smooth transitions → delete weak regions and let the engine smooth.

**Cap extensions at 2–3 per song.** Beyond that, lyrics get uneven and vocals weaken.

**Regenerate from scratch only when** the overall structure or genre is wrong, the fundamental mood misses, or vocals are consistently off-key. Those are prompt problems, and editing won't reach them.

---

## Extending

Extending appends to an existing generation up to the ~8-minute ceiling. Lyrics tend to degrade across repeated extends — write the added sections explicitly rather than letting Suno improvise, and keep the total number of extends low.

---

## Stem extraction

Overhauled in June 2026: stems are now *generatively regenerated* rather than frequency-carved, so extracted parts sound cleaner and more natural.

| Mode | What it does | Output |
|---|---|---|
| **Auto Split** | Splits the song into 12 stem categories at once | 12 stems |
| **Split from Mix** | Pulls one chosen instrument or voice out | 2 stems: target + everything else |
| **Advanced Split** | Extracts one instrument from a list of ~100 | 1 targeted stem *(Premier, per-extraction cost)* |

The 12 Auto Split categories: Vocals, Backing Vocals, Drums, Bass, Guitar, Keyboard, Strings, Brass, Woodwinds, Percussion, Synth, FX/Other.

Access via **More Actions (…) → Get Stems** on any clip. For an isolated vocal or single instrument, **Split from Mix** targeting that part is usually cleaner in one pass than repeated carving. If a stem still bleeds, run extraction again on the extracted stem.

**Loudness note:** Suno's raw output is not a master. Typical levels run -9 to -7 LUFS for pop/EDM and -12 to -11 for lo-fi. For streaming delivery, master to **-14 LUFS / -1.0 dBTP** regardless of genre.

---

## Suno Studio

Premier-tier generative DAW: timeline multitrack editing, stem generation and manipulation, MIDI export, audio upload, Sample-to-Song, and pitch transposition (±12 semitones, preserving melody and phrasing — useful for fixing key mismatches without spending credits on a regeneration).

**Sample to Song:** upload a short snippet (a guitar riff, a vocal melody), describe the full composition, and Suno expands it. Practical for building arrangements around a real recorded part — which also strengthens the human-contribution side of any ownership claim.

**Studio 1.2** (Feb 2026) added four things that change what's worth fixing in Studio rather than by regenerating:

| Tool | Use it for |
|---|---|
| **Remove FX** | Strip Suno's reverb/delay off a clip and re-apply your own plug-ins in a DAW. The fix for "too much reverb" that no prompt reliably delivers |
| **Warp Markers** | Set markers on transients (or automatically) to time-stretch and quantize loose audio to the grid |
| **Time Signature** | Anything outside 4/4 — the selector is in the bottom panel |
| **Alternates** | Hold several takes of a section side by side and swap between them |

Order of operations: set the time signature first, warp to fix timing, then Remove FX last.

## Lyrics editor (web)

Since July 2026 the web lyrics field is a full-screen editor with autosave, structure labels, natural-language editing ("make this line funnier"), variation suggestions, and saved *lyricist* examples that carry a voice across songs.

It's a drafting aid, not a formatting authority — it will not stop you writing parentheticals that get sung, and the syllable and tag discipline in `lyrics-box.md` still applies to whatever comes out of it.

---

## Known limitations

- Heavy electric guitars can sound dirty or blend together
- Acoustic nuance isn't always captured
- Niche subgenres (metalcore, extreme styles) may miss hallmarks
- Extreme cross-style fusions → muddy results
- Quality degrades past 6–7 minutes; hard ceiling ~8
- **V4.5 sometimes beats V5 for heavy genres.** If metal or hardcore output sounds thin, test both models

Current models are slated for deprecation when the WMG-licensed models launch. Download WAVs of anything worth keeping.
