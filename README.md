# els-exchange

Spazio di passaggio temporaneo per la validazione esterna di documenti e decisioni.

## Cos'è

Questo repository esiste solo per rendere leggibili, ad agenti AI esterni senza accesso ai repository privati, copie temporanee di documenti che vivono altrove. **Non è la fonte di verità.**

- `els-platform` (privato) resta la fonte di verità per tutto ciò che riguarda l'Orchestrator e il progetto operativo.
- `human-in-the-field` (privato) resta la fonte di verità per tutto ciò che riguarda HITF.

Ogni file presente qui è un **duplicato**, copiato manualmente da uno dei due repository privati al momento in cui serve una lettura o una validazione da parte di un agente esterno che non ha accesso diretto. Non va modificato qui: le modifiche vanno fatte nel repository di origine e poi ricopiate, se serve ancora una validazione.

## Struttura

- `orchestrator/` — duplicati di documenti/decisioni Orchestrator (origine: `els-platform`), destinati alla lettura da parte di Claude per validazione esterna.
- `hitf/` — duplicati di documenti/decisioni HITF (origine: `human-in-the-field`), destinati alla lettura da parte di GPT per validazione esterna.

## Regola di igiene

I file qui presenti vanno **cancellati periodicamente** dopo che la validazione per cui sono stati copiati è conclusa. Questo repository non è pensato per accumulare storia o archivio: è un canale di passaggio, non un archivio.

Prima di copiare un documento qui, verificare che non contenga dati personali, dati cliente, prezzi, credenziali, token, endpoint interni, percorsi locali o altro materiale sensibile — il repository è **pubblico**.
