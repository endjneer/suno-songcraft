# Models and Versions Reference

Which model to use, what changed between versions, and what is gated behind a plan. Getting this wrong is expensive in a subtle way: a perfectly good prompt written for the wrong model reads as a prompting failure.

## Contents
- [Model timeline](#model-timeline)
- [Capability matrix](#capability-matrix)
- [How prompting differs by version](#how-prompting-differs-by-version)
- [Choosing a model](#choosing-a-model)
- [Personalization: Voices, Custom Models, Personas, My Taste](#personalization-voices-custom-models-personas-my-taste)
- [Feature timeline 2026](#feature-timeline-2026)
- [Plan gating](#plan-gating)
- [Sources](#sources)

---

## Model timeline

Suno's own timeline, with the parts that affect prompting.

| Model | Released | Max first generation | Headline change |
|---|---|---|---|
| V2 | Fall 2023 | 1:20 | — |
| V3 | Spring 2024 | 2:00 | — |
| V3.5 | Summer 2024 | 4:00 | Better song structure; extend up to 2 min per pass |
| V4 | Nov 2024 | 4:00 | Improved vocal quality; Extend, Cover, Persona |
| **V4.5** | May 1 2025 | **8:00** | Improved prompt adherence, smarter style mashups, longer style/lyrics fields |
| **V4.5+** | Jul 2025 | 8:00 | Add Vocals / Add Instrumental production tools |
| **V5** | Sep 23 2025 | 8:00 | Superior audio quality, authentic vocals, remastering |
| **v4.5-all** | Oct 21 2025 | 8:00 | V4.5 made free for everyone |
| **V5.5** | Mar 26 2026 | 8:00 | Richer arrangements, sharper vocals; Voices, Custom Models, My Taste |

Suno has said the current line is a bridge to industry-licensed models arriving later in 2026, and that these models are slated for deprecation when those land. Download WAVs of anything worth keeping.

---

## Capability matrix

| | V4.5 / v4.5-all | V4.5+ | V5 | V5.5 |
|---|---|---|---|---|
| Style Box cap | 1,000 | 1,000 | 1,000 | 1,000 |
| Lyrics Box cap | 5,000 | 5,000 | 5,000 | 5,000 |
| Max length | ~8 min | ~8 min | ~8 min | ~8 min |
| Creative sliders | ✅ | ✅ | ✅ | ✅ |
| Exclude Styles field | ✅ | ✅ | ✅ | ✅ |
| Prompt enhancement (Enhance button) | ✅ | ✅ | ✅ | ✅ |
| Add Vocals / Add Instrumental | — | ✅ | ✅ | ✅ |
| Remaster | — | — | ✅ | ✅ |
| **Duration slider** (web) | — | — | — | ✅ |
| **Voices** (voice capture) | — | — | — | ✅ |
| **Custom Models** | — | — | — | ✅ |
| Personas | ✅ | ✅ | ✅ | ✅ |

---

## How prompting differs by version

The shift across the line is from *keyword lists* to *briefs* and then back toward *restraint*.

**V4.5 opened the door to conversational style prompts.** Suno's own before/after in the help centre:

```
Before:  deep house, emotional, melodic

After:   Create a melodic, emotional deep house song with organic textures
         and hypnotic rhythms. Begin with soft ambient layers, natural
         sounds, and a deep, steady groove. Build gradually with flowing
         melodic synths, warm basslines, and intricate, subtle percussion
```

V4.5 also reads descriptive, non-technical phrasing — "uplifting nostalgic tones", "leaf textures", "melodic whistling" all influence the result. And it made the Lyrics Box carry more weight: Suno's guidance is to keep genre-level information in the Style field while adding song-level context directly in the Lyrics field.

**V5 listens more precisely and needs less instruction.** The same prompt that produced richness on V4.5 can produce clutter on V5, because V5 honours more of what you wrote. Suno's explicit advice is not to rerun old V4/V4.5 prompts on V5 — rewrite them shorter. This is where the synonym-pile problem bites hardest.

**V5.5 is V5's behaviour with richer arrangement and sharper vocals**, plus the personalization layer. Prompt it like V5. If a Voice or Custom Model is active, cut the parts of the style box those features already carry (see below).

**Practical rule:** V4.5 tolerates a paragraph. V5 and V5.5 reward a tight 100–400 characters where every term does distinct work.

---

## Choosing a model

| Situation | Model | Why |
|---|---|---|
| New work, paid plan | **V5.5** | Best arrangement and vocals; duration control; personalization |
| Free account | **v4.5-all** | The only current model available; still 1,000/5,000 field caps |
| Metal, hardcore, extreme genres | **V4.5**, tested against V5 | V5 can sound thin on heavy material; V4.5 sometimes wins outright |
| Adding vocals to an instrumental, or vice versa | **V4.5+** or later | Add Vocals / Add Instrumental |
| Fixing an old track's audio quality | **V5 / V5.5 Remaster** | Upgrades an earlier generation with a controllable variation amount |
| Exact target length | **V5.5 on web** | Only place the Duration slider exists |

If a user's output disappoints and they're on the free tier, say so plainly: they are on an older model line, and that alone explains a fair amount of the gap.

---

## Personalization: Voices, Custom Models, Personas, My Taste

All four change what the Style Box should contain. Putting a vocal description in the style box while a Voice is active makes the two fight.

| Feature | What it carries | Drop from the Style Box |
|---|---|---|
| **Voices** (V5.5) | A specific captured singing voice | Gender, range, and vocal-identity descriptors |
| **Custom Models** (V5.5) | Your production aesthetic, learned from your own uploaded tracks | Generic production language — "glossy", "polished mix", "modern pop production" |
| **Personas** (V4+) | Vocals, style and vibe of one past generation | Vocal identity; keep the style prompt to 1–2 genres plus instrumentation |
| **My Taste** (all tiers) | Learned genre/mood preferences | Nothing — it shapes the style *autogenerate* button, not explicit prompts |

**Voices**, in practice:
- Source audio can be a Suno song you made, a live microphone recording, or an upload — a cappella or full mix, since Suno stem-splits it automatically
- Supply 15 seconds to 4 minutes, then choose the best 2-minute segment
- Verification is mandatory: Suno shows a phrase to read aloud and matches the speech to the singing recording, to stop people cloning other people's voices
- 18+, geography-restricted in some regions, and you must confirm you hold the rights to the voice
- Voices are private to the account that created them
- Arrived on iOS and Android in Aug 2026; free plans have reduced functionality
- Keep **Audio Influence around 0.70–0.85** or the output drifts back toward a generic vocal

**Custom Models:** Pro and Premier only, up to three per account, tuned by uploading tracks from your own catalogue. Best for album-level consistency; switch back to stock V5.5 when you deliberately want something off-brand.

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
| Jul 20 2026 | **Duration slider on web** (V5.5) |
| Aug 7 2026 | **Voices on mobile** — record once, reuse on any song |

---

## Plan gating

Tiers move; verify against Suno's current pricing page before making a purchase recommendation. As of this writing:

| Capability | Free | Pro | Premier |
|---|---|---|---|
| v4.5-all | ✅ | ✅ | ✅ |
| V5 / V5.5 | — | ✅ | ✅ |
| Commercial use rights | ❌ **permanently, for anything generated on free** | ✅ | ✅ |
| Custom Models (up to 3) | — | ✅ | ✅ |
| Voices | limited | ✅ | ✅ |
| Sounds | — | ✅ | ✅ |
| Advanced Split stems | — | — | ✅ |
| Suno Studio | — | — | ✅ |

The free-tier commercial restriction does not clear retroactively. A track made on a free account stays non-commercial even after upgrading — anything intended for release has to be generated on a paid plan from the start.

---

## Sources

Official, and worth re-checking when something here looks stale:

- Model timeline — https://help.suno.com/en/articles/5782721
- What's new in V4.5 — https://help.suno.com/en/articles/5782593
- Detailed style instructions (V4.5) — https://help.suno.com/en/articles/5782849
- Better prompts in lyrics (V4.5) — https://help.suno.com/en/articles/5782977
- Creative sliders — https://help.suno.com/en/articles/6141377
- What's new in V5.5 — https://help.suno.com/en/articles/11362305
- Voices — https://help.suno.com/en/articles/11362369
- Personas — https://help.suno.com/en/articles/3484161
- Music glossary — https://help.suno.com/en/articles/9010177
- Release notes — https://suno.com/release-notes
- V5.5 announcement — https://suno.com/blog/v5-5
- V4.5 announcement — https://suno.com/blog/introducing-v4-5
