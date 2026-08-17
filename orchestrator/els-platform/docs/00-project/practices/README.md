<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/practices/README.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Registro vivo delle pratiche anti-errore

Questa cartella raccoglie pratiche operative nate da errori, quasi-errori o ambiguità realmente emerse nel progetto `els-platform`.

Il registro non sostituisce la governance ufficiale, `AGENTS.md` o `.orchestrator/**`. Serve a conservare memoria verificabile di pratiche utili prima che diventino regole formali o controlli tecnici.

## Stato del pilota Orchestrator

> Fotografia verificata alla conclusione di PILOT-008, il 20 luglio 2026.
> Questa sezione non è un contatore aggiornato automaticamente.

- Attività ufficiali completate: **8/10**.
- Attività residue prima della revisione: **2/10**.
- OPS-001 resta esclusa dal conteggio.
- Pratiche attive e richieste durante il pilota: **PRACT-001–PRACT-008**.
- PRACT-008 è stata validata con PILOT-007 e promossa a
  `active / required-for-pilot / blocked` con PILOT-008.
- Il registro completo e autoritativo è disponibile in
  [`registry.md`](./registry.md).
- La revisione del pilota scatta al raggiungimento di 10 attività oppure
  alla scadenza della finestra di 30 giorni, a seconda di quale condizione
  si verifica per prima.
- La finestra corrente termina il `2026-08-15T20:06:01+02:00`,
  corrispondente al `2026-08-15T18:06:01Z`.
- Il raggiungimento di `10/10` avvia una revisione e non approva
  automaticamente ORCH-003, `aidos-vision.md`, nuove pratiche o modifiche
  alla governance.

## File

- `registry.md`: registro delle pratiche approvate o proposte.

## Scopo

Il registro serve a:

- rendere visibili pratiche di verifica già imparate dal progetto;
- evitare che decisioni e correzioni restino solo nella cronologia delle conversazioni;
- permettere a Codex, Claude, ChatGPT, Human Approver e futuri collaboratori di proporre nuove voci;
- mantenere traccia delle pratiche superate senza cancellarne la storia.

## Stati

Ogni pratica può avere uno di questi stati:

- `proposed`: pratica proposta, non ancora vincolante;
- `active`: pratica approvata da Human Approver e applicabile secondo l'ambito indicato;
- `superseded`: pratica superata, mantenuta per memoria storica.

Questa versione del registro non ammette altri valori di stato.

## Effetto operativo

Ogni pratica indica anche il suo effetto operativo:

- `advisory`: orienta il lavoro, ma la mancata applicazione non blocca automaticamente il task;
- `required-for-pilot`: è richiesta durante il pilota Orchestrator;
- `formalized`: è stata recepita in una fonte normativa o tecnica più forte.

Questa versione del registro non ammette altri valori di effetto operativo.

## Esiti

Ogni pratica deve indicare uno di questi esiti se non viene rispettata:

- `blocked`: il task deve fermarsi finché manca evidenza o autorizzazione essenziale;
- `changes-required`: il task può proseguire solo dopo una correzione puntuale;
- `warning`: il rischio va dichiarato, ma non blocca automaticamente il task.

Questa versione del registro non ammette altri valori di esito.

## Fonte di verità

Prima della formalizzazione, `registry.md` è la fonte di verità operativa per la pratica descritta.

Dopo la formalizzazione, la fonte primaria diventa il documento o meccanismo indicato nel campo `Formalizzata in`.

Il registro resta comunque la memoria storica dell'origine della pratica.

## Formalizzazione

Una voce formalizzata:

- conserva lo stesso ID;
- assume `Effetto operativo: formalized`;
- indica percorso e, quando possibile, sezione della fonte normativa nel campo `Formalizzata in`;
- conserva episodio di origine e provenienza;
- non duplica integralmente il testo normativo.

Ogni Pull Request che modifica una regola formalizzata deve dichiarare se richiede:

- aggiornamento di stato, riferimento o data della voce nel registro;
- oppure nessun aggiornamento dei metadati del registro.

Il testo normativo non deve essere mantenuto in due copie parallele.

## ID e storico

Gli ID usano il formato `PRACT-NNN`.

Gli ID sono immutabili:

- non vengono riutilizzati;
- non vengono rinumerati;
- restano associati alla stessa pratica anche se la pratica cambia stato.

Il registro è append-only per le nuove voci.

Le voci esistenti possono essere aggiornate tramite Pull Request, conservando ID, episodio di origine e storico Git.

## Proposta di nuove voci

Chiunque può proporre una voce quando nota un pattern di errore reale non ancora coperto.

Una proposta deve includere almeno:

- errore intercettato;
- episodio di origine verificabile;
- istruzione operativa concreta;
- evidenza minima richiesta per verificarne il rispetto;
- esito previsto se non viene rispettata.

Il campo `Proposta da` può contenere un singolo proponente, per esempio `Codex`, `Claude`, `ChatGPT`, `Human Approver` o `altro`. Quando la proposta nasce da più partecipanti in una stessa discussione, elencarli tutti separati da virgola. Non è necessario forzare un singolo proponente quando non corrisponde a come la pratica è realmente nata.

## Approvazione umana

Nessuna nuova voce diventa `active` senza approvazione esplicita di Human Approver.

Gli agenti possono proporre inserimenti, revisioni o superamenti, ma non possono approvarli autonomamente.

## Superseded

Chiunque può proporre che una voce passi a `superseded`.

Solo Human Approver può approvare il passaggio a `superseded`.

Una voce `superseded`:

- non viene cancellata;
- non viene rinumerata;
- indica perché è superata;
- indica da cosa è sostituita;
- conserva data e approvazione.

## Autorizzazione alla scrittura

L'approvazione concettuale di una pratica o del registro non autorizza automaticamente modifiche al repository.

Ogni scrittura richiede un task operativo esplicito con scope e autorizzazioni definite.

## Revisione periodica

Il registro va rivisto alla prima delle seguenti scadenze:

- completamento di 10 issue del pilota;
- 30 giorni dall'avvio della finestra pilota.

La finestra pilota corrente è stata avviata dall'evento GitHub `ai-ready labeled` sulla issue #12.

## Fuori scope

Questo registro non introduce:

- automazioni;
- workflow GitHub Actions;
- modifiche a ruleset o branch protection;
- nuovi permessi;
- dipendenze;
- obblighi tecnici non già indicati nelle singole voci.

## Chiusura del pilota — 10/10 (21 luglio 2026)

Il pilota Orchestrator si è concluso con 10/10 attività completate il 20 luglio 2026. La fotografia storica a `8/10` sopra riportata resta invariata come registrazione del proprio momento.

Decisione formale e analisi completa: [`docs/00-project/orchestrator-pilot-final-review.md`](../orchestrator-pilot-final-review.md).

Sintesi: pilota approvato come validazione riuscita del processo manuale di autorizzazione, revisione indipendente e controllo pre-merge su attività documentali e procedurali. Non ancora esteso a sviluppo applicativo reale. PRACT-008 resta attiva e invariata. PRACT-009 resta `proposed / advisory / warning`. ORCH-003 e `aidos-vision.md` rinviati.
