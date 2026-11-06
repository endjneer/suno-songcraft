# Changelog

## 1.2.0 — 2026-11-06

Aggiornamento alla famiglia di modelli Suno v6 (v6, v6-wild, v6-mini), uscita il 9 settembre 2026. Tutti i modelli precedenti sono ritirati per le nuove generazioni.

### Aggiunto

- Scelta del modello fra v6, v6-wild e v6-mini, con piani, costi e la regola di tenere fisso il modello mentre si itera.
- Slider **Variety** (Off di default in tutti i prompt della skill) e toggle **Max Mode**, in `SKILL.md` e `sliders-and-iteration.md`. Primo passo di ogni diagnosi: leggere la style line del brano generato, perché tag cambiati vogliono dire Variety.
- Edit in linguaggio naturale su un brano esistente (una sezione o una parola), prima del Song Editor.
- Simple mode con più input (brani, playlist, audio, immagini, video) come alternativa alla Custom mode.
- Sezione **Through the Suno API** con la mappatura dei campi (`style`, `lyrics`, `negative_style`, `controls.*`, `max_mode`, `description`...).
- Limiti di download per piano (Termini in vigore dal 3 settembre 2026) e Studio 2.0.
- In `models-and-versions.md`: matrice della famiglia v6, migrazione v5.5 → v6, timeline estesa (Studio 2.0, Termini, v6), sezione **Retired models (history)**.
- In `troubleshooting.md`: controllo di Variety in cima e segnalazioni (aneddotiche) degli utenti su v6.

### Modificato

- Limiti dei campi in una sola colonna "v6 family", più il limite di 3.000 caratteri della description in Simple mode.
- Durata: lo slider Duration (annunciato per v5.5) va verificato in-app su v6; il numero di sezioni resta la leva principale.
- Voices, Custom Models e My Taste non più etichettati v5.5; i Custom Models esistenti sono passati a v6 da soli e vanno riprovati su un brano di riferimento.
- Riferimenti di versione in `lyrics-box.md` e `style-box.md`.
- Formato di output: `MODEL`, `MODE`, `SLIDERS` con Variety, `MAX MODE`.

### Rimosso

- Ogni consiglio di provare V4.5 sui generi pesanti: non c'è più un modello di riserva.
- L'avviso «current models are slated for deprecation»: la deprecazione è avvenuta.
- I nomi API `styleWeight` e `weirdnessConstraint`, che vengono da wrapper di terze parti.

## 1.1.0 — 2026-08-09

Specializzazione sulla musica in lingua italiana e napoletana, più attribuzioni esplicite.

### Aggiunto

- `references/italian-language.md`: pronuncia italiana per Suno — i tre ancoraggi (dichiarazione in Style Box, esclusioni, respelling), vocali finali, doppie geminate, tabella dei grafemi a rischio, accento tonico, dieci omografi italiani, elisione e troncamento, numeri e nomi propri, gerarchia dei rimedi, accenti regionali, descrittori vocali per tradizione, workflow della tabella di pronuncia.
- `references/italian-genres.md`: diciassette voci di genere italiano con template di Style Box, BPM e bande di slider — cantautorato classico e moderno, itpop, pop radiofonico, Sanremo, leggera anni Sessanta, boom bap e trap italiana, drill milanese, italo disco, italo house, eurodance, canzone napoletana, neomelodico, rock, rock alternativo e prog italiano, pizzica, liscio, canto popolare, spaghetti western, giallo, commedia all'italiana. Più la blocklist degli artisti italiani scomposti in descrittori e una sezione onesta sui limiti di Suno sul repertorio italiano.
- `references/neapolitan-language.md`: il napoletano trattato come lingua a sé — scelta tra ortografia autentica e italiano fonetico, schwa, mutamenti fonetici regolari dall'italiano, articoli e apostrofi, metafonia, raddoppiamento sintattico, tabella di respelling, sette tradizioni dalla villanella al rap, strumenti e ritmi, sei template di Style Box, e i casi in cui conviene rinunciare.
- Sezione **Italian and Neapolitan** in `SKILL.md` con le tre regole trasversali e l'instradamento ai file.
- `CREDITS.md`: cosa deriva da `bitwize-music-studio/claude-ai-music-skills` (CC0), voce per voce, e cosa è originale.
- `LICENSE`: CC0 1.0 Universal.

### Modificato

- Descrizione della skill estesa alla specializzazione italiana, per il triggering.
- README: sezione sulla taratura italiana, crediti e licenza.

## 1.0.0 — 2026-08-09

Prima release come plugin Claude Code. La skill preesistente `suno-ai-mastery-v55` è stata rinominata `suno-songcraft` (un nome con il numero di versione dentro invecchia a ogni rilascio Suno) e impacchettata con manifest e marketplace.

### Aggiunto

- `references/models-and-versions.md`: matrice di capacità v4.5 / v4.5+ / v5 / v5.5, differenze di prompting tra versioni, criteri di scelta del modello, dettaglio su Voices / Custom Models / Personas / My Taste, timeline funzioni 2026, gating per piano, elenco fonti ufficiali.
- Sezione **Duration** in `SKILL.md`: slider di durata su web con v5.5 (dal 20 luglio 2026), modalità Auto e Custom, e il fallback a conteggio sezioni per mobile, API e modelli precedenti.
- Sezione **Pick the model before writing anything** in `SKILL.md`.
- Forma alternativa dello style box come *production brief* discorsivo, con l'esempio ufficiale Suno introdotto in v4.5.
- Studio 1.2 (Remove FX, Warp Markers, time signature, Alternates) e l'editor testi web di luglio 2026 in `sliders-and-iteration.md`.
- Regola esplicita: testi nella lingua richiesta, style box sempre in inglese.

### Corretto

- «Non esiste alcun parametro di durata» — non è più vero da luglio 2026. Corretto in `SKILL.md` e in `troubleshooting.md`.
- Voices non è più solo Pro/Premier: da agosto 2026 è su mobile, con funzionalità ridotte sui piani free.
- Aggiunte le formulazioni ufficiali degli slider (Weirdness **Safe → Chaos**, 50% = risultato normale atteso; Style Influence **Loose → Strong**) come baseline dichiarata.
