# orchestrator/

Duplicati temporanei di documenti e decisioni Orchestrator, copiati da `els-platform` (repository privato, fonte di verità) per essere letti da Claude ai fini di validazione esterna.

- Non è la fonte di verità: eventuali correzioni vanno fatte nel documento originale su `els-platform`, non qui.
- Cancellare i file qui presenti dopo che la validazione per cui sono stati copiati è conclusa.
- Non copiare qui dati personali, dati cliente, prezzi, credenziali, token, endpoint interni o percorsi locali — questo repository è pubblico.

## Pacchetto corrente per validazione Claude

Duplicati pubblici sanificati copiati da `els-platform` sotto `orchestrator/els-platform/`:

- `AGENTS.md` — regole operative generali per agenti e sviluppatori nel repository origine.
- `.orchestrator/README.md` — panoramica della foundation dichiarativa Orchestrator v0.1.
- `.orchestrator/agents.yaml` — ruoli, responsabilità e limiti degli agenti.
- `.orchestrator/policies.yaml` — policy operative, sicurezza, access matrix, comandi e directory.
- `.orchestrator/states.yaml` — tassonomia tecnica degli stati.
- `.orchestrator/workflows.yaml` — workflow dichiarativo issue-to-draft-PR.
- `docs/00-project/ai-development-operating-model.md` — modello operativo e governance del pilota.
- `docs/00-project/vscode-agent-operating-model.md` — modello operativo del cockpit VS Code multi-agente e trigger di validazione esterna.
- `docs/00-project/orchestrator-pilot-final-review.md` — chiusura formale del pilota Orchestrator 10/10.
- `docs/00-project/practices/README.md` — guida al registro pratiche anti-errore.
- `docs/00-project/practices/registry.md` — pratiche consolidate e proposta PRACT-009.
- `docs/00-project/headroom-pilot-closure.md` — chiusura/parcheggio del micro-pilot Headroom come valutazione tecnica separata.

Sanificazione applicata: rimossi/generalizzati nomi personali, account GitHub, percorsi locali e riferimenti non necessari a domini/progetti pubblici operativi. Gli evidence pack Headroom non sono stati copiati perché contengono dettagli di run e percorsi locali.
