# Suno Connector Reference

When Claude has Suno's connector (tools such as `audio-create`, `audio-analysis`, `audio-listen`), this skill can go past paste-ready fields: generate the song, measure what came back, and fix one thing at a time with evidence instead of guesses.

The connector's own tool descriptions already cover parameters, errors and spending rules, and Claude reads them when it calls a tool. This file covers only the decisions that interact with the rest of the skill: which values to send, the traps that undo its advice, and how to check a take.

## Contents
- [Before generating](#before-generating)
- [From skill fields to connector fields](#from-skill-fields-to-connector-fields)
- [Traps that undo this skill's advice](#traps-that-undo-this-skills-advice)
- [Measure, then fix](#measure-then-fix)
- [Voices and Sounds](#voices-and-sounds)

---

## Before generating

**Read `account-usage` first.** It is free and answers the questions that decide the call:

| Field | What it tells you |
|---|---|
| `allowed_models` | The labels you may pass as `model`: `v6`, `v6-wild`, `v6-mini`, depending on the plan |
| `features` | Whether the plan has `controls.advanced` (sliders, `negative_style`, `vocal_gender`), `generate.custom`, `generate.cover`, `generate.extend`, `voices` |
| `suno_account.credits_remaining` | Song-generation credits left |
| `suno_account.download_credits_remaining` | Downloads left this period |

**Generating spends the user's credits. Ask first.** Show the fields in the skill's output format, say which model and roughly what it costs (a standard generation is 10 credits for 2 songs; Max Mode costs a multiple), and wait for a yes before the first `audio-create` and before each new round. Reading, analysing, aligning, listening and joining extensions are free.

**Custom mode is this skill's mode.** Send `style` + `lyrics` + `title`. Simple mode (`description`, up to 3,000 chars, optionally with up to 10 of the user's songs in `reference_audio_ids`, named by title in the description, never by id) cannot be mixed with `style` or `lyrics` in the same call: that returns an error.

---

## From skill fields to connector fields

| Skill output | Connector field | Note |
|---|---|---|
| Style Box | `style` (≤ 1,000) | |
| Lyrics Box | `lyrics` (≤ 5,000) | |
| Title | `title` (≤ 256) | The API takes 256; the 100-char in-app figure is from the v5 era |
| Exclude Styles | `negative_style` (≤ 1,000) | Needs `controls.advanced`; only with your own `style` |
| Variety Off | `controls.variety: 0` | **Send it explicitly** — see the first trap below |
| Weirdness / Style Influence | `controls.weirdness` / `controls.style_influence`, 0–1 | Same scale as the bands in `genre-playbook.md`. Omit to keep the model's default; `0` is a real value, not "unset" |
| Audio Influence | `controls.audio_influence`, 0–1 | In `audio-create` only alongside a `voice_id`; in covers, extensions and mashups it sets closeness to the source |
| Voice Gender | `vocal_gender`: `male` / `female` | Needs `controls.advanced`; a `voice_id` overrides it |
| Instrumental | `instrumental: true` | A `voice_id` always sings and overrides it |
| Model | `model`: `v6`, `v6-wild` or `v6-mini` | **Send it every time:** omitted, Suno uses the plan's default, which isn't necessarily `v6`. Must be in `allowed_models` |
| Max Mode | `max_mode` | Only when the user asks for it by name, and only on the songs they name |
| Duration | `duration`, 15–360 s | See the second trap below |

**On a plan without `controls.advanced`,** sliders, `negative_style` and `vocal_gender` are refused. Drop them, move the exclusions into the style box as `no …` (the inline fallback in `style-box.md`), and tell the user the sliders stayed at the model's defaults.

---

## Traps that undo this skill's advice

**1. Omitting Variety is not the same as Off.** Omitted, every slider takes the model's own default, and nothing guarantees Variety's default is Off. Since every style box this skill writes assumes Variety Off, send `controls.variety: 0` on every call — create, cover, extension, mashup — unless the user wants Suno to reinterpret the style.

**2. `duration` cuts songs off.** When `duration` is set, `duration_strict` turns on by default: generation is hard-capped at the target, and a song that would run longer is truncated and ends abruptly, with no outro. Custom lyrics are never shortened to fit (`duration_guidance` only resizes lyrics Suno writes itself). With this skill's lyrics, either:
- leave `duration` out and let the section count set the length (the table in SKILL.md), or
- set it with `duration_strict: false`, so it is a soft target.

**3. Covers drop the lyrics.** A cover does not carry the source's words over: without `lyrics` it comes out instrumental (unless a `voice_id` sings). To keep the vocals, pass the source's lyrics — `audio-retrieve` returns them as `metadata.lyrics` for the user's own songs. And pass `duration` equal to the source's length: in one field test, a 5:36 source covered without it came back at 4:27–4:54, with the intro shortened. (Covers take `duration` only; `duration_strict` belongs to `audio-create`.)

**4. Extensions are only the new part.** `audio-extensions-create` returns just the continuation from `continue_at`; join the chain with `audio-full-song`, which is free. The extension advice in `sliders-and-iteration.md` still holds: write the new section's lyrics explicitly and keep extends to 2–3 per song.

**5. `audio-edit` doesn't touch the audio.** It changes the title and lyrics text stored with a library song. The plain-language audio edits ("Change the chorus so it's sung by a gospel choir") are not exposed by the connector: send the user to Remix & Edit in the Suno app for those.

**6. Downloads can spend a download credit.** Call `audio-download` without `confirm` first; if it answers `requires_credit`, ask before confirming. Download keepers, not every take.

---

## Measure, then fix

Without the connector, diagnosis is by ear. With it, check the take first, then apply `troubleshooting.md`. After `audio-wait` (pass every id in `clip_ids` together), run these. All four are free.

**1. Did Variety rewrite the style?** `audio-retrieve` (or `library-list`) shows the style the clip was made with as `metadata.style`. If it differs from the `style` you sent, Variety rewrote it: resend with `variety: 0`. Whether `metadata.style` always shows the rewritten version is unverified, so if it matches but the sound ignores the tags, go on to the checks below.

**2. `audio-analysis`: does it match the brief?** It reports `bpm`, `key`, `time_signature`, the structural sections, and `terms` / `labels` describing the voice, instruments, genre, mood and mix polish as a tagging model hears them, not as the prompt claimed.

| Finding | It's a… | Move |
|---|---|---|
| BPM far from the one asked for | prompt | State the BPM explicitly; check the genre implies that tempo |
| Genre or instruments missing from the labels | prompt | Sharpen the genre tag; name 2–4 instruments |
| Fewer sections than the lyrics tagged | lyrics | Too long; cut toward ~3,000 chars |
| Labels right, but generic | slider | Weirdness up **or** Style Influence down, one at a time |

Sections that share a label repeat the same material, so a recurring label is usually the chorus. That shows whether the chorus actually came back.

**3. `audio-lyrics-alignment`: were the words sung?** It returns each word with the span of audio it is sung over. Words it could not place carry `success: false`, and a cluster of them marks a line that was skipped, rushed or mangled. That is where to listen first. It aligns the lyric text rather than transcribing the audio, so it locates problems; it doesn't hear substitutions. For Italian and Neapolitan, those clusters are where to check final vowels and doubled consonants.

**4. `audio-listen`: ask what the measurements can't answer.** Suno's music agent listens and replies in text; ask for JSON with named fields to get data back. Aim the questions at the known failure modes:

```
Is the lead vocal clearly above the band? Is the top end bright or
muffled? Are there backing vocals or a choir? Are the Italian final
vowels fully articulated? End with a JSON block with fields
vocal_level (buried|balanced|upfront), top_end (dull|neutral|bright),
backing_vocals (none|some|heavy), final_vowels (clear|swallowed|mixed).
```

It is a model's judgment, not a measurement: use it to decide where to listen and confirm by ear before acting on it. Field use has shown its limits: it hears one track at a time and can't compare melodies across files, its timestamps are approximate, its prose and its JSON sometimes disagree, it misjudges repetitiveness, and it transcribes Neapolitan poorly — so for dialect diction, trust your ear over its answer. Use it to rule out obvious problems, not to pick the best take. It never names real artists or recordings, which fits the blocklist rule. Up to five questions can be open at once, 200 a day.

**Then fix one thing.** Map the finding to the quick lookup table in `troubleshooting.md`, change one variable, and regenerate after the user's go-ahead. Log each round: clip ids, model, the fields and controls sent, and what the four checks said. A log of measured attempts is what turns a lucky take into a repeatable recipe.

---

## Voices and Sounds

- **Voices:** `voices-list` gives the user's voices; pass one as `voice_id`. Drop the vocal-identity block from the style box, and keep `audio_influence` around 0.70–0.85 (see `style-box.md`).
- **Out of scope here:** stitching sections from different takes, final renders and mastering. For loudness targets see `sliders-and-iteration.md`.
- **Sounds:** for a sound effect, one-shot or loop on its own, `sounds-create` makes two per request at 1 credit each (Pro and up), with `loop`, `tempo` and `key` settable. Use it instead of trying to get the effect out of lyrics-box SFX tags in a song generation.
