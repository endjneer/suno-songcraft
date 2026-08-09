# Italian Lyrics Reference

How to get Suno to sing Italian like an Italian. This is the highest-leverage file in the skill for Italian-language tracks: the style box decides the genre, but pronunciation decides whether a native listener believes the record.

The core problem is mechanical. Suno's vocal model is weighted toward English orthography, so when it meets Italian spelling it applies English reading rules unless something anchors it. Every technique below is a way of anchoring it.

## Contents
- [The three anchors](#the-three-anchors)
- [Final vowels: the single biggest tell](#final-vowels-the-single-biggest-tell)
- [Double consonants](#double-consonants)
- [Grapheme risk table](#grapheme-risk-table)
- [Stress and written accents](#stress-and-written-accents)
- [Italian homographs](#italian-homographs)
- [Elision and truncation](#elision-and-truncation)
- [Numbers, foreign words, proper nouns](#numbers-foreign-words-proper-nouns)
- [Fix hierarchy](#fix-hierarchy)
- [Dialects and regional diction](#dialects-and-regional-diction)
- [Vocal descriptors for Italian](#vocal-descriptors-for-italian)
- [Pronunciation notes workflow](#pronunciation-notes-workflow)

---

## The three anchors

Use all three. Any one alone drifts.

**1. Declare the language in the Style Box — in English.**
The style box stays English even for an Italian track, because Suno's style vocabulary is English-trained. The language of the *lyrics* is a descriptor like any other:

```
Italian male baritone, cantautore phrasing, conversational and consonant-forward,
sung in Italian with native diction. Acoustic singer-songwriter, nylon-string
guitar, upright piano, brushed drums. 84 BPM, warm intimate mix, vocal upfront.
```

**2. Exclude the drift.** Suno's default pull is back toward English vowels:

```
EXCLUDE STYLES: no English vocals, no foreign accent on Italian
```

**3. Respell what matters in the Lyrics Box.** Not the whole lyric — only the words where a wrong reading would be audible. The rest of this file is about identifying which those are.

**One language per section.** Mixed Italian and English inside the same section causes pronunciation drift across the whole section. Keep the English hook in its own `[Chorus]` and the Italian verses in theirs, and say so in the style box: `bilingual, Italian verses, English chorus`.

---

## Final vowels: the single biggest tell

Italian has no schwa. Every final vowel is fully articulated: *amore* ends on a clear open **e**, not on the swallowed *-uh* an English model defaults to. This one failure makes an otherwise good take sound instantly foreign, and it is the most common complaint about Italian on Suno.

Three defences, in order:

1. **Style box**: `open Italian vowels, fully articulated final syllables`
2. **Melody**: put final vowels on sustained notes where you can — Suno articulates a held vowel far more reliably than a passing one. Hyphenate to force it: `amo-re`, `cuo-re`, `mare-e`
3. **Respelling** for the words that carry the line: `amore` → `a-MO-re`, `cantare` → `kan-TA-re`

Watch for it especially at the end of a phrase, which is exactly where an English-weighted model wants to relax into a schwa.

---

## Double consonants

Italian geminates are phonemic — they change the word, not just its colour. English has no equivalent, so the model flattens them and you get *fato* where you wrote *fatto*.

| Written | Means | Flattened to | Means |
|---|---|---|---|
| fatto | done | fato | fate |
| carro | cart | caro | dear |
| palla | ball | pala | shovel |
| nonno | grandfather | nono | ninth |
| sette | seven | sete | thirst |
| notte | night | note | notes |
| anno | year | ano | anus |

That last row is why this matters more than it looks.

**Never simplify a double consonant to fit a syllable count.** If the geminate carries meaning and the take keeps flattening it, split it across the syllable boundary:

```
not-te    car-ro    fat-to    an-no
```

Use this sparingly — a hyphen also signals a sustained note, so a lyric full of them will start bending the melody. Reserve it for the two or three words per song where the distinction actually lands.

---

## Grapheme risk table

Italian spelling is regular; the problem is that its rules differ from English exactly where the letters look familiar.

| Spelling | Italian value | What an English-weighted read does | Respelling |
|---|---|---|---|
| `gli` | palatal *ʎ*, roughly *ly* | hard *glee* | `figlio` → `FEE-lyo` |
| `gn` | palatal *ɲ*, roughly *ny* | hard *g* + *n* | `sogno` → `SO-nyo` |
| `sci`, `sce` | *sh* | *sky*, *ski* | `pesce` → `PE-she`, `sciogliere` → `SHO-lye-re` |
| `ch`, `chi` | hard *k* | *ch* as in *chair* | `che` → `ke`, `perché` → `per-KE` |
| `gh` | hard *g* | soft *g* | `ghiaccio` → `GYA-cho` |
| `c` + e/i | *ch* as in *chair* | hard *k* | `cielo` → `CHE-lo` |
| `g` + e/i | *j* as in *jam* | hard *g* | `gelo` → `JE-lo` |
| `z` | *ts* or *dz* | *z* as in *zoo* | `grazie` → `GRA-tsye`, `zero` → `DZE-ro` |
| `s` between vowels | voiced *z* | unvoiced *s* | `casa` → `KA-za` |
| `r` | tapped/trilled | English approximant | not fixable by spelling — see style box below |

The `r` is the one respelling can't reach. `Italian rolled R` in the style box helps; a strong take usually gets it right on its own once the other anchors are in place.

---

## Stress and written accents

Italian default stress is penultimate. Words stressed on the final syllable carry a written accent, and Suno routinely ignores it and falls back to the default — *città* becomes *CIT-ta*, *perché* becomes *PER-che*.

**Always keep the accent**, and for the words that carry a line, add capitals:

```
per-CHÉ    cit-TÀ    pe-RÒ    vir-TÙ    caf-FÈ    veri-TÀ
```

You can also write an accent where orthography doesn't require one, purely to disambiguate for the model. It looks wrong on the page and nobody sees the page.

Open vs closed vowels (*pèsca* peach / *pésca* fishing, *bòtte* barrel / *bótte* blows) are worth marking only when the whole line turns on the difference. Most of the time the listener resolves it from context faster than the model would.

---

## Italian homographs

The Italian equivalent of the English *live* / *read* problem. Same spelling, different stress, different meaning — and Suno picks by frequency, not by your intent.

| Written | Reading A | Reading B | Disambiguate as |
|---|---|---|---|
| ancora | **àn**cora — anchor | an**có**ra — still, again | `AN-co-ra` / `an-CO-ra` |
| pesca | **pè**sca — peach | **pé**sca — fishing | context or accent |
| botte | **bòt**te — barrel | **bót**te — blows | context or accent |
| principi | **prìn**cipi — princes | prin**cì**pi — principles | `PRIN-ci-pi` / `prin-CI-pi` |
| subito | **sù**bito — immediately | su**bì**to — endured | `SU-bi-to` / `su-BI-to` |
| capitano | capi**tà**no — captain | ca**pì**tano — they happen | `capi-TA-no` / `ca-PI-ta-no` |
| ambito | **àm**bito — scope | am**bì**to — coveted | `AM-bi-to` / `am-BI-to` |
| compito | **còm**pito — task | com**pì**to — polite | `COM-pi-to` / `com-PI-to` |
| seguito | **sé**guito — retinue, sequel | segu**ì**to — followed | `SE-gui-to` / `se-GUI-to` |
| tenere | **tè**nere — tender (f. pl.) | te**né**re — to hold | `TE-ne-re` / `te-NE-re` |

Before respelling, ask whether a rewrite is cleaner — see the fix hierarchy.

---

## Elision and truncation

Canzone italiana lives on these, and both confuse the model.

**Troncamento** — dropping a final vowel: *amor*, *cuor*, *voler*, *andar*, *far*, *son*, *van*. Suno tends to restore the missing vowel, which breaks the syllable count you wrote the melody around. If the take keeps restoring it, either accept the full form and re-fit the line, or hyphenate the truncated form to mark it as complete: `a-MOR`.

**Elisione** — apostrophe merging two words: *d'amore*, *l'anima*, *un'ora*, *dell'alba*. The risk is that the apostrophe is read as a break, splitting one sung word into two. Respell as the single word it actually is:

```
d'amore   → da-MO-re
l'anima   → LA-ni-ma
un'ora    → u-NO-ra
dell'alba → del-LAL-ba
```

Note that `dell'alba` also carries a geminate across the apostrophe — the respelling preserves it.

---

## Numbers, foreign words, proper nouns

**Spell numbers out.** `ventuno`, not `21`. Digits are read inconsistently and sometimes in English.

**English words inside an Italian lyric** get an Italian reading, which may be what you want (it's how Italians actually sing them) or may not. If you want the English pronunciation, isolate the word with a comma and add `English word pronounced in English` to the pronunciation notes; if you want it Italianised, respell it: *weekend* → `wee-KEND`.

**Place and proper names** are the most-mangled category, because they're rare tokens. Respell every one you care about: *Trastevere* → `tras-TE-ve-re`, *Chiaia* → `KYA-ya`, *Genova* → `JE-no-va`.

**Watch the filter.** Ordinary Italian words occasionally collide with a producer tag and make the generation fail or return something unrelated. If a prompt fails for no visible reason, try an alternate spelling before assuming the model is broken.

---

## Fix hierarchy

Work down this list. The techniques get more powerful and more disfiguring as you go, so stop as soon as the problem is solved.

**1. Rewrite.** The best fix is usually a different word. *Ancora* ambiguous? Use *di nuovo* or *ferma*. This costs nothing at generation time and leaves the lyric clean.

**2. Phonetic respelling.** Write it as it sounds. Ugly on the page, invisible in the audio.

**3. Hyphenation.** Splits syllables and forces articulation. Remember it also sustains the note — a side effect you can exploit on a held final vowel, or fight on a fast line.

**4. Context padding.** Add a word that makes the reading obvious. *Ancora una volta* forces *ancóra* without any respelling at all.

**5. Accept it.** Say the line out loud both ways and ask whether a wrong reading actually ruins the song. Often it doesn't. Note the risk and move on rather than disfiguring the lyric.

*(This five-step hierarchy is adapted from the pronunciation guide in `bitwize-music-studio/claude-ai-music-skills`, CC0 — see `CREDITS.md`. The Italian material above is specific to this skill.)*

---

## Dialects and regional diction

Dialect is where Suno struggles most, because these forms are thin in the training data. Two rules make it survivable: **keep dialect in its own sections**, and **respell aggressively** — orthographic conventions for Italian dialects are inconsistent even among native writers, so the model has nothing stable to latch onto.

| Variety | Style box cue | Written traits to respell |
|---|---|---|
| **Napoletano** | `Neapolitan diction, melodic southern phrasing` | `'o`, `'a` articles; `nun` for *non*; `chiù` for *più*; final vowels reduced — the one Italian variety that *does* have a schwa, so mark it: `mare` → `MA-rə` reads unreliably, prefer `MA-re` and let the phrasing carry it |
| **Romanesco** | `Roman accent, clipped urban delivery` | `nun`, `daje`, `annamo`, doubled consonants after articles (`a casa` → `a ccasa`) |
| **Siciliano** | `Sicilian diction, dark closed vowels` | `u`, `chistu`, `beddu` (the *dd* is retroflex — `BED-du` is close enough) |
| **Milanese / settentrionale** | `Northern Italian diction, closed vowels, light gemination` | fewer doubles, tighter vowels — mostly a phrasing instruction, little to respell |

For neomelodico specifically, the vocal style matters more than the dialect accuracy: `Neapolitan tenor, heavy vibrato, melismatic, emotional belt` does more work than any spelling.

---

## Vocal descriptors for Italian

These go at the front of the Style Box, in English, like any vocal identity. Pick the register and the tradition — the tradition word carries a lot.

| Tradition | Descriptor block |
|---|---|
| Cantautorato | `Italian male baritone, conversational near-spoken phrasing, consonant-forward, unpolished` |
| Pop italiano | `Italian female alto, open vowels, melodic pop phrasing, clean modern delivery` |
| Sanremo / leggera | `Italian tenor, theatrical vibrato, sustained belt on the hook, orchestral phrasing` |
| Canzone napoletana | `Neapolitan tenor, operatic vibrato, melismatic, full chest voice` |
| Indie italiano | `Italian male tenor, flat affect, deadpan delivery, slightly nasal, close-mic` |
| Rap italiano | `Italian male rap flow, clipped consonants, conversational cadence, dry vocal` |
| Trap italiana | `Italian male vocal, auto-tuned, melodic ad-libs, laid-back behind the beat` |

Add `sung in Italian with native diction` in every case, and drop the whole block if a Voice or Persona is carrying the vocal.

---

## Pronunciation notes workflow

For anything longer than a demo, keep a small table alongside the lyric and apply every row before generating. The point is that respellings get lost between drafts — the table is the record of which ones are load-bearing.

| Word | Risk | Applied form | Why |
|---|---|---|---|
| perché | stress falls back to penultimate | `per-CHÉ` | ends the chorus line |
| anno | flattens to *ano* | `an-no` | meaning-critical |
| d'amore | apostrophe read as a break | `da-MO-re` | title word |
| Trastevere | rare token | `tras-TE-ve-re` | proper noun in the hook |

Then check the take against the table specifically, rather than listening for "does it sound Italian" in general — a vague listen misses exactly the errors that are one syllable long.
