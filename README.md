<a id="english"></a>

# Suno Songcraft

> **English** · [Italiano →](#italiano)

A Claude Code plugin that turns a song idea into paste-ready Suno prompts — **Style Box**, **Lyrics Box** with structure tags and performance cues, **Exclude Styles**, creative sliders including Variety and Max Mode, duration, and model choice across v6 / v6-wild / v6-mini.

It isn't a lyric generator with extra adjectives. It works on the places Suno generations actually fail: stage directions sung out loud by mistake, vocals buried in the mix, sections skipped, generic-but-correct output, and artist names that make a prompt fail silently.

**Its distinguishing feature is Italian.** Most Suno guidance is English-first, and an Italian-language track doesn't fail on the arrangement — it fails on pronunciation. One swallowed final vowel and a native listener hears it immediately. This plugin carries three reference files that no general Suno guide covers:

- **`italian-language.md`** — final vowels, geminate consonants, the grapheme risk table (`gli`, `gn`, `sci`, `z`, intervocalic `s`), stress and written accents, ten Italian homographs, elision and truncation, regional diction
- **`italian-genres.md`** — 17 Italian genre entries with style-box templates, BPM ranges and slider bands: cantautorato, itpop, Sanremo, boom bap and trap italiana, drill, italo disco, italo house, eurodance, Italian rock and prog, pizzica, liscio, spaghetti western, giallo. Plus the Italian half of the artist blocklist, decomposed into sonic descriptors
- **`neapolitan-language.md`** — Neapolitan treated as its own language: the schwa, regular sound changes from Italian (*quanno*, *chiù*, *Maronna*), apostrophes Suno reads as pauses, metaphony, syntactic doubling, a respelling table, seven traditions from villanella to rap, tammorra and tarantella rhythms

The rule that governs all of it: **lyrics in the target language, Style Box always in English** — Suno's style vocabulary is English-trained and translated descriptors land unreliably.

## Install

No cloning needed: this repo **is** the marketplace, because it carries `.claude-plugin/marketplace.json` at its root.

```
/plugin marketplace add https://github.com/electroendjneer/suno-songcraft.git
/plugin install suno-songcraft@suno-tools
```

If the install summary says `Run /reload-plugins to activate.`, run it. Check with `/plugin`.

The skill is then available as `/suno-songcraft`, and Claude invokes it on its own whenever the conversation turns to Suno, style prompts, lyrics meant for generation, or a track that came out wrong.

**Why the full URL and not the `owner/repo` shorthand.** The shorthand clones over SSH, which authenticates as whichever GitHub account your SSH key belongs to — not necessarily the one that has access to this repo. The explicit `https://` URL goes through your git credential helper (`gh auth login`, keychain, `git-credential-store`) and matches the account you're actually signed in as. The shorthand works too if your SSH key is on the right account, or with `CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1` in front of the command — but the full URL simply always works, including for updates.

**This repo is currently private.** Installing from a private repo is supported, but only for accounts with access. To let someone else install it, either add them as a collaborator on the repo, or make the repo public.

## Usage

Just describe what you want:

> *"Voglio una ballad italiana malinconica per pianoforte e archi, voce femminile, circa 3 minuti"*
> *"A Neapolitan tammurriata, group vocals, tammorra ostinato"*
> *"This came out generic — here's the style box I used, fix it"*
> *"Why is Suno singing '(instrumental break)' out loud?"*

Output always arrives field by field, with character counts:

```
MODEL: v6 · MODE: Custom · INSTRUMENTAL: Off

STYLE BOX  (238/1000)
────────────────────────────────
...

LYRICS BOX  (1,847/5000)
────────────────────────────────
...

EXCLUDE STYLES: ...
SLIDERS: Variety Off · Weirdness ... · Style Influence ...
MAX MODE: Off
DURATION: ...
```

## Layout

```
.
├── .claude-plugin/
│   ├── plugin.json           plugin manifest
│   └── marketplace.json      catalog — lets /plugin marketplace add point at this repo
├── skills/
│   └── suno-songcraft/
│       ├── SKILL.md          rules, workflow, output format, pre-flight checklist
│       └── references/
│           ├── models-and-versions.md    v6 / v6-wild / v6-mini, v5.5 → v6 migration, plan gating, retired models, 2026 timeline
│           ├── style-box.md              style construction, vocal vocabulary, artist blocklist
│           ├── lyrics-box.md             structure tags, reliability tiers, syllables, SFX, duets
│           ├── sliders-and-iteration.md  sliders incl. Variety, Max Mode, plain-language edits, Song Editor, stems, Studio 2.0
│           ├── genre-playbook.md         per-genre templates with BPM and slider bands
│           ├── italian-language.md       Italian pronunciation for Suno
│           ├── italian-genres.md         Italian genres + Italian artist blocklist
│           ├── neapolitan-language.md    Neapolitan: phonology, orthography, traditions
│           └── troubleshooting.md        symptom → cause → fix
└── dist/
    └── suno-ai-mastery.skill             previous packaged version, kept for reference
```

Claude loads `SKILL.md` when the skill fires and opens `references/` files only when it needs them.

## Credits, sources, license

Model facts, field limits and feature availability come from Suno's official documentation — help centre, release notes, blog. The full link list is at the bottom of `references/models-and-versions.md`, so it stays verifiable as Suno changes.

Parts of the general reference material are adapted from [`bitwize-music-studio/claude-ai-music-skills`](https://github.com/bitwize-music-studio/claude-ai-music-skills) (CC0 1.0) — a far larger project, 52 skills and a full album production pipeline. If that's what you want, go there instead. Item-by-item attribution is in [`CREDITS.md`](CREDITS.md).

The Italian and Neapolitan material is original to this plugin.

License: **CC0 1.0 Universal**. Take it, change it, republish it, no obligations.

---

<a id="italiano"></a>

# Suno Songcraft — in italiano

> [← English](#english) · **Italiano**

Plugin per Claude Code che trasforma un'idea di canzone in prompt Suno pronti da incollare: **Style Box**, **Lyrics Box** con structure tag e performance cue, **Exclude Styles**, slider creativi (incluse Variety e Max Mode), durata e scelta del modello (v6 / v6-wild / v6-mini).

Non è un generatore di testi con qualche aggettivo in più: lavora sui punti in cui le generazioni Suno falliscono davvero — didascalie cantate per errore, voci sepolte nel mix, sezioni saltate, output generico, nomi di artisti che fanno fallire il prompt in silenzio.

## Tarato sulla musica italiana

È la parte che non trovi altrove. Un pezzo in italiano non fallisce sull'arrangiamento, fallisce sulla pronuncia: una vocale finale ingoiata e il disco si smaschera da solo.

- **`italian-language.md`** — vocali finali, doppie geminate, tabella dei grafemi a rischio (`gli`, `gn`, `sci`, `z`, `s` intervocalica), accento tonico e accenti scritti, dieci omografi italiani (*àncora* / *ancóra*), elisione e troncamento, dizione regionale
- **`italian-genres.md`** — 17 voci di genere con template di Style Box, BPM e bande di slider: cantautorato classico e moderno, itpop, pop radiofonico, Sanremo, leggera anni Sessanta, boom bap e trap italiana, drill milanese, italo disco, italo house, eurodance, rock e prog italiano, pizzica, liscio, canto popolare, spaghetti western, giallo, commedia all'italiana. Più la blocklist degli artisti italiani, scomposti in descrittori sonori
- **`neapolitan-language.md`** — il napoletano come lingua a sé: schwa, mutamenti fonetici regolari dall'italiano (*quanno*, *chiù*, *Maronna*), apostrofi che Suno legge come pause, metafonia, raddoppiamento sintattico, tabella di respelling, sette tradizioni dalla villanella al rap, tammorra e tarantella

Regola trasversale: **testi nella lingua richiesta, Style Box sempre in inglese**, perché il vocabolario di stile di Suno è addestrato in inglese e i descrittori tradotti rendono in modo inaffidabile.

## Installazione

Non serve clonare niente: questo repo **è** il marketplace, perché contiene `.claude-plugin/marketplace.json` nella root.

```
/plugin marketplace add https://github.com/electroendjneer/suno-songcraft.git
/plugin install suno-songcraft@suno-tools
```

Se al termine compare `Run /reload-plugins to activate.`, esegui `/reload-plugins`. Per verificare: `/plugin`.

La skill diventa disponibile come `/suno-songcraft` e Claude la richiama anche da solo quando la conversazione riguarda Suno, prompt musicali, testi da generare o una traccia venuta male.

**Perché l'URL completo e non la forma `utente/repo`.** La forma breve clona via SSH, e SSH ti autentica come l'account GitHub a cui appartiene la chiave — che non è per forza quello con accesso a questo repo. Se hai più account configurati sulla stessa macchina, è la trappola classica: il comando fallisce con un errore di repo inesistente, che sembra un problema di nome. L'URL `https://` esplicito passa invece dal credential helper git (`gh auth login`, keychain, `git-credential-store`) e usa l'account con cui sei realmente loggato. La forma breve funziona lo stesso se la chiave SSH è sull'account giusto, oppure anteponendo `CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1` — ma l'URL completo funziona sempre, aggiornamenti inclusi.

**Il repo al momento è privato.** L'installazione da repo privata è supportata, ma solo per account che vi hanno accesso. Per farlo installare a qualcun altro: o lo aggiungi come collaboratore, o rendi il repo pubblico.

### Installazione da cartella locale

```
/plugin marketplace add ./sunoskill
/plugin install suno-songcraft@suno-tools
```

### Aggiornamenti

Chi ha già installato riceve le novità solo se alzi `version` in `.claude-plugin/plugin.json` **e** nella voce corrispondente di `.claude-plugin/marketplace.json`. Poi:

```
/plugin marketplace update suno-tools
/plugin update suno-songcraft
```

Togliendo del tutto il campo `version` da entrambi i file, gli aggiornamenti seguono invece il commit SHA — comodo in sviluppo attivo, meno adatto a una distribuzione stabile.

## Manutenzione

Suno rilascia funzioni con frequenza alta. I punti che invecchiano per primi, in ordine:

1. **Limiti dei campi** e **modelli disponibili per piano** — tabella in `models-and-versions.md`
2. **Timeline funzioni 2026** — stessa pagina, sezione finale
3. **Gating dei piani** — verifica sulla pagina prezzi prima di consigliare un upgrade

Quando aggiorni, alza `version` nei due manifest e annota la modifica nel `CHANGELOG.md`.

## Crediti e licenza

Dati su modelli, limiti dei campi e funzioni dalla documentazione ufficiale Suno; link completi in fondo a `references/models-and-versions.md`.

Parte del materiale di riferimento generale è adattato da [`bitwize-music-studio/claude-ai-music-skills`](https://github.com/bitwize-music-studio/claude-ai-music-skills) (CC0 1.0), progetto molto più ampio — 52 skill e una pipeline album completa. Il dettaglio voce per voce è in [`CREDITS.md`](CREDITS.md). Il materiale su italiano e napoletano è originale di questo plugin.

Licenza: **CC0 1.0 Universal**.
