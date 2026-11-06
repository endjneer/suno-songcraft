# Lyrics Box Reference

Everything that goes in Suno's lyrics field. Cap is 5,000 characters on the v6 family — but **~3,000 is the practical ceiling** before Suno starts rushing, compressing, or skipping sections. Target 200–350 words for most genres, up to 500 for rap.

## Contents
- [The literal-singing rule](#the-literal-singing-rule)
- [Structure tags](#structure-tags)
- [Tag reliability](#tag-reliability)
- [Performance cues](#performance-cues)
- [Delivery tags](#delivery-tags)
- [Bar count targeting](#bar-count-targeting)
- [Line and syllable craft](#line-and-syllable-craft)
- [Sound effects](#sound-effects)
- [Preventing word substitution](#preventing-word-substitution)
- [Structure templates](#structure-templates)
- [Instrumental tracks](#instrumental-tracks)
- [Multi-language and code-switching](#multi-language-and-code-switching)

---

## The literal-singing rule

**Suno sings everything in this box that isn't a bracketed tag.** This is the single most damaging misunderstanding about the lyrics field.

```
❌ Will be sung out loud as words:
(Machine-gun snare, guitars explode)
(Instrumental break)
(Verse 1)
(atmospheric opening)
(build-up lyrics)

✅ Bracketed tags — read as structure, not sung:
[Intro]  [Verse]  [Chorus]  [Guitar Solo]  [Break]
```

Stage directions, production notes, and parenthetical descriptions all belong in the **Style Box** or nowhere. For an instrumental passage, a bare descriptive tag does the job: `[Guitar Solo]`, `[Drum Break]`, `[Instrumental]`.

This isn't an argument for keeping the Lyrics Box thin. Suno's own guidance, published with V4.5, is the opposite: keep *genre-level* information in the Style field and put *song-level* context directly in the Lyrics field. That context arrives as bracketed structure tags and performance cues — the mechanisms below — not as prose.

### Two deliberate exceptions

**Backing-vocal echoes.** Parentheses are the correct way to trigger a call-and-response echo, because you *want* those words sung:

```
I'm on fire (on fire!)
Never coming back (never coming back)
```

**Per-section genre cues for mid-song switch-ups.** A K-pop-derived technique for songs that change genre between sections. The parenthetical *will* influence the arrangement — occasionally at the cost of a stray sung word, so use it only when the switch-up is the point:

```
[Chorus]
(Explosive EDM drop, heavy bass, full energy)
...lyrics...

[Bridge]
(Stripped-back ballad, solo piano)
...lyrics...
```

If neither of these is what you're doing, no parentheses.

---

## Structure tags

Every section gets one. Without tags, arrangement is unpredictable.

**Openings:** `[Intro]`, `[Short Instrumental Intro]`, `[Intro - Spoken]`, `[Fade In]`

**Body:** `[Verse]`, `[Verse 1]`, `[Verse 2]`, `[Catchy Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Hook]`, `[Catchy Hook]`, `[Post-Chorus]`, `[Bridge]`, `[Refrain]`

**Instrumental:** `[Break]`, `[Interlude]`, `[Guitar Solo]`, `[Guitar Solo Interlude]`, `[Drum Break]`, `[Percussion Break]`, `[Melodic Interlude]`, `[Dance Break]`

**Endings:** `[Outro]`, `[End]`, `[Fade Out]`, `[Fade to End]`, `[Big Finish]`

**Rap-specific:** `[Rap Verse]` signals a distinct vocal character — use it rather than letting a rap section sit under a plain `[Verse]`.

**Group:** `[All]`, `[Group]` before chant or unison sections.

---

## Tag reliability

Not all tags land equally. These tiers were observed on V5-era models; unverified on v6.

| Tier | Tags |
|---|---|
| **Reliable** | `[Verse]` / `[Verse 1]`, `[Chorus]`, `[End]`, `[Fade Out]`, `[Pre-Chorus]` |
| **Moderate** | `[Bridge]`, `[Break]`, `[Outro]` |
| **Unreliable** | `[Intro]`, `[Post-Chorus]`, `[Fade In]`, custom tags |

`[Intro]` is the notable weak spot — use `[Short Instrumental Intro]` or `[Intro - Spoken]` instead. Keeping the intro short also stops it burying the vocals, which is one of the most common complaints about Suno output.

`[End]` is the strongest stop signal available. Tracks that trail off, loop, or cut abruptly are almost always missing it.

---

## Performance cues

**Do this by default on every track.** Append a brief cue — a word or two after a dash — to each structure tag:

```
[Verse 1 - quiet intimate]
[Pre-Chorus - lifting]
[Chorus - building anthemic]
[Verse 2 - harder, more clipped]
[Bridge - raw exposed]
[Chorus - full release]
```

This is how an emotional arc gets carried across a song. Leaving every section as a bare `[Verse]` / `[Chorus]` is a common, easy-to-miss cause of flat output — the track is technically correct and emotionally inert.

**Keep the cue short.** A word or two. Long cue lists become noise, and the budget is shared with delivery tags below: **no more than 3 bracketed descriptors per section, total.**

---

## Delivery tags

Standalone bracket tags that color performance without defining a section. Optional accents — 1–3 per section, counted against the same budget as performance cues.

```
[Shout]        [Whispered]     [Spoken]       [Melancholy]
[Energetic]    [Aggressive]    [Intimate]     [Playful]
[Triumphant]   [Vulnerable]    [Haunting]     [Whimsical]
```

These are not a substitute for mood and energy prose in the Style Box. Stacking many at once produces the same prompt fatigue as a synonym-pile.

---

## Bar count targeting

Target bar counts can be appended to section tags (tested on V5; unverified on v6):

```
[INTRO 4] [VERSE 1 8] [PRE 4] [CHORUS 8] [VERSE 2 8] [PRE 4]
[CHORUS 8] [BRIDGE 8] [CHORUS 8] [OUTRO 4]
```

Results are approximate — Suno treats these as targets, not guarantees. Most useful for controlling intro and outro length and balancing section proportions.

---

## Line and syllable craft

| Section | Syllables per line |
|---|---|
| Verse | 7–9 |
| Chorus | 10–12 |
| Absolute range | 6–12 |

Lines outside this range lock in poorly — the vocal either rushes or leaves dead space.

**Notation that works:**
- Hyphens sustain a note: `lo-ove`, `sooo-long`
- Repeated letters create sustain and emphasis: `Loooove`, `Ohhhh`
- ALL CAPS shouts: `NEVER AGAIN`
- Commas are pauses; ellipses trail off

**Structure economy:** two verses plus chorus plus bridge is the sweet spot. Four- and five-verse songs get compressed or truncated.

---

## Sound effects

Bracketed effect tags trigger vocal and environmental sounds inline:

```
[Verse 1]
Walking through the night [footsteps]
I hear a voice calling [echo]
Then suddenly [laughter] breaks the silence
```

**Human:** `[laughter]`, `[screaming]`, `[whisper]`, `[sigh]`, `[gasp]`, `[cough]`

For atmospheric and environmental sound — rain, crowds, traffic, wind — mention it in **both** the Lyrics Box tag and the Style Box. A single mention often doesn't survive.

---

## Preventing word substitution

Suno has known token biases and will quietly swap your words for its favorites: **Neon, Echo, Ghost, Silver, Shadow, Whisper, Crystal, Velvet.** If these appear in output you didn't write, that's the model defaulting, not a creative choice.

Add at the top of the lyrics:

```
Do not change any words. Sing exactly as written.
```

For proper nouns, dialect, homographs, and anything Suno is likely to mangle, spell phonetically. Hyphenated romanization is more reliable than native script for pronunciation control.

---

## Structure templates

### Pop / rock
```
[Short Instrumental Intro]
[Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [Bridge] → [Chorus] → [Outro] → [Fade Out]
```

### Hip-hop
```
[Intro - Spoken] → [Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [Verse 3] → [Outro] → [End]
```

### Punk (short and fast)
```
[Intro] → [Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [Break] → [Chorus] → [Big Finish]
```

### K-pop (more sections than Western pop)
```
[Intro] → [Verse 1] → [Pre-Chorus] → [Chorus] → [Post-Chorus] → [Verse 2] →
[Pre-Chorus] → [Chorus] → [Rap Verse] → [Bridge] → [Dance Break] →
[Final Chorus] → [Outro]
```
The final chorus often modulates up a half-step — note `(key change up, maximum energy)` as a section cue. Keep `[Dance Break]` lyrics minimal or empty.

**On bridge placement:** putting the bridge before the final chorus is standard pop convention and a good default, but it's a songwriting norm rather than a Suno constraint. Genres with different shapes should follow their own.

---

## Instrumental tracks

With `Instrumental: On`, the lyrics box holds **structure tags only** — no words at all:

```
[Intro]
[Main Theme]
[Bridge]
[Main Theme]
[Outro]
[End]
```

Drop all vocal description from the Style Box too, and spend that space on instrumentation, mood, and arrangement. Section count is the main duration lever: for a ~1:00–1:30 cue, `[Intro] → [Main Theme] → [End]` is usually right.

---

## Multi-language and code-switching

- Romanized text with hyphens is more reliable for pronunciation than native script: `Sa-rang-hae` beats `Saranghae`
- Add `[Clear Vocals]` or `[High Fidelity Vocals]` when mixing languages
- Keep languages in **separate sections** where possible rather than alternating mid-line
- Dialects and regional pronunciations benefit from the same phonetic-respelling treatment as proper nouns — write what you want heard, not what's orthographically correct
