# Suno Songcraft — plugin per Claude Code

Trasforma un'idea di canzone in prompt Suno pronti da incollare: **Style Box**, **Lyrics Box** con structure tag e performance cue, **Exclude Styles**, slider creativi, durata e scelta del modello (v4.5 / v4.5+ / v5 / v5.5).

Non è un generatore di testi con qualche aggettivo in più: la skill lavora sui punti in cui le generazioni Suno falliscono davvero — didascalie cantate per errore, voci sepolte nel mix, sezioni saltate, output generico, nomi di artisti che fanno fallire il prompt in silenzio.

## Installazione

Non serve clonare niente: questo repo **è** il marketplace, perché contiene `.claude-plugin/marketplace.json` nella root. Da dentro Claude Code:

```
/plugin marketplace add electroendjneer/suno-songcraft
/plugin install suno-songcraft@suno-tools
```

Se al termine compare `Run /reload-plugins to activate.`, esegui `/reload-plugins`. Per verificare: `/plugin`.

La skill diventa disponibile come `/suno-songcraft` e Claude la richiama anche da solo quando la conversazione riguarda Suno, prompt musicali, testi da generare o una traccia venuta male.

### Due avvertenze sulla forma `utente/repo`

**Clona via SSH per default.** Se non hai una chiave SSH caricata per GitHub, forza HTTPS:

```
CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1 claude plugin marketplace add electroendjneer/suno-songcraft
```

oppure passa direttamente l'URL completo:

```
/plugin marketplace add https://github.com/electroendjneer/suno-songcraft.git
```

**Il repo è privato.** L'installazione da repo privata funziona — Claude Code usa i credential helper git che hai già configurati (`gh auth login`, keychain, `git-credential-store`) — ma solo per chi ha accesso al repo. Perché chiunque possa installarlo con quel comando, il repo deve diventare pubblico.

### Aggiornamenti

Chi ha già installato riceve le novità solo se alzi `version` in `.claude-plugin/plugin.json` **e** nella voce corrispondente di `.claude-plugin/marketplace.json`. Poi:

```
/plugin marketplace update suno-tools
/plugin update suno-songcraft
```

In alternativa, togliendo del tutto il campo `version` da entrambi i file gli aggiornamenti seguono il commit SHA — comodo mentre il plugin è in sviluppo attivo, meno adatto a una distribuzione stabile.

### Installazione da cartella locale

Se preferisci lavorarci in locale senza passare da GitHub:

```
/plugin marketplace add ./sunoskill
/plugin install suno-songcraft@suno-tools
```

## Come si usa

Basta descrivere quello che vuoi. Qualche esempio:

- «Voglio una ballad italiana malinconica per pianoforte e archi, voce femminile, circa 3 minuti»
- «Fammi un pezzo drum & bass strumentale per un trailer, 174 BPM, cupo»
- «Questa traccia mi è venuta generica, ecco lo style box che ho usato — sistemalo»
- «Perché Suno mi canta “(instrumental break)”?»

L'output arriva sempre nello stesso formato, campo per campo, con il conteggio caratteri:

```
MODEL: v5.5 · INSTRUMENTAL: Off

STYLE BOX  (238/1000)
────────────────────────────────
...

LYRICS BOX  (1.847/5000)
────────────────────────────────
...

EXCLUDE STYLES: ...
SLIDERS: Weirdness ... · Style Influence ...
DURATION: ...
```

Nota: i **testi** vengono scritti nella lingua che chiedi, lo **style box resta in inglese** — il vocabolario di stile di Suno è addestrato in inglese e i descrittori tradotti rendono in modo inaffidabile.

## Struttura

```
.
├── .claude-plugin/
│   ├── plugin.json           manifest del plugin
│   └── marketplace.json      catalogo (permette /plugin marketplace add su questa cartella)
├── skills/
│   └── suno-songcraft/
│       ├── SKILL.md          regole, workflow, formato di output, checklist
│       └── references/
│           ├── models-and-versions.md    v4.5 / v4.5+ / v5 / v5.5, gating per piano, timeline funzioni
│           ├── style-box.md              costruzione dello stile, vocabolario vocale, blocklist artisti
│           ├── lyrics-box.md             tag di struttura, affidabilità, sillabe, effetti, duetti
│           ├── sliders-and-iteration.md  slider, Song Editor, extend, stem, Studio 1.2
│           ├── genre-playbook.md         template per genere con BPM e bande di slider
│           └── troubleshooting.md        sintomo → causa → rimedio
└── dist/
    └── suno-ai-mastery-v55.skill         pacchetto .skill della versione precedente (storico)
```

Claude carica `SKILL.md` quando la skill si attiva e apre i file in `references/` solo quando servono.

## Fonti

I dati su modelli, limiti dei campi e funzioni provengono dalla documentazione ufficiale Suno (help center, release notes, blog). L'elenco completo dei link è in fondo a `skills/suno-songcraft/references/models-and-versions.md`, così è verificabile e aggiornabile quando Suno cambia qualcosa.

Parte del materiale di riferimento è adattato da `bitwize-music-studio/claude-ai-music-skills` (CC0 1.0 / pubblico dominio).

## Manutenzione

Suno rilascia funzioni con frequenza alta. I punti che invecchiano per primi, in ordine:

1. **Limiti dei campi** e **modelli disponibili per piano** — tabella in `models-and-versions.md`
2. **Timeline funzioni 2026** — stessa pagina, sezione finale
3. **Gating dei piani** — verifica sulla pagina prezzi prima di consigliare un upgrade

Quando aggiorni, alza `version` in `plugin.json` e in `marketplace.json` e annota la modifica nel `CHANGELOG.md`.
