# Troubleshooting

Symptom → cause → fix. Work top-down: most complaints about Suno output resolve to one of the first four entries.

## Contents
- [Check this first on v6](#check-this-first-on-v6)
- [Vocal problems](#vocal-problems)
- [Structure and arrangement problems](#structure-and-arrangement-problems)
- [Mix and production problems](#mix-and-production-problems)
- [Lyric problems](#lyric-problems)
- [Genre and style problems](#genre-and-style-problems)
- [Generation failures](#generation-failures)
- [Quick lookup table](#quick-lookup-table)

---

## Check this first on v6

**Read the style line of the generated song.** If the tags came back different from what you wrote, Variety rewrote them — that is its documented behavior, and the only documented cause of rewritten tags. Set Variety to Off and regenerate before diagnosing anything else. Every fix below assumes Variety is Off.

**Early user reports on v6** (anecdotal, not confirmed by Suno): dull or muffled top end, vocals buried in the mix, BPM and genre ignored. Rule out Variety first, then work the matching entry below — [Vocals buried under the band](#vocals-buried-under-the-band), [Mix and production problems](#mix-and-production-problems), [Output drifts off-genre or ignores the tags](#output-drifts-off-genre-or-ignores-the-tags) — and state the BPM explicitly in the style box.

**With Suno's connector, measure before guessing.** `audio-analysis`, `audio-lyrics-alignment` and `audio-listen` are free and turn most symptoms below into a measured finding — see `suno-connector.md`.

---

## Vocal problems

### Lyrics are inaudible or the clip won't sing
Suno's randomization occasionally produces a clip that refuses to sing; more often the cause is an overly complex style prompt or a long intro burying the vocals.

- Simplify the prompt — fewer descriptors, clearer intent
- Replace `[Intro]` with `[Short Instrumental Intro]`
- Add `clear and prominent vocals` to the style box
- Introduce vocals early, with a hook or a wordless `(Ahh ahh ahh)` line
- If none of that works, regenerate — sometimes it's just a bad roll

### Vocals buried under the band
- Put the vocal description **first** in the style box if it isn't already
- Add a mix instruction: `lead vocal 1–2 dB louder than band`
- Thin the arrangement — fewer simultaneous instruments in the style box

### Vocal sounds too young despite "mature" or "deep"
Age adjectives are weak signals, outcompeted by breathy-coded words nearby.

- Swap the age word for a concrete range: `alto`, `contralto`, `baritone`, `bass-baritone`
- Add maturity-coded texture: `smoky`, `weathered`, `resonant`, `gravelly`
- Remove `breathy`, `whispered`, `delicate`, `intimate` — they skew young
- Exclude: `no youthful or breathy vocals`
- Expect 2–3 regenerations; this narrows odds rather than guaranteeing

### Vocal is technically fine but characterless
Emotion words ("powerful", "defiant", "heartbroken") describe intent, not timbre. Suno can't map them to a voice, so it defaults to a competent genre-standard vocal.

- Replace with audible qualities: range + grain. `gritty`, `raspy`, `rasp on the belted notes`, `raw chest voice`, `commanding`
- Keep one or two emotion words to set the arc, but let texture do the work
- Exclude: `no generic or polished studio pop vocal`

### Still wrong after all of the above
Escalate in this order:
1. **Inline per-section metatags** in the lyrics box, repeated on every section: `[Verse 1: Raspy older female vocal, husky contralto]`
2. **Check whether the genre tag is fighting you** — "pop" carries a bright/youthful bias. Swap to `torch song`, `vintage soul`, `cabaret`, `1940s jazz`
3. **Voices** (Pro/Premier), or Personas (unverified on v6) — more reliable than further style-box iteration

### Wrong gender
Use the **Voice Gender selector** in Advanced Options rather than relying on prompt text. It's the most reliable control available.

---

## Structure and arrangement problems

### Song jumps straight into vocals with no intro
Missing intro tag. Add `[Short Instrumental Intro]` — but keep it short, or you trade this problem for buried vocals.

### Song cuts off, trails away, or loops oddly at the end
Missing stop signal. Add `[Outro]` followed by `[End]`. `[End]` is the strongest terminator available. `[Fade Out]` also works when a fade is wanted.

### No build, weak climax, structurally flat
Two separate causes, often together:
- Missing `[Pre-Chorus]` and `[Bridge]` — the tension-building sections
- **No Performance Cues.** Bare `[Verse]` / `[Chorus]` throughout gives Suno no arc to play. Add cues: `[Verse 1 - restrained]` → `[Chorus - open]` → `[Bridge - raw]`

### Sections repeat or blur together
- Number the verses explicitly: `[Verse 1]`, `[Verse 2]`
- Vary the actual lyric content between them
- Give each section a distinct Performance Cue

### Song is rushed, sections skipped or compressed
Lyrics are too long. The cap is 5,000 chars but Suno starts rushing well before it — target ~3,000 chars / 200–350 words. Cut to two verses plus chorus plus bridge.

### Wrong length
Section count is the primary lever. Add or remove sections, use `[End]` to force termination, and expect 2–3 generations to land near target. Trim in post for an exact length.

The Duration slider announced for V5.5 on web may also be in the Create form on v6 — verify in-app on v6. Through the API, `duration` (15–360 s) is a target, not a guarantee. Either way the structure has to fit: a 90-second target with three verses and a bridge still forces Suno to rush or truncate.

### Arrangement too busy
Specify rests directly: `verse 2: bass rests for 4 bars`. Also reduce the instrument count in the style box — 2–4 key instruments, not a full inventory.

---

## Mix and production problems

| Symptom | Fix |
|---|---|
| Muddy, unclear | `clean production, wide stereo field, good instrument separation` |
| Flat, lifeless | `bus compression 2–3 dB, slow attack, fast release` |
| Chorus doesn't lift | `double-time hats, octave guitars` on the chorus |
| Too loud / distorted | This is a mastering issue, not a generation issue. Suno outputs -9 to -7 LUFS for pop/EDM; master to -14 LUFS / -1.0 dBTP for streaming |
| Unwanted choir or backing vocals | The most common Suno over-add. `no choir, no backing vocals, no gang vocals` — probabilistic, so also lean the prompt more intimate |
| Unwanted instrument | 2–4 exclusions in `no [element]` form. More than 4 dilutes all of them |

---

## Lyric problems

### Suno changed my words
Token bias. The model gravitates toward **Neon, Echo, Ghost, Silver, Shadow, Whisper, Crystal, Velvet**. Add at the top of the lyrics box:
```
Do not change any words. Sing exactly as written.
```

### Stage directions are being sung
The lyrics box is sung literally. Parentheticals like `(instrumental break)` or `(building tension)` come out of the vocalist's mouth. Move them to the style box, or replace with a bare tag: `[Break]`, `[Guitar Solo]`.

### Mispronunciation
Spell phonetically in the lyrics box. Hyphenated syllables give the most control. This applies to proper nouns, dialect, technical terms, and homographs — write what you want heard, not what's correct orthographically. No slider fixes this.

### Lyrics degraded after extending
Extends accumulate damage. Cap at 2–3 per song, and write the extended sections explicitly rather than letting Suno improvise them.

---

## Genre and style problems

### Output drifts off-genre or ignores the tags
- First confirm the tags weren't rewritten — Variety Off
- Raise Style Influence
- If it's still off, the genre tag is too vague — sharpen it. `Rock` → `Midwest emo, math rock influences, clean guitar`

### Output is on-genre but generic
- Raise Weirdness slightly **or** lower Style Influence slightly — one at a time
- Check the style box for a synonym-pile. Five words for one mood give Suno nothing to act on
- Check for missing Performance Cues

### Output is chaotic and incoherent
Lower Weirdness, keep Style Influence mid-to-high. If you also fused four genres, cut to two.

### Result feels rigid and wooden
Very high Style Influence on a thin or self-contradictory prompt. Lower Style Influence slightly, or fix the contradictions — `quiet aggressive`, `fast slow ballad`, and similar pairs make the engine enforce tags that fight each other.

### Heavy genres sound thin
A known weakness on V5, unverified on v6 — and there is no older model to fall back on any more. Lock Style Influence high, Weirdness low, Variety Off.

---

## Generation failures

### Prompt fails or returns something unrelated
Almost always a **filtered artist or band name**. Suno blocks them. Replace with a description of the sound.

Ordinary words can collide with producer tags too — "ninety-three" hits the `ninetythree` tag. Try an alternate spelling (`'93`) or rephrase.

### Nothing changed after my edit
If a slider and the prompt were both changed in the same pass, the result is uninterpretable. Revert one and go again — one variable per generation.

Also rule out session carryover before concluding a fix failed: confirm on a fresh generation.

---

## Quick lookup table

| Symptom | It's a… | First move |
|---|---|---|
| Style tags changed in the output | slider | Variety → Off |
| Wrong genre | prompt | Sharpen the genre tag |
| Wrong instruments | prompt | Name 2–4 explicitly |
| Wrong tempo | prompt | State BPM |
| Wrong vocal character | prompt | Concrete range + texture |
| Mispronunciation | lyrics | Phonetic respelling |
| Stage directions sung | lyrics | Remove parentheticals |
| Rushed / skipped sections | lyrics | Cut to ~3,000 chars |
| No build or arc | lyrics | Add Performance Cues + `[Pre-Chorus]` / `[Bridge]` |
| Abrupt or endless ending | lyrics | Add `[End]` |
| Generic but correct | slider | Weirdness up **or** Style Influence down |
| Off-genre drift | slider | Style Influence up |
| Chaotic | slider | Weirdness down |
| Wooden | slider | Style Influence down |
| Cover doesn't match source | slider | Audio Influence up |
| Prompt outright fails | filter | Remove the artist name |
| Too quiet or too loud | mastering | Not a Suno problem — master to -14 LUFS |
