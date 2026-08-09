---
name: suno-songcraft
description: Build release-ready Suno prompts — Style Box, Lyrics Box with structure tags and performance cues, Exclude Styles, creative sliders, duration control, and model choice across v4.5 / v4.5+ / v5 / v5.5. Use this skill whenever the user mentions Suno, AI music generation, style prompts, song metatags, or asks for lyrics intended for generation — and equally when they want to fix a track that came out generic, muddy, off-genre, rushed, too long, or with buried vocals. Carries deep support for Italian- and Neapolitan-language songs: pronunciation control, dialect diction, and genre playbooks for cantautorato, itpop, trap italiana, italo disco, canzone napoletana, neomelodico and tammurriata. Also covers instrumental tracks, Voices/Personas/Custom Models, stem extraction, Studio edits, and the artist-name blocklist that silently breaks prompts.
---

# Suno Songcraft

Suno builds a complete song — melody, harmony, arrangement, vocals — from a small set of inputs: the **Style Box**, the **Lyrics Box**, the **Creative Sliders**, the **Duration** control, and the **model** you pick. Most bad output traces back to a handful of specific mistakes in those places, not to a shortage of adjectives.

Work from the field limits below. They are the single most common source of stale advice.

## Field limits (current models)

| Field | V4.5 / V4.5+ / V5 / V5.5 | V4 and older |
|---|---|---|
| Style Box | **1,000 chars** | 200 chars |
| Lyrics Box | **5,000 chars** | 3,000 chars |
| Title | 100 chars | 80 chars |

Limits follow the **model version**, not the subscription tier. Two caveats matter more than the caps:

- **Practical lyrics ceiling is ~3,000 chars** (roughly 200–350 words, up to 500 for rap). Past that, Suno rushes, compresses, or skips sections outright.
- **Practical style ceiling is far below 1,000.** Most effective style boxes run 100–400 chars. The constraint is descriptor quality, not length.

Any guidance claiming a 120- or 200-character style limit predates V4.5 and should be discarded.

## Pick the model before writing anything

The prompt you write depends on which model runs it — v4.5 rewards long descriptive briefs, v5 and v5.5 are literal and need *less* instruction. Suno's own advice is not to rerun old V4/V4.5 prompts on V5; rewrite instead of porting.

| Model | Released | Reach for it when |
|---|---|---|
| **V4.5** / **v4.5-all** | May 2025 (free tier Oct 2025) | Free account, or heavy genres (metal, hardcore) where V5 sounds thin |
| **V4.5+** | Jul 2025 | You need Add Vocals / Add Instrumental on an existing track |
| **V5** | Sep 2025 | Cleanest audio and most natural vocals with tight prompt adherence |
| **V5.5** | Mar 2026 | Default for new work — richest arrangements, plus Voices, Custom Models, My Taste, and the Duration slider |

Full capability matrix, per-model prompting differences, and the feature timeline: **`references/models-and-versions.md`**

## Five rules that prevent most failures

**1. The Lyrics Box is sung literally — everything in it.**
Parenthetical stage directions get sung as words. `(atmospheric opening)`, `(build-up lyrics)`, `(Instrumental break)` will come out of the vocalist's mouth. Only actual lyrics and bracketed tags belong there. For an instrumental passage use a bare tag: `[Guitar Solo]`, `[Break]`, `[Instrumental]`.
*(Narrow exception: parenthetical backing-vocal echoes are intentional — `I'm on fire (on fire!)` — and per-section genre cues are a deliberate K-pop switch-up technique. Both are covered in `references/lyrics-box.md`.)*

**2. Vocals go first in the Style Box.**
`Male baritone, gritty, storytelling. Alternative rock, clean electric guitar, driving bass. Modern production.` — not the reverse. Position carries weight; a vocal description buried at the end gets outcompeted.

**3. Never use real artist or band names.**
Suno actively filters them; the prompt fails or degrades. Describe the sound instead: not "Aphex Twin" but `IDM, glitchy beats, ambient textures`. See `references/style-box.md`.

**4. Every descriptor must add distinct information.**
The failure mode is the *synonym-pile*: "imperious, commanding, regal, grand, theatrical" is one mood said five times, and it dilutes attention rather than reinforcing it. A focused ~10-descriptor box is fine. Collapse synonyms; keep genuinely distinct instrument, vocal, and production detail.

**5. Put the emotional arc in per-section Performance Cues, not in more adjectives.**
Append a one-or-two-word cue to each structure tag: `[Verse 1 - cold restrained]`, `[Bridge - raw breaking]`, `[Chorus - open anthemic]`. Bare `[Verse]` / `[Chorus]` throughout is a common and easily-missed cause of flat, generic output. Do this by default on every track.

## Style Box

**Shape:** `[Vocal identity]. [Genre + instrumentation]. [Production notes]`

```
Female alto, smoky, low register, restrained phrasing. Trip-hop, dusty
breakbeat, upright bass, Rhodes. Warm analog mix, vocal upfront.
```

Include, in rough priority order: vocal identity → genre (2–3 descriptors max) → 2–4 key instruments → mood/energy → tempo/BPM → 1–2 production notes.

Genre specificity beats genre stacking. `Midwest emo, math rock influences, clean guitar` works; six fused genres produce mud.

A **conversational production brief** is the officially supported alternative on V4.5 and later — Suno's own example is *"Create a melodic, emotional deep house song with organic textures and hypnotic rhythms. Begin with soft ambient layers, natural sounds, and a deep, steady groove. Build gradually with flowing melodic synths, warm basslines, and intricate, subtle percussion."* Use it when the track has an arc worth narrating; use the comma-separated shape when precision on specific elements matters more. Don't mix the two halfway.

**Exclude Styles (negative prompting)** shifts odds against an element — probabilistic, never a hard filter. Keep to 2–4 items in `no [element]` form. The dedicated Exclude Styles field (Custom Mode → Advanced Options) is the reliable path; appending `no …` inline to the style box is the weaker fallback. Most useful against Suno's habit of over-adding group vocals: `no choir, no backing vocals, no gang vocals`.

Full construction guidance, vocal descriptor vocabulary, and the artist blocklist: **`references/style-box.md`**

## Lyrics Box

```
[Short Instrumental Intro]

[Verse 1 - quiet close]
First line of lyrics
Second line of lyrics

[Pre-Chorus - lifting]
Build lyrics

[Chorus - open anthemic]
Hook lyrics

[Verse 2 - harder]
...

[Bridge - raw exposed]
...

[Chorus - full]
...

[Outro]
...

[End]
```

- **Structure tags on every section.** Without them, arrangement is unpredictable.
- **`[Intro]` is unreliable** — prefer `[Short Instrumental Intro]` or `[Intro - Spoken]`. A long intro also buries the vocals.
- **`[End]` is the strongest stop signal.** Songs that trail off or cut awkwardly are usually missing it.
- **Bridge before the final chorus** is standard pop convention and worth following, but it is a songwriting norm, not a Suno constraint — genres with different shapes should follow their own.
- **6–12 syllables per line** (7–9 verse, 10–12 chorus) locks vocals in best. Hyphens sustain notes (`lo-ove`); ALL CAPS shouts.
- **To stop word substitution**, add at the top: `Do not change any words. Sing exactly as written.` Suno has token biases and will drift toward favorites — Neon, Echo, Ghost, Silver, Shadow, Whisper, Crystal, Velvet.

Full tag inventory, reliability tiers, bar-count targeting, sound effects, duets: **`references/lyrics-box.md`**

## Creative sliders

Sliders sit *on top of* the prompt. They change how hard Suno commits to it, never what it makes.

| Slider | Low | High |
|---|---|---|
| **Weirdness** | Predictable, hooky, conventional | Experimental; more variance, more takes needed |
| **Style Influence** | Loose, blends freely, happy accidents | Genre-pure, tags enforced hard |
| **Audio Influence** | Reference is a loose seed | Output hews to the uploaded audio *(appears only with an upload)* |

Suno describes Weirdness as **Safe → Chaos with 50% as the normal expected result**, and Style Influence as **Loose → Strong**. Treat 50/50 as the true baseline.

**Diagnose before touching anything.** Wrong genre, wrong instruments, wrong tempo, wrong vocal character, mispronunciation → these are *prompt* problems and no slider fixes them. Generic-but-correct, drifting, chaotic, or wooden → those are slider problems.

Generate at defaults first. Then move **one slider, one small step**, and regenerate. Changing a slider and the prompt in the same pass makes the result uninterpretable.

Per-genre starting ranges, interaction effects, full diagnosis table: **`references/sliders-and-iteration.md`**

## Duration

Since July 2026 there is a **Duration slider** in the Create form on web with V5.5 — set the target length before generating instead of fighting the arrangement afterwards. It offers an Auto mode (model decides) and a Custom mode; reported range runs from about 10 seconds to 6 minutes in 5-second steps.

The slider sets a target, not a contract. Structure still has to fit it: asking for 90 seconds while supplying three verses and a bridge forces Suno to rush or truncate. Match the section count to the length.

**When the slider isn't available** — mobile, API, or any model below V5.5 — section count is the only lever:

| Target | Structure |
|---|---|
| Under 2:00 | 1–2 sections + `[End]`. Add `short` or `concise` to the style box |
| Under 3:00 | 2 verses max, short bridge, no extended instrumentals |
| 3:00–5:00 | Standard structure |
| Over 5:00 | 3+ verses, pre-chorus, bridge, 1–2 instrumental sections; add `extended` or `epic` |

Without the slider, expect 2–3 generations to land near target, and trim in post. Max is ~8 minutes on V4.5 and later; quality degrades past 6–7.

## Italian and Neapolitan

The skill carries a deep layer for Italian-language repertoire, because pronunciation is where those tracks actually fail — the arrangement can be perfect and one swallowed final vowel still gives the record away.

Three rules apply to any non-English track:

- **Lyrics in the target language, Style Box always in English.** Suno's style vocabulary is English-trained; translated descriptors land unreliably. The language of the lyric is itself a style descriptor: `sung in Italian with native diction`.
- **One language per section.** Mixing inside a section drifts the pronunciation across the whole section, not just the mixed line.
- **Exclude the drift**: `no English vocals` earns its place in almost every Italian generation.

Beyond that, reach for the reference files rather than improvising:

| Situation | File |
|---|---|
| Any Italian-language lyric — final vowels, geminates, stress, homographs, elision | `references/italian-language.md` |
| Cantautorato, itpop, Sanremo, rap and trap italiana, italo disco, pizzica, liscio, colonna sonora | `references/italian-genres.md` |
| Anything in Neapolitan — schwa, sound changes from Italian, apostrophes, tammurriata, neomelodico, sceneggiata | `references/neapolitan-language.md` |

`italian-genres.md` also carries the Italian half of the artist blocklist — the decomposition of named Italian artists into genre, vocal texture, instrumentation and production era, since naming them outright makes the prompt fail.

## Workflow

1. **Establish intent** — genre and mood, theme, language, vocal direction, target duration, and whether Voices / Custom Model / Persona is active. Ask only for what's genuinely missing; infer the rest and state the assumption.
2. **Pick the model** — V5.5 unless the user is on free tier or working in a heavy genre. State which one the prompt is written for, since it changes how much instruction to give.
3. **Check the instrumental branch** — if instrumental, set `Instrumental: On`, drop all vocal description from the style box, and use structure tags only in the lyrics box (`[Intro]`, `[Main Theme]`, `[Break]`, `[End]`). Skip steps involving vocals entirely.
4. **Build the Style Box** — vocals first, then genre, instruments, mood, tempo, production. Pull concrete texture and range words rather than emotion words (see rule 4 and `references/style-box.md`).
5. **Decide exclusions** — 2–4 items, or explicitly none. Consider what the genre implies: acoustic folk → `no electric instruments`; a cappella → `no instruments`.
6. **Write the Lyrics Box** — structure tags with Performance Cues on every section, syllable counts in range, `[End]` at the close, no parentheticals.
7. **Set sliders and duration** — defaults unless the genre table suggests otherwise; duration matched to the section count.
8. **Run the pre-flight checklist** below.
9. **Present every field ready to paste** (format below).
10. **Iterate** — generate several takes, pick the closest, then use the Song Editor on the weak 20% rather than regenerating the whole track. Log what changed each pass.

## Output format

Present the fields separately and paste-ready, with character counts so the user can see the headroom:

```
MODEL: v5.5 · INSTRUMENTAL: Off

STYLE BOX  (238/1000)
────────────────────────────────
<style prompt>

LYRICS BOX  (1,847/5000)
────────────────────────────────
<tagged lyrics>

EXCLUDE STYLES: <2-4 items, or "none">
SLIDERS: Weirdness <x> · Style Influence <y>
DURATION: <target, or "Auto">
```

Then add a short note on what to listen for on the first take and which lever to move if it misses.

For non-English tracks, see the Italian and Neapolitan section above — the language rules apply to the output format too.

## Pre-flight checklist

- [ ] Model stated, and the prompt written for that model's verbosity
- [ ] Style Box opens with vocal identity (or the track is instrumental)
- [ ] No real artist or band names anywhere
- [ ] Every descriptor adds distinct information — no synonym-piles
- [ ] Genre held to 2–3 descriptors
- [ ] Exclude Styles decided — 2–4 items or an explicit "none"
- [ ] Lyrics Box contains only lyrics and bracketed tags — **no parentheticals**
- [ ] Every section carries a structure tag with a Performance Cue
- [ ] `[End]` or `[Fade Out]` closes the track
- [ ] Lyrics under ~3,000 chars; lines 6–12 syllables
- [ ] Section count matches the duration target
- [ ] All fields within limits, with counts shown

## Rights and catalog

Since the Warner Music partnership (Nov 2025), subscribers hold **commercial use rights** but are generally **not considered the owner** of generated output; Suno takes no revenue share.

**The free-tier trap is not reversible.** Tracks generated on a free account are permanently non-commercial — upgrading later does **not** retroactively unlock rights for anything already made. Anything that might eventually be released has to be generated on a paid plan from the start. The free plan also runs an older model line (v4.5-all); v5.5 requires Pro or Premier.

Two practical consequences worth raising when a user is building a catalog: **current models are slated for deprecation** when licensed models launch, so important generations should be downloaded now; and human creative contribution — original lyrics, live-tracked layers, arrangement decisions made in a DAW, a documented process — is what strengthens any ownership claim over a fully generated track.

## Reference map

| File | Read it when |
|---|---|
| `references/models-and-versions.md` | Choosing a model; a feature may not exist on the user's tier; porting a prompt between versions |
| `references/style-box.md` | Building or debugging a style prompt; need vocal/texture vocabulary; checking the artist blocklist |
| `references/lyrics-box.md` | Formatting lyrics; choosing structure tags; bar counts, sound effects, duets |
| `references/sliders-and-iteration.md` | Choosing slider values; deciding prompt-vs-slider; Song Editor, extends, stems, Studio |
| `references/genre-playbook.md` | Need a genre-specific starting point, BPM range, or slider band |
| `references/italian-language.md` | Any Italian-language lyric — pronunciation, stress, geminates, homographs |
| `references/italian-genres.md` | Italian repertoire and the Italian artist blocklist |
| `references/neapolitan-language.md` | Anything in Neapolitan — language, traditions, instruments, rhythms |
| `references/troubleshooting.md` | A generation came back wrong and you need symptom → fix |

---

*Attribution and sources: see `CREDITS.md` at the plugin root. In short — parts of the general reference material are adapted from `bitwize-music-studio/claude-ai-music-skills` (CC0 1.0), and model/feature facts come from Suno's official release notes, blog and help centre, linked in `references/models-and-versions.md`. The Italian and Neapolitan material is original to this skill.*
