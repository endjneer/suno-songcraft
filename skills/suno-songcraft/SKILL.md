---
name: suno-songcraft
description: Build release-ready Suno prompts — Style Box, Lyrics Box with structure tags and performance cues, Exclude Styles, creative sliders including Variety and Max Mode, duration control, and model choice across v6 / v6-wild / v6-mini. Use this skill whenever the user mentions Suno, AI music generation, style prompts, song metatags, or asks for lyrics intended for generation — and equally when they want to fix a track that came out generic, muddy, off-genre, rushed, too long, with buried vocals or with style tags Suno rewrote, edit an existing song in plain language, or migrate prompts from v5.5 to v6. Carries deep support for Italian- and Neapolitan-language songs: pronunciation control, dialect diction, and genre playbooks for cantautorato, itpop, trap italiana, italo disco, canzone napoletana, neomelodico and tammurriata. Also covers generating and checking songs through Suno's connector, instrumental tracks, Voices and Custom Models, stems, Studio, and the artist-name blocklist that silently breaks prompts.
---

# Suno Songcraft

Suno builds a complete song — melody, harmony, arrangement, vocals — from a small set of inputs: the **Style Box**, the **Lyrics Box**, the **Creative Sliders**, the **Duration** control, and the **model** you pick. Most bad output traces back to a handful of specific mistakes in those places, not to a shortage of adjectives.

Work from the field limits below. They are the single most common source of stale advice.

## Field limits

| Field | v6 family |
|---|---|
| Style Box | **1,000 chars** |
| Lyrics Box | **5,000 chars** |
| Simple mode description | **3,000 chars** |
| Title | 100 chars in-app *(v5-era figure)*; the API takes 256 |

The style, lyrics and description caps are the ones Suno's own API enforces; if the Create form's counter disagrees, trust the counter. Two caveats matter more than the caps (both measured on v5-era models; unverified on v6):

- **Practical lyrics ceiling is ~3,000 chars** (roughly 200–350 words, up to 500 for rap). Past that, Suno rushes, compresses, or skips sections outright.
- **Practical style ceiling is far below 1,000.** Most effective style boxes run 100–400 chars. The constraint is descriptor quality, not length.

Any guidance claiming a 120- or 200-character style limit predates V4.5 and should be discarded.

## Pick the model before writing anything

Since Sep 9 2026 every new generation runs on the v6 family. All earlier models (v4, v4.5, v4.5+, v5, v5.5) are retired for new generations: songs made with them stay in the library and can still be played, shared, remastered and covered, but every new iteration runs on v6.

| Model | Plans | Reach for it when |
|---|---|---|
| **v6** | Pro, Premier | Default for a deliberately built prompt — the precise, reliable model, for when you know what you want |
| **v6-wild** | Pro, Premier | Idea-mining. Favors unexpected choices and genre-blending, and moves away from the prompt by design. Take a keeper into v6 to refine it |
| **v6-mini** | All plans (the Free plan's model) | Quick ideas, high-volume drafts, concept tests |

All three generate up to 8 minutes. A standard generation costs 10 credits for 2 songs; Max Mode and prompts with many images or videos cost more.

v6 understands more musical language than the models before it, but the descriptor discipline below still holds: a tight box where every term does distinct work beats a longer one. **Hold the model fixed while iterating** — switching v6 ↔ v6-wild while also editing the prompt makes the result uninterpretable.

Full capability matrix, migration from v5.5, retired-model history and the feature timeline: **`references/models-and-versions.md`**

## Five rules that prevent most failures

**1. The Lyrics Box is sung literally — everything in it.**
Parenthetical stage directions get sung as words. `(atmospheric opening)`, `(build-up lyrics)`, `(Instrumental break)` will come out of the vocalist's mouth. Only actual lyrics and bracketed tags belong there. For an instrumental passage use a bare tag: `[Guitar Solo]`, `[Break]`, `[Instrumental]`.
*(Narrow exception: parenthetical backing-vocal echoes are intentional — `I'm on fire (on fire!)` — and per-section genre cues are a deliberate K-pop switch-up technique. Both are covered in `references/lyrics-box.md`.)*

**2. Vocals go first in the Style Box.**
`Male baritone, gritty, storytelling. Alternative rock, clean electric guitar, driving bass. Modern production.` — not the reverse. Position carries weight; a vocal description buried at the end gets outcompeted.

**3. Never use real artist or band names.**
Suno actively filters them, and still does on v6; the prompt fails or degrades. Describe the sound instead: not "Aphex Twin" but `IDM, glitchy beats, ambient textures`. v6 also screens uploaded audio and lyrics for unauthorized use. See `references/style-box.md`.

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

A **conversational production brief** became the officially supported alternative with V4.5 (unverified on v6) — Suno's own example is *"Create a melodic, emotional deep house song with organic textures and hypnotic rhythms. Begin with soft ambient layers, natural sounds, and a deep, steady groove. Build gradually with flowing melodic synths, warm basslines, and intricate, subtle percussion."* Use it when the track has an arc worth narrating; use the comma-separated shape when precision on specific elements matters more. Don't mix the two halfway.

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

Weirdness, Style Influence and Audio Influence sit *on top of* the prompt. They change how hard Suno commits to it, never what it makes. **Variety**, new in v6, is different in kind: it adjusts and reinterprets the style prompt itself before generating.

| Slider | Low | High |
|---|---|---|
| **Variety** *(v6)* | **Off** — style tags used as written | Normal → High → Extra → Max: Suno adjusts and reinterprets the style prompt |
| **Weirdness** | Predictable, hooky, conventional | Experimental; more variance, more takes needed |
| **Style Influence** | Loose, blends freely, happy accidents | Genre-pure, tags enforced hard |
| **Audio Influence** | Reference is a loose seed | Output hews to the uploaded audio *(appears only with an upload)* |

Suno describes Weirdness as **Safe → Chaos with 50% as the normal expected result**, and Style Influence as **Loose → Strong**. Treat 50/50 as the true baseline.

**Variety is Off in every prompt this skill builds.** Suno's v6 FAQ says Variety works by adjusting and updating the style prompt, and that setting it to 0 keeps full control of the style tags. Left on, it swaps the descriptor work for Suno's own rewrite, so you end up testing its prompt instead of yours. Raise it only when the user wants Suno to reinterpret the style.

**Diagnose before touching anything.** First read the style line of the generated song: tags that came back changed mean Variety rewrote them — set it to Off and regenerate. Wrong genre, wrong instruments, wrong tempo, wrong vocal character, mispronunciation → these are *prompt* problems and no slider fixes them. Generic-but-correct, drifting, chaotic, or wooden → those are slider problems.

Generate at defaults first, with Variety Off. Then move **one slider, one small step**, and regenerate. Changing a slider and the prompt in the same pass makes the result uninterpretable.

**Max Mode** is an optional toggle that costs a multiple of the normal credits. Suno recommends it for songs over ~2 minutes, covers that should stay close to the original, style transfers, and keeping voice and style consistent across the track. Suggest it when one of those applies, say why, and leave the spend to the user.

Per-genre starting ranges, interaction effects, full diagnosis table: **`references/sliders-and-iteration.md`**

## Duration

A **Duration slider** was announced for V5.5 on web (Jul 20 2026), with an Auto mode (model decides) and a Custom mode. Whether it is in the app on v6 is not confirmed — **verify in-app on v6** before relying on it. Through the Suno API, `duration` takes 15–360 seconds, as a target rather than a guarantee.

Any duration setting is a target, not a contract. Structure still has to fit it: asking for 90 seconds while supplying three verses and a bridge forces Suno to rush or truncate. **Section count is the primary lever**, slider or not:

| Target | Structure |
|---|---|
| Under 2:00 | 1–2 sections + `[End]`. Add `short` or `concise` to the style box |
| Under 3:00 | 2 verses max, short bridge, no extended instrumentals |
| 3:00–5:00 | Standard structure |
| Over 5:00 | 3+ verses, pre-chorus, bridge, 1–2 instrumental sections; add `extended` or `epic` |

Expect 2–3 generations to land near target, and trim in post. Every v6 model generates up to 8 minutes; v5-era testing found quality degrading past 6–7 (unverified on v6). For long tracks, consider Max Mode.

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

1. **Establish intent** — genre and mood, theme, language, vocal direction, target duration, the user's plan (Free runs only v6-mini), and whether Voices / Custom Model / Persona is active. Ask only for what's genuinely missing; infer the rest and state the assumption.
2. **Pick model and mode** — v6 for a deliberately built prompt, v6-wild for idea-mining, v6-mini for quick tests or on Free. Use **Custom mode** for anything this skill builds: separate Style and Lyrics fields are what make a miss diagnosable. **Simple mode** fits when the user wants to start from existing material: it takes Suno songs, playlists, uploaded audio, images and video in one prompt and chooses between Cover, Remix and Extend itself.
3. **Check the instrumental branch** — if instrumental, set `Instrumental: On`, drop all vocal description from the style box, and use structure tags only in the lyrics box (`[Intro]`, `[Main Theme]`, `[Break]`, `[End]`). Skip steps involving vocals entirely.
4. **Build the Style Box** — vocals first, then genre, instruments, mood, tempo, production. Pull concrete texture and range words rather than emotion words (see rule 4 and `references/style-box.md`).
5. **Decide exclusions** — 2–4 items, or explicitly none. Consider what the genre implies: acoustic folk → `no electric instruments`; a cappella → `no instruments`.
6. **Write the Lyrics Box** — structure tags with Performance Cues on every section, syllable counts in range, `[End]` at the close, no parentheticals.
7. **Set sliders, Max Mode and duration** — Variety Off; the other sliders at defaults unless the genre table suggests otherwise; Max Mode only when the track is long or must stay consistent, with the reason; duration matched to the section count.
8. **Run the pre-flight checklist** below.
9. **Present every field ready to paste** (format below). With Suno's connector, show the same fields and generate only after the user's go-ahead (see *Through Suno's connector*).
10. **Iterate** — generate several takes, pick the closest, then fix the weak 20% rather than regenerating the whole track. Try a plain-language edit first, on one section (`Change the chorus so it's sung by a gospel choir`) or one word (`Change the lyric from 'love' to 'light'`); then the Song Editor or Remix & Edit (Replace Section, Extend, Cover). With the connector, measure the take first. Log what changed each pass.

## Output format

Present the fields separately and paste-ready, with character counts so the user can see the headroom:

```
MODEL: v6 / v6-wild / v6-mini · MODE: Custom · INSTRUMENTAL: Off

STYLE BOX  (238/1000)
────────────────────────────────
<style prompt>

LYRICS BOX  (1,847/5000)
────────────────────────────────
<tagged lyrics>

EXCLUDE STYLES: <2-4 items, or "none">
SLIDERS: Variety Off · Weirdness <x> · Style Influence <y>
MAX MODE: Off (or On, with the reason)
DURATION: <target, matched by section count>
```

Then add a short note on what to listen for on the first take and which lever to move if it misses.

For non-English tracks, see the Italian and Neapolitan section above — the language rules apply to the output format too.

## Through Suno's connector

When Claude has Suno's connector (tools like `audio-create`, `audio-analysis`, `audio-listen`), it can generate the song itself and check the result. Three rules on top of the workflow:

- **Ask before spending credits.** Read `account-usage` (plan, credits, allowed models), show the fields in the format above, and generate only after the user says yes — again before every new round.
- **Send the skill's choices explicitly.** `model: "v6"` (or the one chosen) and `controls.variety: 0` on every call: omitted, Suno falls back to its own defaults, which aren't necessarily v6 or Off. Leave `duration` out with this skill's lyrics, or set `duration_strict: false`: by default it hard-cuts the song at the target with no outro.
- **Measure before fixing.** After a take, `audio-analysis` (tempo, key, sections, what is heard), `audio-lyrics-alignment` (words that weren't placed) and `audio-listen` (targeted questions) are free. Use them to find the problem, then apply `references/troubleshooting.md`.

| In the app | Connector field |
|---|---|
| Style Box | `style` (≤ 1,000) |
| Lyrics Box | `lyrics` (≤ 5,000) |
| Exclude Styles | `negative_style` |
| Variety | `controls.variety`, integer 0–4 (0 = Off … 4 = Max) — send `0` explicitly |
| Weirdness / Style Influence | `controls.weirdness` / `controls.style_influence`, 0–1 |
| Audio Influence | `controls.audio_influence`, 0–1, only with a `voice_id` |
| Voice Gender selector | `vocal_gender` |
| Model | `model`: `v6`, `v6-wild`, `v6-mini` — always send it |
| Max Mode | `max_mode`, set only when the user asks for it |
| Duration | `duration`, 15–360 s, a target; hard cap unless `duration_strict: false` |
| Simple mode | `description` (≤ 3,000), optionally with `reference_audio_ids` (up to 10 songs) |

Field mapping, plan gating, the traps with covers, extensions and `audio-edit`, and the full measure-then-fix loop: **`references/suno-connector.md`**

## Pre-flight checklist

- [ ] Model stated (v6 / v6-wild / v6-mini), and held fixed across iterations
- [ ] Variety Off unless the user wants Suno to reinterpret the style
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

**The free-tier trap is not reversible.** Tracks generated on a free account are permanently non-commercial — upgrading later does **not** retroactively unlock rights for anything already made. Anything that might eventually be released has to be generated on a paid plan from the start. The Free plan runs v6-mini; v6 and v6-wild require Pro or Premier.

**Downloads are capped** (Terms in force since Sep 3 2026): Free gets 7 trial downloads in total, for personal use only; Pro 20 a month; Premier 60 a month, plus unlimited exports from Studio. Extra downloads can be bought, and the caps also apply to songs made before Sep 3. Songs downloaded on a paid plan stay commercially usable. In practice: iterate inside Suno and download only keepers; on Premier, export finals and stems through Studio.

The deprecation earlier versions of this skill warned about has happened: pre-v6 models are retired for new generations, though their songs stay in the library. And human creative contribution — original lyrics, live-tracked layers, arrangement decisions made in a DAW, a documented process — is what strengthens any ownership claim over a fully generated track.

## Reference map

| File | Read it when |
|---|---|
| `references/models-and-versions.md` | Choosing among v6 / v6-wild / v6-mini; a feature may not exist on the user's plan; migrating a v5.5 prompt to v6 |
| `references/style-box.md` | Building or debugging a style prompt; need vocal/texture vocabulary; checking the artist blocklist |
| `references/lyrics-box.md` | Formatting lyrics; choosing structure tags; bar counts, sound effects, duets |
| `references/sliders-and-iteration.md` | Choosing slider values, Variety, Max Mode; deciding prompt-vs-slider; plain-language edits, Song Editor, extends, stems, Studio 2.0 |
| `references/genre-playbook.md` | Need a genre-specific starting point, BPM range, or slider band |
| `references/italian-language.md` | Any Italian-language lyric — pronunciation, stress, geminates, homographs |
| `references/italian-genres.md` | Italian repertoire and the Italian artist blocklist |
| `references/neapolitan-language.md` | Anything in Neapolitan — language, traditions, instruments, rhythms |
| `references/troubleshooting.md` | A generation came back wrong and you need symptom → fix |
| `references/suno-connector.md` | Generating through Suno's connector; checking a take with analysis, lyric alignment and listening |

---

*Attribution and sources: see `CREDITS.md` in the repository, https://github.com/endjneer/suno-songcraft. In short — parts of the general reference material are adapted from `bitwize-music-studio/claude-ai-music-skills` (CC0 1.0), and model/feature facts come from Suno's official release notes, blog and help centre, linked in `references/models-and-versions.md`. The Italian and Neapolitan material is original to this skill.*
