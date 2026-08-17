<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:.orchestrator/README.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Orchestrator Foundation v0.1

Questa cartella contiene la foundation dichiarativa dell'Orchestrator per il repository `els-platform`.

La foundation v0.1 non e eseguibile: non chiama API, non avvia agenti, non modifica repository, non crea automazioni GitHub e non esegue merge. Serve a rendere espliciti ruoli, policy, stati, workflow e prompt operativi minimi per il pilota AI.

## Scopo

L'Orchestrator coordina un solo flusso pilota:

```text
Issue pronta
-> Implementazione Codex
-> Draft Pull Request
-> Revisione Claude
-> Approvazione umana
-> Merge eseguito esclusivamente dall'umano
```

Il comportamento da validare e uno solo: trasformare una issue chiara in una draft PR verificabile, senza estendere lo scope e senza modificare `main`.

## Gerarchia delle fonti

In caso di conflitto prevale sempre la fonte piu alta:

1. `docs/00-project/ai-development-operating-model.md`
2. `AGENTS.md`
3. file in `.orchestrator/`
4. singola issue approvata

Se una configurazione in `.orchestrator/` contraddice la governance, il task deve essere bloccato e portato all'approvazione umana.

## Relazione con AGENTS.md

`AGENTS.md` contiene le regole operative generali per agenti e sviluppatori nel repository. Questa cartella traduce quelle regole in una forma piu strutturata per il workflow pilota, senza sostituirle.

## Relazione con il modello operativo

`docs/00-project/ai-development-operating-model.md` resta la fonte normativa. La cartella `.orchestrator/` ne materializza la versione v0.1 in file leggibili da umani e agenti.

## File presenti

- `agents.yaml`: ruoli attivi, responsabilita e permessi.
- `policies.yaml`: vincoli operativi, sicurezza e blocchi.
- `states.yaml`: tassonomia tecnica degli stati del task.
- `workflows.yaml`: workflow pilota `issue-to-draft-pr`.
- `prompts/`: prompt minimi per analisi, implementazione e revisione.

## Incluso

- ruoli attivi: Codex, Claude, Orchestrator, Human Approver;
- policy per protezione di `main`, segreti, scope, branch e baseline;
- stati coerenti con la sezione 3.3 della governance;
- workflow dichiarativo fino alla draft PR e alla revisione;
- prompt testuali per agenti, senza integrazione API.

## Escluso

- merge automatico;
- deploy;
- GitHub Actions;
- webhook;
- API OpenAI, Anthropic, Claude o GitHub;
- database;
- dashboard;
- metriche;
- supporto multi-repository;
- nuovi ruoli non approvati;
- modifiche a codice applicativo, infrastruttura o dipendenze.

## Modifica della foundation

Ogni modifica a questa cartella deve passare da branch dedicata, pull request, revisione indipendente e approvazione umana. Nessun agente puo modificare `main` o fare merge.

## Prossimo step previsto

Dopo approvazione della foundation v0.1, il prossimo step sara usare questi file come base per una prima issue pilota controllata, mantenendo il merge fuori da qualunque automazione.
