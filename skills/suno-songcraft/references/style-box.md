# Style Box Reference

Everything that goes in Suno's "Style of Music" field. Cap is 1,000 characters on V4.5/V5/V5.5, but effective boxes usually run 100–400.

## Contents
- [Anatomy](#anatomy)
- [Descriptor discipline](#descriptor-discipline)
- [Vocal identity](#vocal-identity)
- [Vocal texture and style vocabulary](#vocal-texture-and-style-vocabulary)
- [When emotion words fail](#when-emotion-words-fail)
- [Genre selection](#genre-selection)
- [Negative prompting](#negative-prompting)
- [Voices, Custom Models, Personas](#voices-custom-models-personas)
- [Artist name blocklist](#artist-name-blocklist)

---

## Anatomy

**Shape:** `[Vocal identity]. [Genre + instrumentation]. [Production notes]`

Periods separate the three blocks; commas separate items within a block. Both are read.

```
1. Vocal identity     Female alto, smoky, low register, restrained phrasing
2. Genre + instruments Trip-hop, dusty breakbeat, upright bass, Rhodes
3. Production          Warm analog mix, vocal upfront
```

**Alternative — top-loaded palette.** Simpler, useful when the vocal is the hook:

```
[Mood] + [Energy] + [2 instruments] + [Vocal identity]

Melancholic, slow-burn, piano and strings, female alto with subtle vibrato
```

**Alternative — conversational production brief.** Officially supported since V4.5, and the shape Suno itself demonstrates. Useful when the track has an arc worth narrating rather than a list of elements worth naming:

```
Create a melodic, emotional deep house song with organic textures and
hypnotic rhythms. Begin with soft ambient layers, natural sounds, and a
deep, steady groove. Build gradually with flowing melodic synths, warm
basslines, and intricate, subtle percussion
```

Pick one shape and commit. A half-list, half-narrative box reads as neither and dilutes both. On V5/V5.5 keep the brief shorter than you would on V4.5 — those models honour more of what's written, so a paragraph that added richness on V4.5 can add clutter here.

**Optional additions that earn their place:** BPM (critical for dance genres, useful everywhere), key, era ("90s alt-rock with Britpop undertones"), and one arrangement note ("verse 2: bass rests for 4 bars").

---

## Descriptor discipline

V5 is literal and dilutes attention when descriptors restate each other. The target is not a word count — it's that **each descriptor tells Suno something the others don't.**

```
❌ Synonym-pile — one idea said six ways:
"Ethereal indie folk with vintage analog warmth and melancholic undertones,
finger-picked acoustic, tape hiss, lo-fi, intimate, breathy, whispery,
nostalgic, contemplative, minimalist production"

❌ Too vague:
"Nice upbeat music"

✅ Every term doing distinct work:
"Sad indie folk, acoustic, gentle, breathy female vocal, intimate"
```

The widely-repeated "4–7 descriptors maximum" rule traces to a single third-party guide and isn't borne out in practice — rich ~10-descriptor boxes work well when the terms are distinct. **Trim synonyms, not detail.** Real bloat starts above ~12.

Where the emotional arc belongs: **per-section Performance Cues in the Lyrics Box**, not a longer adjective list here. The Style Box carries the baseline mood; the arc is sectional.

---

## Vocal identity

Put it **first**. Position carries weight — a vocal description at the end gets outcompeted by everything before it.

**Pattern:** `[gender/range], [texture], [delivery style]`

```
Male tenor, warm, slightly raspy, indie rock delivery
Female alto, sultry, breathy, R&B phrasing with subtle runs
Male baritone, gravelly, introspective, folk storyteller
```

V5 also has a dedicated **Voice Gender selector** in Advanced Options (male/female). It is more reliable than prompt text alone — use it as the baseline and let the prompt handle texture and delivery.

### Section-by-section vocal dynamics

Useful when describing how the performance should evolve:

| Section | Dynamics | Phrasing | Vibrato |
|---|---|---|---|
| Verse | Low | Tight | Minimal |
| Pre-Chorus | Rising | Shorter | Growing |
| Chorus | High / open | Sustained | Full |
| Bridge | Variable | New texture | Altered |

---

## Vocal texture and style vocabulary

Reach for these instead of emotion words. They describe *audible qualities*, which Suno can render.

**Range:** soprano, mezzo-soprano, alto, contralto, tenor, baritone, bass-baritone, low register, chest voice, head voice

**Texture:** whispered, gravelly, velvety, dreamy, resonant, nasal, brassy, metallic, saturated, smoky, weathered, rough-edged, shimmery, glassy, crunchy, liquid, breathy exhale

**Delivery:** staccato, legato, vibrato-heavy, monotone, melismatic, syncopated, operatic, chanting, spoken-word, growling, belting, humming, rapping, scatting, falsetto runs, call-and-response

**Vocal FX (Style Box prose, not bracket tags):** reverb / spacious reverb, slapback delay, auto-tuned, natural pitch, vocoded, distorted vocals, telephone effect

**Regional flavor:** British rock vocal, Southern gospel, Nashville country, New York hip-hop, Jamaican dancehall, Irish folk

### Duets and two-character dialogue

Alternate the section tags per character in the Lyrics Box, and state the arrangement in the Style Box so Suno generates two distinct voices:

```
Lyrics Box:                    Style Box:
[Verse - Character A]          Dual vocalists, male and female,
...                            trading verses
[Verse - Character B]
...
```

For a blended chorus, describe it directly — `duet chorus, blended male/female harmony` — rather than inventing a bracket tag.

---

## When emotion words fail

Two distinct failure modes, both fixed the same way.

### Symptom: vocal sounds too young despite "mature" / "deep"

Age adjectives are weak signals and lose to breathy-coded words sitting nearby (intimate, whispered, delicate).

- Replace the age word with a concrete range: `alto`, `contralto`, `baritone`, `bass-baritone`
- Add maturity-coded textures: `smoky`, `weathered`, `resonant`, `gravelly`
- Drop `breathy`, `whispered`, `delicate` if you want an older voice — they skew young in training data
- Add `no youthful or breathy vocals` to exclusions

```
❌ Female character vocal, mature and deep, aching and intimate
✅ Female alto, low register, smoky and weathered, resonant and world-weary
```

### Symptom: vocal sounds generic despite "powerful" / "defiant"

Emotion words describe what the performance should *feel like*, not what the voice should *sound like*. Suno has no reliable mapping from emotion to timbre, so it defaults to a competent, characterless genre voice.

```
❌ Female character vocal, powerful and defiant
✅ Female mezzo-soprano, gritty and raw, rasp on the belted notes,
   commanding chest voice, weathered and fierce
```

Keep one or two emotion words if they set the arc — the fix is making sure concrete texture and range carry the actual load.

### If it still misses

Two escalations, in order:

1. **Inline per-section metatags in the Lyrics Box** — a vocal descriptor inside the section tag, repeated on *every* section: `[Verse 1: Raspy older female vocal, husky contralto]`. Different mechanism from the Style Box; Suno may weight it independently. This is an escalation, not a default pattern.
2. **Check whether the genre tag is fighting you.** "Pop" carries a bright/youthful bias no adjective fully cancels. Swap for genre words that are inherently mature-vocal-coded: `torch song`, `vintage soul`, `cabaret`, `1940s jazz`, `vintage country`.

Beyond that, Personas or Voices (Pro/Premier) are more reliable than further style-box iteration.

---

## Genre selection

More specific is better — but stop at 2–3 genre descriptors.

**Pattern:** `[primary genre] + [1–2 subgenre modifiers] + [1 key technique]`

```
Generic:  Rock
Better:   Alternative rock
Best:     Midwest emo, math rock influences, clean guitar
Too much: Midwest emo, math rock, post-rock, shoegaze, ambient, clean guitar,
          intricate picking, reverb-heavy    ← Suno can't honor all of these
```

Fusions work up to about three genres: "hip-hop with jazz influences", "indie folk meets trip-hop". Extreme cross-style fusions produce mud.

---

## Negative prompting

Exclusions **shift the odds** against an element. They are probabilistic, not a filter, and won't override a prompt that strongly implies the thing being excluded.

**Where they go:**
- **Pro / Premier** → the dedicated **Exclude Styles** field (Custom Mode → Advanced Options). The reliable path.
- **No field available** → append inline to the Style Box: `..., no drums, no autotune`. Weaker but still nudges.

**Rules:**
- **2–4 items maximum.** Over-specification dilutes the effect.
- Simple `no [element]` form.
- Record the decision even when empty — an explicit "none" confirms it was considered rather than skipped.

**What's worth excluding:**

| Category | Examples |
|---|---|
| Instruments | `no drums`, `no electric guitar`, `no strings` |
| Vocal processing | `no autotune`, `no heavy reverb` |
| Stylistic | `no EDM drops`, `no screaming`, `no key change` |
| Group vocals *(Suno's most common over-add)* | `no choir`, `no crowd vocals`, `no backing vocals`, `no gang vocals`, `no call-and-response`, `no vocal harmonies` |

Group vocals are stubborn: excluding them improves the odds, but a big anthemic prompt pulls them back in. Pair the exclusion with a leaner, more intimate style prompt.

**Auto-populate from context** when the genre clearly implies it:

```
Acoustic folk  → no electric instruments, no drums
A cappella     → no instruments
Lo-fi chill    → no aggressive vocals
```

---

## Voices, Custom Models, Personas

All three change what the Style Box should contain — the point is to stop the style prompt fighting the feature that already carries that information. Custom Models are Pro/Premier; Voices reached mobile in Aug 2026 with reduced functionality on free plans.

| Feature | What it carries | What to drop from the Style Box |
|---|---|---|
| **Voices** (v5.5 voice cloning) | The specific voice | Gender, range, and vocal-identity descriptors |
| **Custom Models** (v5.5 fine-tuning, 6+ of your tracks) | Your production aesthetic | Generic production language — "glossy", "polished mix", "modern pop production" |
| **Personas** | Vocals, style, and vibe of a past generation | Vocal identity; keep the style prompt to 1–2 genres plus instrumentation |

Voice + Persona is redundant — pick one. With Voices, keep **Audio Influence fairly high (~0.70–0.85)** or the result drifts toward a generic vocal. Custom Models are best for album consistency; generic v5.5 is better for deliberately off-brand tracks.

**My Taste** (all tiers) learns passively and shapes the *style autogenerate* button only. It does not override explicit prompts.

Voice capture rules, verification, plan gating and the full feature timeline: **`models-and-versions.md`**.

---

## Artist name blocklist

**Suno actively filters real artist and band names.** The prompt fails or produces unexpected results. If you catch yourself typing a name, stop and describe the sound.

| Don't say | Say instead |
|---|---|
| Daft Punk | French house, vocoder vocals, disco-funk, filtered synths |
| Aphex Twin | IDM, glitchy beats, ambient textures, experimental |
| Deadmau5 | progressive house, melodic synths, building drops |
| Skrillex | aggressive dubstep, heavy drops, distorted bass |
| Kraftwerk | robotic vocals, minimal synths, electronic pioneer |
| Eminem | rapid-fire aggressive rap, complex rhyme schemes, intense delivery |
| Kendrick Lamar | conscious hip-hop, jazz samples, introspective, dynamic flow |
| Travis Scott | dark trap, auto-tuned vocals, psychedelic, atmospheric |
| MF DOOM | abstract lyrics, jazz samples, complex wordplay |
| Miles Davis | cool jazz, modal, atmospheric trumpet, sophisticated |
| John Coltrane | spiritual jazz, intense saxophone, exploratory |
| Billie Holiday | torch song, melancholic jazz vocals, intimate |
| Metallica | thrash metal, aggressive riffs, double bass drums |
| Led Zeppelin | blues rock, powerful vocals, heavy riffs, epic |
| Pink Floyd | progressive rock, atmospheric, psychedelic, conceptual |
| Nirvana | grunge, raw vocals, quiet-loud dynamics, angst |
| Black Sabbath | doom metal, heavy riffs, dark |

The pattern generalizes: **decompose the artist into genre + vocal texture + instrumentation + production era.** That description is usually more useful to Suno than the name would have been anyway.

Ordinary words can also trip the filter when they collide with a producer tag — "ninety-three" hits the `ninetythree` tag, for instance. On a filter error, try an alternate spelling (`'93`) or rephrase.
