# Crediti e fonti

## Materiale derivato

### `bitwize-music-studio/claude-ai-music-skills`

- Repo: https://github.com/bitwize-music-studio/claude-ai-music-skills
- Licenza: **CC0 1.0 Universal** (dedica al pubblico dominio)

Progetto molto più ampio di questo: 52 skill, oltre 380 file di genere, un server MCP e una pipeline di produzione album completa. Se cerchi un flusso di lavoro end-to-end — idea, testi, generazione, mix, mastering, copertina, promozione, uscita — è quello il riferimento, non questo plugin.

Parte del materiale di riferimento generale di `suno-songcraft` è adattato da lì. In particolare:

| Qui | Deriva da |
|---|---|
| Impostazione dello Style Box, disciplina dei descrittori, tag di struttura e loro affidabilità, performance cue | `skills/suno-engineer/SKILL.md`, `reference/suno/v5-best-practices.md`, `reference/suno/structure-tags.md` |
| Bande degli slider creativi e distinzione problema-di-prompt / problema-di-slider | `reference/suno/creative-sliders.md` |
| Principio della blocklist artisti — scomporre il nome in genere, voce, strumentazione, epoca | `reference/suno/artist-blocklist.md` |
| Gerarchia dei rimedi di pronuncia (riscrivere → respelling → trattini → contesto → accettare) e workflow della tabella di pronuncia | `reference/suno/pronunciation-guide.md` |

La licenza CC0 non impone attribuzione: questi crediti ci sono perché è giusto darli, non perché siano dovuti.

**Non deriva da lì**, ed è originale di questo plugin:

- tutto il materiale su italiano e napoletano (`italian-language.md`, `italian-genres.md`, `neapolitan-language.md`), incluse le tabelle di respelling, gli omografi italiani, i mutamenti fonetici del napoletano e la blocklist di artisti italiani
- `suno-connector.md`, cioè le scelte da passare al connettore, le trappole che annullano i consigli della skill e il ciclo misura-poi-correggi
- `models-and-versions.md`, cioè la matrice della famiglia v6 (v6 / v6-wild / v6-mini), la migrazione da v5.5, la storia dei modelli ritirati, la scelta del modello e il gating per piano
- il controllo della durata tramite numero di sezioni, con lo slider annunciato per v5.5 da verificare su v6
- la mappatura dei campi verso l'API Suno
- il formato di output a campi separati con conteggio caratteri

## Fonti ufficiali Suno

Dati su modelli, limiti dei campi, slider e funzioni presi dalla documentazione ufficiale. Elenco completo dei link in `skills/suno-songcraft/references/models-and-versions.md`; i principali:

- Knowledge base: https://help.suno.com/
- Release notes: https://suno.com/release-notes
- Blog: https://suno.com/blog

Per la famiglia v6 (v6, v6-wild, v6-mini), Variety, Max Mode, limiti di download e Studio 2.0:

- Introducing v6: https://suno.com/blog/introducing-v6
- v6 FAQ: https://help.suno.com/en/articles/13924481
- What's new in v6: https://help.suno.com/en/articles/13924801
- Current models: v6: https://help.suno.com/en/articles/13924737
- Aggiornamento dei Termini e limiti di download: https://suno.com/blog/suno-updates-tos
- Studio 2.0: https://about.suno.com/blog/studio-2
- Add Vocals: https://help.suno.com/en/articles/6882817

Per il connettore Suno: le descrizioni degli strumenti del connettore ufficiale di Suno per Claude (API `v0`), consultate il 6 novembre 2026. Suno non pubblica una documentazione pubblica di questa API: quando un parametro cambia, fanno fede le descrizioni che il connettore espone in quel momento.

Suno rilascia funzioni con frequenza alta e questi file invecchiano. Quando qualcosa non torna, la fonte ufficiale vince sempre su quanto scritto qui.

## Licenza di questo plugin

**CC0 1.0 Universal**, come il progetto da cui deriva parte del materiale. Prendi, modifica, ripubblica, senza obblighi.
