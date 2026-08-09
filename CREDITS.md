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
- `models-and-versions.md`, cioè il confronto v4.5 / v4.5+ / v5 / v5.5, la scelta del modello e il gating per piano
- il controllo della durata con lo slider v5.5
- il formato di output a campi separati con conteggio caratteri

## Fonti ufficiali Suno

Dati su modelli, limiti dei campi, slider e funzioni presi dalla documentazione ufficiale. Elenco completo dei link in `skills/suno-songcraft/references/models-and-versions.md`; i principali:

- Knowledge base: https://help.suno.com/
- Release notes: https://suno.com/release-notes
- Blog: https://suno.com/blog

Suno rilascia funzioni con frequenza alta e questi file invecchiano. Quando qualcosa non torna, la fonte ufficiale vince sempre su quanto scritto qui.

## Licenza di questo plugin

**CC0 1.0 Universal**, come il progetto da cui deriva parte del materiale. Prendi, modifica, ripubblica, senza obblighi.
