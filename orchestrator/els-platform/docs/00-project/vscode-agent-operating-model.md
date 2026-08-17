<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/vscode-agent-operating-model.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# VS Code Agent Operating Model

## Scopo

VS Code come cockpit operativo del team multi-agente, con massima autonomia compatibile con reversibilità, sicurezza e governance.

## Relazione con la governance esistente

Questo documento non sostituisce `docs/00-project/ai-development-operating-model.md`. Lo specializza esclusivamente per il funzionamento operativo del cockpit VS Code e del team multi-agente.

Resta subordinato alle governance e alle pratiche già approvate e attive nel repository, inclusa PRACT-008 e il registro in `docs/00-project/practices/registry.md`.

In caso di conflitto tra questo documento e la governance già approvata, prevale quest'ultima, salvo successiva modifica esplicitamente autorizzata.

La tassonomia degli stati già definita nell'AI Development Operating Model (sezione 3.3) resta invariata e non viene ridefinita da questo documento.

La regola già vigente sul disaccordo tra agenti resta applicabile: è consentito il ciclo di replica previsto dalla governance esistente; se il disaccordo permane dopo tale ciclo, si procede secondo l'escalation prevista. EV-2 si applica solo a un conflitto non risolto dopo questo passaggio, non al primo disaccordo.

## Ruoli

### GPT

- strategia;
- scope;
- governance;
- supporto alle decisioni;
- consolidamento requisiti.

### Codex

- implementazione;
- codice, test e documentazione tecnica;
- branch/commit/draft PR;
- segnale HITF non bloccante quando rilevante.

### Claude Code

- validazione tecnica indipendente sul repository;
- verifica di codice, diff, test, architettura e conformità allo scope.

### Claude esterno

- validazione indipendente esterna, invocata esclusivamente quando ricorre uno dei trigger EV-1…EV-7 definiti nel presente documento.

### Human Approver

- approvazione umana finale nei casi previsti;
- merge;
- decisioni strategiche;
- azioni irreversibili;
- pubblicazioni esterne.

### VS Code

- cockpit operativo;
- coordina repository, terminale, agenti, diff, test e sessioni;
- non è un decisore.

### GitHub

- fonte di verità e tracciabilità.

### Human in the Field

- sistema satellite;
- riceve segnali non bloccanti;
- non modifica lo stato tecnico delle attività.

## Classificazione operativa

### VERDE — autonomia

L'agente procede senza autorizzazione quando il lavoro è nello scope approvato, reversibile, confinato al branch/worktree, senza effetti esterni, senza costi e senza esposizione di dati sensibili.

Includere:

- lettura/analisi repository;
- documentazione;
- modifiche su branch;
- bug fix nello scope;
- test;
- lint/typecheck/build;
- refactoring senza variazione di contratti;
- creazione branch;
- preparazione commit;
- draft PR;
- analisi alternative;
- debito tecnico;
- correzione errori propri;
- segnale HITF non bloccante;
- dipendenze di sviluppo locali standard, gratuite e reversibili.

Confine documentazione VERDE/GIALLO:

- documentazione operativa, esplicativa o di supporto che non modifica una fonte di verità = VERDE;
- requisiti, decisioni/ADR, governance, policy e altri documenti che costituiscono fonte di verità = GIALLO.

Non ogni modifica Markdown diventa GIALLO.

Principio:

se può essere annullato con Git, non costa, non espone dati e non cambia produzione o strategia, normalmente non richiede Human Approver.

### GIALLO — autonomia + validazione indipendente

L'agente completa il lavoro, poi il risultato viene validato indipendentemente prima del passaggio successivo rilevante.

Includere:

- funzionalità significative;
- bug fix con variazioni comportamentali;
- cambi architetturali;
- dipendenze rilevanti;
- schema/migrazioni database;
- autenticazione/autorizzazione;
- API e integrazioni;
- CI/CD;
- documenti fonte di verità;
- governance;
- refactoring significativo;
- infrastruttura;
- modifiche trasversali;
- disaccordi tra agenti.

Workflow:

implementazione → automated checks → draft PR → Claude Code review → eventuali correzioni → eventuale Claude esterno secondo EV-1…EV-7 → decisione umana se prevista.

### ROSSO — approvazione Human Approver obbligatoria

L'agente può analizzare e preparare, ma non eseguire l'azione finale.

Includere:

- merge su main;
- deploy produzione;
- cancellazioni irreversibili;
- modifica/cancellazione dati reali;
- dati personali/clienti;
- gestione/esposizione segreti;
- policy di sicurezza;
- apertura pubblica di repository/risorse;
- costi/acquisti/abbonamenti;
- lock-in strategico;
- ampliamento sostanziale scope;
- cambi governance;
- decisioni commerciali/contrattuali;
- comunicazioni esterne;
- pubblicazioni HITF/social/sito;
- impatto reputazionale;
- conflitti non risolti tra validatori.

### NERO — vietato

- pubblicazione di segreti;
- bypass intenzionale dei controlli;
- modifica produzione fuori scope;
- occultamento/riscrittura della cronologia per nascondere errori;
- trasferimento dati sensibili verso servizi non autorizzati;
- azioni illegali o contrarie alla governance.

## Escalation

Gli agenti non devono interrompere Human Approver alla prima incertezza.

Prima devono:

1. analizzare;
2. consultare le fonti di verità;
3. tentare una soluzione reversibile quando consentito;
4. coinvolgere il reviewer appropriato;
5. escalare solo quando rimane una vera decisione umana.

L'escalation deve contenere:

- problema;
- opzioni realistiche;
- raccomandazione;
- motivazione;
- rischio che rende necessaria l'approvazione.

## HITF

Alla conclusione di attività potenzialmente interessanti, Codex/Claude Code possono creare un segnale HITF leggero e non bloccante secondo la governance del repository Human in the Field.

HITF:

- non blocca la chiusura tecnica;
- non autorizza pubblicazione;
- non sostituisce la governance del progetto operativo.

## Claude esterno — Validazione indipendente

Claude esterno non è un reviewer di routine. Non viene invocato per ogni task
completato, ma solo quando si verifica almeno una delle condizioni seguenti.

### Trigger (EV-1…EV-7)

| Codice | Condizione |
|---|---|
| EV-1 | Modifica a governance, policy o documento fonte di verità |
| EV-2 | Conflitto non risolto tra Codex e Claude Code |
| EV-3 | Decisione classificata ROSSA nel presente modello |
| EV-4 | Impatto multi-repository o multi-sistema |
| EV-5 | Chiusura di una specifica vincolante per il lavoro successivo |
| EV-6 | Pubblicazione esterna o decisione con impatto reputazionale |
| EV-7 | Escalation esplicita di Claude Code: il problema non è solo tecnico, ma anche di coerenza, rischio o completezza |

**EV-1**: si applica a modifiche sostanziali di governance, policy o documenti fonte di verità. Correzioni tipografiche, formattazione e modifiche puramente editoriali che non cambiano significato o comportamento non attivano EV-1.

**EV-6**: identifica esplicitamente pubblicazioni esterne o decisioni reputazionali ai fini della validazione e della tracciabilità. Può coesistere con EV-3 quando la stessa attività è già classificata ROSSA: in tal caso non richiede una validazione separata.

Se nessuna condizione EV è verificata, Claude esterno non viene coinvolto.
Human Approver può inoltre richiedere direttamente una validazione esterna quando
identifica personalmente una condizione EV, anche in assenza di segnalazione
da parte degli agenti.

### Chi prepara il pack

L'External Validation Pack è predisposto dall'agente che rileva per primo
la condizione EV (Codex o Claude Code, indistintamente).

Se il trigger è EV-2 (conflitto tra agenti), il pack deve riportare in modo
neutrale entrambe le posizioni, senza che uno dei due agenti in conflitto
decida quale sia corretta.

### Struttura del pack (minima, non un documento pesante)

- trigger EV di riferimento;
- oggetto della decisione;
- scope;
- file/diff/riferimenti rilevanti;
- conclusione dell'implementatore;
- conclusione del reviewer, se già disponibile;
- eventuali punti controversi;
- domanda o decisione richiesta a Claude esterno.

### Trasferimento

Il trasferimento del pack verso Claude esterno avviene solo previa
approvazione esplicita di Human Approver. Nessun pack viene trasferito senza
questa autorizzazione.

**Stato attuale:** ad oggi non esiste un meccanismo tecnico che permetta al
cockpit operativo (VS Code) di eseguire il trasferimento in modo assistito o
automatico. Il trasferimento avviene quindi tramite copia/incolla manuale
da parte di Human Approver — non come fallback eccezionale, ma come processo
standard nella presente versione del modello.

**Evoluzione futura (non implementata ora):** potrà essere valutato un
meccanismo dedicato — ad esempio un tool/MCP `request_external_validation` —
che prepari il pack, richieda l'approvazione di Human Approver, esegua il
trasferimento e riporti l'esito nel workspace. Da introdurre solo se l'uso
reale del processo manuale ne dimostrerà la necessità, non anticipatamente.

### Esiti ammessi

Claude esterno restituisce uno tra:

- `VALIDATO`
- `VALIDATO CON PERIMETRO`
- `VALIDATO CON RISERVE`
- `NON VALIDATO`

con un massimo di tre rilievi reali a supporto dell'esito.

Ogni validazione deve dichiarare il proprio perimetro effettivamente verificato.
Se una parte dell'esito dipende da verifiche svolte da altri agenti o da fonti
non accessibili direttamente, l'esito è `VALIDATO CON PERIMETRO` e deve
indicare esplicitamente la dipendenza.

- `VALIDATO CON PERIMETRO` = esito positivo con limite dichiarato sul perimetro effettivamente verificato;
- `VALIDATO CON RISERVE` = il perimetro è stato verificato, ma rimangono rilievi non bloccanti.

### Decisione finale

L'esito di Claude esterno non è vincolante in automatico. La decisione
finale resta sempre di Human Approver, coerentemente con il principio generale
del presente modello per le attività classificate ROSSE.

### Tracciabilità

Poiché GitHub è la fonte di verità del progetto, ogni validazione esterna
lascia una traccia minima:

- se esiste una PR collegata alla decisione, la traccia è registrata nella
  PR stessa;
- in assenza di una PR, la traccia è registrata in
  `docs/00-project/external-validation-log.md`.

Formato della traccia (una riga per validazione):

`data | trigger EV-x | oggetto | esito Claude esterno | decisione finale Human Approver`

## Principio generale

Massima autonomia nell'esecuzione.
Validazione indipendente dove esiste rischio concreto.
Intervento umano concentrato sulle decisioni irreversibili, strategiche o reputazionali.
