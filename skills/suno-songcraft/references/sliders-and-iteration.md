# Sliders and Iteration Reference

The sliders and the post-generation tools. Everything here is about *refining* an output, not producing the first one.

## Contents
- [What the sliders do](#what-the-sliders-do)
- [Variety](#variety)
- [Weirdness](#weirdness)
- [Style Influence](#style-influence)
- [Audio Influence](#audio-influence)
- [Max Mode](#max-mode)
- [Interaction effects](#interaction-effects)
- [Prompt problem or slider problem](#prompt-problem-or-slider-problem)
- [Iteration discipline](#iteration-discipline)
- [Plain-language edits](#plain-language-edits)
- [Song Editor](#song-editor)
- [Extending](#extending)
- [Stem extraction](#stem-extraction)
- [Suno Studio 2.0](#suno-studio-20)
- [Known limitations](#known-limitations)

---

## What the sliders do

Weirdness, Style Influence and Audio Influence sit *on top of* the style prompt. They don't change **what** Suno makes — the prompt does that. They change **how hard Suno commits** to it and **how far it may wander**. **Variety**, new in v6, is the exception: it changes the style prompt itself (see below).

Suno's own descriptions are deliberately terse: Weirdness runs **Safe → Chaos**, where **50% is the normal expected result**; Style Influence runs **Loose → Strong**; Audio Influence appears only when audio has been uploaded. Everything below is a working refinement of that, not official doctrine.

Positions below are on a 0.00–1.00 scale, matching Suno's API: `controls.weirdness`, `controls.style_influence`, `controls.audio_influence`. The names `styleWeight` and `weirdnessConstraint` that circulate in guides come from third-party wrappers, not from Suno's API. If the interface shows 0–100, read `0.70` as `70`. These bands are starting points: generate once at the 50/50 baseline with Variety Off, then dial in by ear.

---

## Variety

New in v6, and different in kind from the other three. It doesn't change how hard Suno commits to the style prompt: it **adjusts and reinterprets the style prompt itself** before generating.

| Setting | API `controls.variety` | Behavior |
|---|---|---|
| **Off** | `0` | Style tags used as written |
| Normal → High → Extra → Max | `1`–`4` | Suno adjusts and reinterprets the style prompt before generating |

**Set it to Off for any style box written with care** — which is every style box this skill produces. Suno's v6 FAQ: Variety introduces variety "by adjusting and updating your style prompts", and to keep full control of the style tags you reduce it to 0. Left on, you end up testing Suno's rewrite of your prompt instead of your prompt. Raise it only when the user wants Suno to reinterpret a loose idea.

**How to tell it was on:** read the style line of the generated song. Tags that came back different from what you wrote are Variety's doing — not a Style Influence problem, and not a prompt problem.

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

## Max Mode

Not a slider but an optional toggle on any generation, at a multiple of the normal credit cost. Suno recommends it for:

- songs longer than ~2 minutes
- covers that should stay close to the original
- style transfer
- keeping vocals and style consistent across the whole track

Treat it as a spend decision: suggest it when one of those applies, give the reason, and leave it to the user. Through the API, `max_mode` is set only when the user asks for it.

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
| Style tags came back changed | **Variety → Off.** Check this before anything else |
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
2. **Generate at default slider positions, with Variety Off.** Don't pre-adjust blind
3. Listen, then diagnose — prompt problem or slider problem
4. Move **one thing, one small step**, regenerate — with the model held fixed
5. **Log every attempt** — the value changed and what it did

**The golden rule:** adjusting a slider *and* rewriting the prompt in the same pass makes it impossible to know which move helped.

Generate several takes per prompt rather than one, and pick the closest to intent before refining. When a descriptor combination works, save it — a personal library of proven style boxes compounds faster than any general guide.

**Coming from v5.5:** don't assume a v5.5 prompt behaves the same on v6. Regenerate it on v6 with Variety Off and compare before reusing it — see `models-and-versions.md`.

---

## Plain-language edits

Since v6, an existing song can be edited by describing the change. Try this first when one part is wrong — it leaves the rest of the song alone:

- **A section:** `Change the chorus so it's sung by a gospel choir`
- **A single word:** `Change the lyric from 'love' to 'light'`

Remix & Edit on v6 also covers Extend, Cover, Replace Section and more. Reach for the Song Editor below when the fix is structural — reordering, deleting, remaking several sections.

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

## Suno Studio 2.0

Premier-tier generative DAW: timeline multitrack editing, stem generation and manipulation, MIDI export, audio upload, Sample-to-Song, and pitch transposition (±12 semitones, preserving melody and phrasing — useful for fixing key mismatches without spending credits on a regeneration).

**Studio 2.0** (Aug 13 2026) added:

- MIDI and recording
- automation
- effects and plugins created through chat
- a wavetable synth
- Split from Mix / Advanced Split stem separation inside the session
- unlimited exports of multitracks and stems at 32-bit/48 kHz

Those unlimited exports matter since the Sep 2026 download caps: on Premier, export finals and stems from Studio rather than spending the monthly download allowance.

**Sample to Song:** upload a short snippet (a guitar riff, a vocal melody), describe the full composition, and Suno expands it. Practical for building arrangements around a real recorded part — which also strengthens the human-contribution side of any ownership claim.

**Studio 1.2** (Feb 2026) added four things that change what's worth fixing in Studio rather than by regenerating (whether each carries over unchanged into 2.0 is unverified):

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
- Quality degraded past 6–7 minutes in v5-era testing (unverified on v6); hard ceiling 8 on every v6 model
- **Heavy genres can sound thin.** There is no older model to fall back on any more: lock Style Influence high, Weirdness low, Variety Off, and name the subgenre and vocal type
- Early v6 user reports (anecdotal): dull or muffled top end, buried vocals, BPM and genre ignored — see the top of `troubleshooting.md`

Models before v6 were retired on Sep 9 2026; their songs stay in the library. Downloads are now capped per plan (see `models-and-versions.md`), so download keepers rather than every take.
