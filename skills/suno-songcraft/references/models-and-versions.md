# Models and Versions Reference

Which model to use, what changed between versions, and what is gated behind a plan. Getting this wrong is expensive in a subtle way: a perfectly good prompt written for the wrong model reads as a prompting failure.

## Contents
- [The v6 family](#the-v6-family)
- [Capability matrix](#capability-matrix)
- [Migrating from v5.5 to v6](#migrating-from-v55-to-v6)
- [Choosing a model](#choosing-a-model)
- [Personalization: Voices, Custom Models, Personas, My Taste](#personalization-voices-custom-models-personas-my-taste)
- [Feature timeline 2026](#feature-timeline-2026)
- [Plan gating](#plan-gating)
- [Retired models (history)](#retired-models-history)
- [Sources](#sources)

---

## The v6 family

Released **Sep 9 2026**, developed with WMG, BMG and Believe. Three models:

| Model | Plans | What it's for |
|---|---|---|
| **v6** | Pro, Premier | The precise, reliable model — "when you know what you want" |
| **v6-wild** | Pro, Premier | Unexpected choices and genre-blending; moves away from the prompt by design. A take that works can be brought into v6 to refine it |
| **v6-mini** | All plans (the Free plan's model) | Quick ideas, high-volume generation, concept tests |

Every model before v6 (v4, v4.5, v4.5+, v5, v5.5) is retired for new generations. Old songs stay in the library and can still be played, shared, remastered and covered, but every new iteration runs on v6. See [Retired models](#retired-models-history) for what came before.

---

## Capability matrix

Per model:

| | v6 | v6-wild | v6-mini |
|---|---|---|---|
| Plans | Pro, Premier | Pro, Premier | All |
| Max length per generation | 8 min | 8 min | 8 min |
| Standard generation | 10 credits, 2 songs | 10 credits, 2 songs | 10 credits, 2 songs |

Max Mode and prompts with many images or videos cost more than a standard generation.

Across the family:

| Feature | Status on v6 |
|---|---|
| Style Box cap | 1,000 chars (Suno API limit) |
| Lyrics Box cap | 5,000 chars (Suno API limit) |
| Simple mode description cap | 3,000 chars (Suno API limit) |
| Title cap | 100 chars — v5-era figure, unverified on v6 |
| **Variety** slider | ✅ New. Off / Normal / High / Extra / Max (API 0–4); reinterprets the style prompt before generating |
| Weirdness, Style Influence, Audio Influence | ✅ (API `controls.*`; Audio Influence only with a Voice) |
| Exclude Styles | ✅ (API `negative_style`) |
| **Max Mode** | ✅ New. Optional, costs a multiple of the credits |
| **Simple mode** with multiple inputs | ✅ Suno songs, playlists, uploaded audio, images, video in one prompt; picks Cover, Remix or Extend itself |
| **Plain-language edits** | ✅ One section or one word of an existing song |
| Remix & Edit | ✅ Extend, Cover, Replace Section and more |
| Remaster | ✅ Songs made with retired models stay remasterable; the result runs on v6 |
| Add Vocals | ✅ Documented, Pro/Premier, beta |
| Add Instrumental | Unverified on v6 |
| Prompt enhancement (Enhance button) | Unverified on v6 |
| Duration slider | Announced for V5.5 on web — verify in-app on v6. API `duration`: 15–360 s, a target |
| Voices, My Taste | ✅ |
| Custom Models | ✅ Fine-tuning now runs on v6 |
| Personas | Unverified on v6 |
| Suno Sounds | ✅ Sound effects, one-shots and loops, tempo, key and looping settable (Pro and up) |
| Artist-name blocking | ✅ Still enforced; v6 also screens uploaded audio and lyrics for unauthorized use |

---

## Migrating from v5.5 to v6

A prompt and slider set tuned on v5.5 is a starting point on v6, not a known result. Don't port it blind:

1. **Regenerate it on v6 with Variety Off.** Variety is the one new control that silently changes what a ported prompt does — left on, Suno rewrites your style tags before generating.
2. **Compare against the v5.5 take**, which is still in the library. Listen for the same things you'd diagnose on a new track: genre, vocal character, mix balance.
3. **Change one thing at a time** from there, with the model held fixed. The descriptor discipline in `style-box.md` still holds on v6.
4. **Recheck any Custom Model** before trusting it — existing ones were moved to v6 automatically (see below).

Suno's v6 FAQ links a tutorial on getting closer to the results of past models.

---

## Choosing a model

| Situation | Model | Why |
|---|---|---|
| Deliberately built prompt, paid plan | **v6** | The precise, reliable model |
| Looking for ideas, genre-blends, a surprise | **v6-wild**, then refine the keeper in **v6** | Moves away from the prompt by design |
| Free account | **v6-mini** | The only model on Free |
| Quick concept tests, high-volume drafts | **v6-mini** | Built for fast ideas and volume |
| Adding vocals to an instrumental | **Add Vocals** (Pro/Premier, beta) | Add Instrumental: unverified on v6 |
| Updating a song made with a retired model | **Remaster** or **Cover** | Old songs stay remasterable and coverable; the result runs on v6 |
| Song over ~2 min, faithful cover, style transfer, voice and style consistency | Any, with **Max Mode** | Suno's own recommendation for Max Mode |
| Exact target length | Section count; the Duration slider if it shows in-app on v6 | API `duration` is a target, not a guarantee |

If a Free user's output disappoints, say so plainly: v6-mini is the model for quick ideas and concept tests, and v6, the precise one, needs Pro or Premier.

---

## Personalization: Voices, Custom Models, Personas, My Taste

All four change what the Style Box should contain. Putting a vocal description in the style box while a Voice is active makes the two fight. Voices, Custom Models and My Taste work on v6; Personas are unverified on v6.

| Feature | What it carries | Drop from the Style Box |
|---|---|---|
| **Voices** | A specific captured singing voice | Gender, range, and vocal-identity descriptors |
| **Custom Models** (fine-tuned on v6) | Your production aesthetic, learned from your own uploaded tracks | Generic production language — "glossy", "polished mix", "modern pop production" |
| **Personas** (V4+; unverified on v6) | Vocals, style and vibe of one past generation | Vocal identity; keep the style prompt to 1–2 genres plus instrumentation |
| **My Taste** (all tiers) | Learned genre/mood preferences | Nothing — it shapes the style *autogenerate* button, not explicit prompts |

**Voices**, in practice:
- Source audio can be a Suno song you made, a live microphone recording, or an upload — a cappella or full mix, since Suno stem-splits it automatically
- Supply 15 seconds to 4 minutes, then choose the best 2-minute segment
- Verification is mandatory: Suno shows a phrase to read aloud and matches the speech to the singing recording, to stop people cloning other people's voices
- 18+, geography-restricted in some regions, and you must confirm you hold the rights to the voice
- Voices are private to the account that created them
- Arrived on iOS and Android in Aug 2026; free plans have reduced functionality
- Keep **Audio Influence around 0.70–0.85** or the output drifts back toward a generic vocal

**Custom Models:** Pro and Premier only, up to three per account, tuned by uploading tracks from your own catalogue. Best for album-level consistency; switch back to stock v6 when you deliberately want something off-brand.

Existing Custom Models were moved to v6 automatically, and songs made with their v5.5 version stay as they were. A model that sounded right on v5.5 can sound different now: **regenerate a known reference song through it before relying on it.**

Voice + Persona together is redundant — pick one.

---

## Feature timeline 2026

Useful when a user describes a feature that doesn't match what you expect, or asks whether something exists yet.

| Date | Feature |
|---|---|
| Jan 27 2026 | **Sounds** — generate one-shot samples and loops from scratch (Pro/Premier) |
| Feb 16 2026 | **Studio 1.2** — Remove FX, Warp Markers, time signatures beyond 4/4, Alternates |
| Mar 26 2026 | **V5.5** — Voices, Custom Models, My Taste |
| May 13 2026 | CarPlay / Android Auto |
| Jun 11 2026 | **Stem separation overhaul** — Auto Split (12 stems), Split from Mix, Advanced Split (~100 instruments) |
| Jul 9 2026 | **Lyrics editor on web** — full-screen editing, autosave, structure labels, natural-language edits ("make this line funnier"), variation suggestions, saved lyricist examples |
| Jul 15 2026 | iMessage integration |
| Jul 20 2026 | **Duration slider on web** (V5.5; verify in-app on v6) |
| Aug 7 2026 | **Voices on mobile** — record once, reuse on any song |
| Aug 13 2026 | **Studio 2.0** (Premier) — MIDI, recording, automation, effects and plugins built through chat, wavetable synth, Split from Mix / Advanced Split inside the session, unlimited 32-bit/48 kHz multitrack and stem exports |
| Sep 3 2026 | **Terms update** — download caps per plan (see [Plan gating](#plan-gating)) |
| Sep 9 2026 | **v6, v6-wild, v6-mini** — Variety, Max Mode, multi-input Simple mode, plain-language edits; all earlier models retired for new generations |

---

## Plan gating

Tiers move; verify against Suno's current pricing page before making a purchase recommendation. As of this writing:

| Capability | Free | Pro | Premier |
|---|---|---|---|
| v6-mini | ✅ | ✅ | ✅ |
| v6 / v6-wild | — | ✅ | ✅ |
| Commercial use rights | ❌ **permanently, for anything generated on free** | ✅ | ✅ |
| Downloads | 7 trial downloads in total, personal use only | 20 / month | 60 / month, plus unlimited Studio exports |
| Custom Models (up to 3) | — | ✅ | ✅ |
| Voices | limited | ✅ | ✅ |
| Add Vocals (beta) | — | ✅ | ✅ |
| Sounds | — | ✅ | ✅ |
| Advanced Split stems | — | — | ✅ |
| Suno Studio 2.0 | — | — | ✅ |

The free-tier commercial restriction does not clear retroactively. A track made on a free account stays non-commercial even after upgrading — anything intended for release has to be generated on a paid plan from the start.

**Downloads** (Terms in force since Sep 3 2026): extra downloads can be bought, and the caps also apply to songs created before Sep 3. Songs downloaded on a paid plan stay commercially usable. Download keepers, not every take; on Premier, export finals and stems through Studio, which is unlimited on top of the 60.

---

## Retired models (history)

None of these runs new generations since Sep 9 2026. Kept so that older prompts, songs and advice can be placed in context.

| Model | Released | Max first generation | Headline change |
|---|---|---|---|
| V2 | Fall 2023 | 1:20 | — |
| V3 | Spring 2024 | 2:00 | — |
| V3.5 | Summer 2024 | 4:00 | Better song structure; extend up to 2 min per pass |
| V4 | Nov 2024 | 4:00 | Improved vocal quality; Extend, Cover, Persona |
| V4.5 | May 1 2025 | 8:00 | Improved prompt adherence, smarter style mashups, longer style/lyrics fields (1,000 / 5,000; 200 / 3,000 before) |
| V4.5+ | Jul 2025 | 8:00 | Add Vocals / Add Instrumental production tools |
| V5 | Sep 23 2025 | 8:00 | Superior audio quality, authentic vocals, remastering |
| v4.5-all | Oct 21 2025 | 8:00 | V4.5 made free for everyone |
| V5.5 | Mar 26 2026 | 8:00 | Richer arrangements, sharper vocals; Voices, Custom Models, My Taste; Duration slider on web from Jul 2026 |

Suno had said this line was a bridge to industry-licensed models, slated for deprecation when those landed. That happened with v6.

**How prompting shifted across the retired line.** V4.5 opened the door to conversational style prompts — Suno's own before/after went from `deep house, emotional, melodic` to a narrated production brief — and read descriptive, non-technical phrasing. V5 listened more precisely and needed less instruction: the same prompt that produced richness on V4.5 could produce clutter on V5, and Suno advised against rerunning V4/V4.5 prompts on V5 without rewriting them. V5.5 kept V5's behaviour with richer arrangement and the personalization layer. For moving prompts onto v6, see [Migrating from v5.5 to v6](#migrating-from-v55-to-v6).

---

## Sources

Official, and worth re-checking when something here looks stale.

**v6 family:**

- Introducing v6 — https://suno.com/blog/introducing-v6
- v6 FAQ (retirement, Variety, Max Mode, Custom Models) — https://help.suno.com/en/articles/13924481
- What's new in v6 — https://help.suno.com/en/articles/13924801
- Current models: v6 — https://help.suno.com/en/articles/13924737
- Terms update and download caps — https://suno.com/blog/suno-updates-tos
- Studio 2.0 — https://about.suno.com/blog/studio-2
- Add Vocals — https://help.suno.com/en/articles/6882817

**General:**

- Creative sliders — https://help.suno.com/en/articles/6141377
- Voices — https://help.suno.com/en/articles/11362369
- Personas — https://help.suno.com/en/articles/3484161
- Music glossary — https://help.suno.com/en/articles/9010177
- Release notes — https://suno.com/release-notes

**Retired models (history):**

- Model timeline — https://help.suno.com/en/articles/5782721
- What's new in V4.5 — https://help.suno.com/en/articles/5782593
- Detailed style instructions (V4.5) — https://help.suno.com/en/articles/5782849
- Better prompts in lyrics (V4.5) — https://help.suno.com/en/articles/5782977
- What's new in V5.5 — https://help.suno.com/en/articles/11362305
- V5.5 announcement — https://suno.com/blog/v5-5
- V4.5 announcement — https://suno.com/blog/introducing-v4-5
