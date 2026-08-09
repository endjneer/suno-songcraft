# Neapolitan Reference

Neapolitan is a language, not an Italian accent — it has its own phonology, its own orthography and a thousand-year song tradition. Treating it as "Italian with a Naples voice" is the single most common reason a Neapolitan generation sounds wrong to anyone from Campania.

It is also the hardest thing in this skill to get out of Suno, because the training data is thin and the written conventions are inconsistent even among native writers. Everything here is about giving the model something stable to hold on to.

Read this alongside `italian-language.md` — the fix hierarchy, the geminate rules and the pronunciation-notes workflow are shared and not repeated here.

## Contents
- [Set expectations first](#set-expectations-first)
- [The three anchors](#the-three-anchors)
- [The schwa](#the-schwa)
- [Sound changes from Italian](#sound-changes-from-italian)
- [Articles, apostrophes and aphaeresis](#articles-apostrophes-and-aphaeresis)
- [Metaphony](#metaphony)
- [Syntactic doubling](#syntactic-doubling)
- [Respelling table](#respelling-table)
- [Traditions and eras](#traditions-and-eras)
- [Instruments and rhythms](#instruments-and-rhythms)
- [Style box templates](#style-box-templates)
- [When it will not work](#when-it-will-not-work)

---

## Set expectations first

Say this to the user before generating, because it saves credits and disappointment: Suno's Neapolitan is an **approximation**. It gets the melodic tradition and the instruments convincingly right; it gets the language partly right, and a native speaker will hear the seams.

Two workable strategies, and it's worth choosing explicitly:

**Authentic orthography.** Write in Neapolitan as it is actually written (`'O sole mio`, `chiù`, `quanno`). Best when the text matters and the listener knows the language. Requires heavy respelling and more takes.

**Phonetic Italian.** Write the Neapolitan *sounds* using Italian spelling conventions the model reads more reliably (`o sole mio`, `chiu`, `quanno` without the apostrophes and with vowels spelled out). Less faithful on the page, often closer in the audio. Best for a chorus that has to land.

For most tracks the answer is: authentic orthography in the lyric you keep, phonetic Italian in the box you paste into Suno. They don't have to be the same document.

---

## The three anchors

**1. Style Box** — in English, as always:
```
Neapolitan tenor, operatic vibrato, melismatic, full chest voice, sung in
Neapolitan with native Campanian diction.
```
`sung in Neapolitan` alone often reads as "Italian". Adding `Campanian diction` or `Southern Italian diction` measurably improves the odds.

**2. Exclusions**:
```
EXCLUDE STYLES: no standard Italian pronunciation, no English vocals
```

**3. Section isolation.** Never mix Neapolitan and Italian inside one section — the pronunciation drifts across the whole section, not just the mixed line. A bilingual track wants `[Verse 1 - Neapolitan]` and `[Chorus - Italian]` as separate blocks, with `bilingual, Neapolitan verses, Italian chorus` in the style box.

---

## The schwa

This is the defining trait and the exact inverse of Italian. In Italian every final vowel is fully articulated; in Neapolitan **unstressed vowels, especially final ones, reduce to a schwa** — the neutral *uh* sound. *Guaglione* ends on a murmur, not on a clear **e**. *Napule* is roughly `NA-pu-lə`.

The good news: an English-weighted model reduces final vowels by default, so for once the model's instinct is right. The problem is written, not acoustic — if you spell the vowel clearly, Suno may over-articulate it back into Italian.

**Practical approach:**
- Do **not** hyphenate or capitalise final vowels in Neapolitan the way you would in Italian. Leave them alone and let the reduction happen.
- Never write `ə` in the lyrics box — it is not read reliably.
- Where a final vowel is being over-pronounced and it matters, drop it and apostrophise: `bell'`, `chell'`, `nun c' sta`. This is legitimate Neapolitan orthography, not a hack.
- Put stressed syllables on the strong beats and let the unstressed ones fall between — the melody does more of this work than the spelling.

---

## Sound changes from Italian

These are regular. Knowing them lets you convert any Italian line into credible Neapolitan and, just as usefully, spot when Suno has silently reverted to Italian.

| Change | Italian | Neapolitan | Note |
|---|---|---|---|
| `-nd-` → `-nn-` | quando, mondo | **quanno**, **munno** | Very high frequency; the clearest single marker |
| `-mb-` → `-mm-` | piombo, gamba | **chiummo**, **gamma** | |
| `pl-` → `chi-` | più, piove, pieno | **chiù**, **chiove**, **chino** | `chiù` is everywhere in song |
| `fl-` → `sci-` | fiore, fiume | **sciore**, **sciummo** | |
| intervocalic `d` → `r` | Madonna, dodici | **Maronna**, **ruricce** | Rhotacism |
| initial `b` → `v` | bocca, barca, bene | **vocca**, **varca**, **bbene** | |
| `s` + consonant → *sh* | stella, spera, scarpa | *shtella, shpera, shcarpa* | **Not written this way** — see below |
| final consonants | — | dropped | `nun` for *non* |

**The *sh* is the most Neapolitan sound there is** and the one Suno most reliably misses. *S* before a consonant is pronounced like English *sh*: `stella` is closer to *shtella*. Neapolitan orthography does **not** write this — but the Suno lyrics box is not orthography, it's an instruction. For the two or three words per song where this sound carries the identity, respell it phonetically:

```
Written (keep in your lyric)     Pasted into Suno
stella                        →  shtella
spusarizio                    →  shpusarizio
'nu sciore                    →  'nu shore
```

Do this selectively. A whole lyric respelled this way reads as noise and the model starts mispronouncing things that were fine.

---

## Articles, apostrophes and aphaeresis

Neapolitan drops initial vowels, and the apostrophe that marks the loss is everywhere. Suno tends to read a leading apostrophe as a pause or a glottal break, splitting one sung word into two.

| Neapolitan | Italian | Risk | Paste as |
|---|---|---|---|
| `'o` | il, lo | read as a break | `o` |
| `'a` | la | read as a break | `a` |
| `'e` | i, le | read as a break | `e` |
| `'nu`, `'na` | un, una | read as a break | `nu`, `na` |
| `'ncoppa` | sopra | broken into two | `ncoppa` |
| `'mmiez'` | in mezzo | broken into two | `mmiezo` |

The rule of thumb: **keep the apostrophes in the lyric you're writing, strip them in the text you paste.** They carry no sound and cost you syllables.

A trailing apostrophe (`bell'`, `chell'`, `sti'`) is different — that one is doing useful work, marking the dropped vowel you *want* dropped. Keep it.

---

## Metaphony

Neapolitan raises a stressed vowel depending on the original final vowel, which is how the language marks gender and number where the endings have collapsed into schwa. It is why *russo* (red, masculine) and *rossa* (red, feminine) differ in the stressed vowel and not just the ending.

| Neapolitan | Meaning |
|---|---|
| `chisto` / `chesta` | this (m.) / this (f.) |
| `russo` / `rossa` | red (m.) / red (f.) |
| `nuosto` / `nosta` | our (m.) / our (f.) |
| `buono` / `bona` | good (m.) / good (f.) |

You don't need to explain this to Suno — you need to **not correct it**. If you write *chisto* where the grammar wants it, leave it; the instinct to "fix" it toward Italian *questo* is what makes a lyric read as translated.

---

## Syntactic doubling

Certain words double the initial consonant of the word that follows: `a ccasa`, `e ppo'`, `cchiù`, `nun ce sta` → `nun cce sta`. It is written in careful Neapolitan and it is audible.

Keep it. It also helps you: a doubled consonant is one of the few spellings Suno reliably articulates, so it reinforces the geminate rather than fighting it.

---

## Respelling table

The words that appear in almost every Neapolitan lyric, with the form to paste.

| Written | Meaning | Paste as | Why |
|---|---|---|---|
| `'o sole` | the sun | `o sole` | leading apostrophe read as a break |
| `'a luna` | the moon | `a luna` | same |
| `chiù` | more | `chiu` | accent unstable, sound is simple |
| `quanno` | when | `quanno` | fine as written — keep the `nn` |
| `munno` | world | `munno` | fine as written |
| `sciore` | flower | `shore` | `sci` reads as *sky* without help |
| `guaglione` | boy, kid | `gwa-LYO-ne` | `gli`-type palatal + stress |
| `Maronna` | Madonna | `ma-RON-na` | geminate + stress |
| `vocca` | mouth | `vocca` | fine as written |
| `napulitano` | Neapolitan | `napuli-TA-no` | long word, stress drifts |
| `Napule` | Naples | `NA-pu-le` | stress falls back otherwise |
| `core` | heart | `CO-re` | very frequent, always stressed |
| `'ncoppa` | on, above | `ncoppa` | apostrophe |
| `mmiez'` | amid | `mmiezo` | apostrophe + dropped vowel |
| `nun` | not | `nun` | fine as written |
| `pecché` | why, because | `pec-CHÉ` | final stress drops otherwise |
| `stella` | star | `shtella` | the *sh* — use only if it carries the line |
| `accussì` | like this | `accus-SÌ` | final stress |
| `t'aggia` | I have to (you) | `taggia` | apostrophe |
| `songo` | I am / they are | `songo` | fine as written |

---

## Traditions and eras

Naming the era does more for the arrangement than any list of instruments, because each one implies a whole production world.

| Tradition | Period | What it sounds like |
|---|---|---|
| **Villanella** | 1500s–1700s | Three or four unaccompanied voices, modal, plain; occasional lute |
| **Canzone classica** | 1880–1950 | The Piedigrotta repertoire: tenor, mandolin, strings, through-composed melody |
| **Sceneggiata** | 1920s–1970s | Sung melodrama, spoken interludes, heightened emotion, small orchestra |
| **Canzone d'autore napoletana** | 1970s–1980s | Neapolitan Power: blues, jazz and Mediterranean fusion, electric band, husky vocal |
| **Neomelodico** | 1980s–now | Synth strings, programmed drums, huge compressed vocal, melismatic tenor |
| **Musica popolare / tammurriata** | revival, 1970s–now | Tammorra-driven, raw open-throated group vocals, modal, hypnotic |
| **Rap e trap napoletana** | 2010s–now | Trap production with Neapolitan flow; the language survives in the cadence more than the vocabulary |

The two that Suno handles best are **canzone classica** and **neomelodico** — the first because its instrumentation is distinctive and well represented, the second because its production is modern and generic. Tammurriata is the hardest.

---

## Instruments and rhythms

Name the technique, not just the instrument. `mandolin` gives you a generic plucked string; `mandolin tremolo` gives you Naples.

**Strings and keys:** `mandolin tremolo`, `Neapolitan mandola`, `chitarra battente`, `nylon-string guitar`, `diatonic accordion`, `organetto`

**Percussion:** `tammorra frame drum`, `putipù friction drum`, `triccheballacche clappers`, `castanets`, `tambourine ostinato`

**Winds:** `ciaramella`, `zampogna` (Christmas repertoire), `clarinet`, `muted trumpet`

**Rhythms:**

| Rhythm | Metre | Style box phrasing |
|---|---|---|
| Tarantella napoletana | 6/8, fast | `fast 6/8 tarantella, driving tambourine` |
| Tammurriata | 2/4 or 4/4 | `tammurriata, tammorra ostinato, hypnotic repetition` |
| Canzone / romanza | 4/4 or 3/4, slow | `slow 4/4 romanza, rubato phrasing` |

Compound metres flatten toward 4/4 if Weirdness is high. For tarantella and tammurriata keep Weirdness low and Style Influence high, and restate the rhythm as an ostinato rather than a genre name.

---

## Style box templates

### Canzone napoletana classica
`60–90 BPM` · W `0.15–0.35` · SI `0.65–0.85`
```
Neapolitan tenor, operatic vibrato, melismatic, full chest voice, sung in
Neapolitan with native Campanian diction. Classic canzone napoletana,
mandolin tremolo, nylon-string guitar, lush string section, harp.
72 BPM, warm vintage mix, natural hall, vocal front and centre.
```

### Neomelodico
`80–105 BPM` · W `0.15–0.35` · SI `0.60–0.80`
```
Neapolitan male tenor, heavy vibrato, emotional belt, melismatic runs, sung in
Neapolitan. Neomelodico, synth strings, programmed drums, electric piano,
mandolin accents. 92 BPM, glossy modern mix, vocal loud and compressed,
big reverb.
```

### Neapolitan Power / fusione mediterranea
`85–110 BPM` · W `0.30–0.50` · SI `0.50–0.70`
```
Neapolitan male vocal, husky and soulful, conversational phrasing, sung in
Neapolitan. Mediterranean blues fusion, nylon and electric guitar, Fender
Rhodes, fretless bass, saxophone, Latin percussion. 96 BPM, warm analog
production, live band feel.
```

### Tammurriata
`100–130 BPM` · W `0.15–0.35` · SI `0.70–0.85`
```
Group vocals, raw open-throated call and response, ornamented, sung in
Neapolitan. Tammurriata, tammorra frame drum ostinato, putipù, castanets,
chitarra battente. 116 BPM, modal and hypnotic, live outdoor recording,
voices close and unpolished.
```

### Sceneggiata
`65–95 BPM` · W `0.20–0.40` · SI `0.60–0.80`
```
Neapolitan tenor, theatrical and declamatory, spoken interludes between sung
lines, sung in Neapolitan. Sceneggiata melodrama, small orchestra, mandolin,
dramatic strings, accordion. 80 BPM, vintage recording, heavy dynamic contrast.
```
*(Use `[Verse - Spoken]` for the recitative sections. This is one of the few genres where a spoken tag is structural rather than decorative.)*

### Rap napoletano
`85–140 BPM` · W `0.20–0.40` · SI `0.55–0.75`
```
Neapolitan male rap flow, clipped southern cadence, rapped in Neapolitan.
Boom bap with Mediterranean sample, filtered mandolin loop, dusty drums,
upright bass. 92 BPM, underground mix, vocal dry and centred.
```

---

## When it will not work

Reach for a different approach when you hit these, rather than burning takes.

- **Long stretches of dense dialect.** Suno degrades as the proportion of unfamiliar tokens rises. A Neapolitan chorus over Italian verses works far better than a fully Neapolitan lyric, and it's a legitimate form in its own right.
- **Tammurriata rhythm** collapsing to 4/4 after three or four takes means the metre isn't landing. Switch to describing it as a percussion ostinato and accept the 4/4, or go instrumental and layer a real tammorra yourself.
- **The *sh* sound** never arriving. It's the least reproducible feature. Respell the two most important words and let the rest go.
- **Neapolitan proper nouns and toponyms** — *Mergellina*, *Spaccanapoli*, *Marechiaro* — are rare tokens and get mangled. Respell every one that appears in a hook.

If the result is close but the diction keeps slipping, **Voices** (Pro/Premier) is the reliable escalation: clone a voice reading Neapolitan and the pronunciation problem largely stops being a prompting problem. Keep Audio Influence at 0.70–0.85 and drop the vocal identity block from the style box.
