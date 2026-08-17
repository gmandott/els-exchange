<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/ai-development-operating-model.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# AI Development Operating Model v1

Documento di governance per la collaborazione tra umano, agenti AI (ChatGPT/Codex, Claude) e GitHub nello sviluppo software.

- **Stato**: approvato per sperimentazione controllata
- **Ambito**: repository pilota `els-platform` per ELS public site
- **Versione**: 1.0
- **Autorità di approvazione**: Human Approver
- **Revisione prevista**: dopo le prime 10 issue completate o dopo 30 giorni, a seconda di quale condizione si verifichi prima

---

## 1. Modello operativo

### 1.1 Ruoli

| Ruolo | Responsabilità | Può modificare main? | Può fare merge? |
|---|---|---|---|
| Umano (Human Approver) | Priorità, obiettivi, approvazione finale, arbitro in caso di conflitto | No, opera via PR come chiunque altro | Sì, unico ruolo autorizzato |
| ChatGPT/Codex | Analisi operativa, pianificazione, implementazione | No | No |
| Claude | Revisione critica, architettura, sicurezza, controllo delle modifiche | No | No |
| GitHub | Memoria ufficiale, tracciabilità, ciclo di vita del lavoro | — | — |
| Orchestrator | Assegna compiti, applica regole, controlla stato, blocca azioni non consentite | No | No |

**Regola cardine: nessun agente può modificare `main` direttamente.** Ogni modifica passa da branch → PR → revisione → approvazione umana → merge manuale.

"Merge manuale" significa che **il merge è approvato ed eseguito direttamente dall'umano tramite GitHub** — non che l'orchestrator lo esegue dopo un'approvazione testuale. Orchestrator e agenti non possiedono permessi di merge. Un divieto scritto solo in `policies.yaml` non basta: va applicato anche a livello di permessi GitHub. Servono, prima di aprire il pilota:

- branch protection su `main`;
- pull request obbligatoria per ogni modifica;
- almeno un'approvazione umana richiesta;
- status check obbligatori (test, lint, build) prima che la PR sia mergeable;
- divieto di force push su `main`;
- divieto di eliminazione del branch protetto;
- nessun token assegnato agli agenti con permesso admin o possibilità di bypassare le protezioni.

### 1.2 Regole di escalation

Regole esplicite:

- **Divergenza tecnica (stile, refactoring, scelta di libreria)**: il revisore (Claude) può bloccare una modifica non corretta, ma non impone automaticamente la propria soluzione — può sbagliare quanto chi implementa. La PR resta bloccata finché l'osservazione del revisore non viene risolta. Codex può accettare la correzione oppure motivare tecnicamente una soluzione alternativa. È consentito un solo ciclo di replica. Se il disaccordo permane, o se la divergenza tocca criteri di accettazione, architettura, sicurezza o costi, decide l'umano.
- **Divergenza su sicurezza, dati sensibili, costi o modifiche ad architettura condivisa**: si ferma tutto, si esce dal flusso automatico e si passa all'umano. Nessuna euristica automatica decide su questi temi.
- **Un agente segnala ambiguità nell'issue** (non capisce cosa fare, o i criteri di accettazione sono contraddittori): il task torna in stato `needs-clarification`, l'orchestrator notifica l'umano, non si procede per tentativi.
- **Timeout o loop**: vedi sezione 4.4.

### 1.3 Output di questo step

- Questo documento come documento di governance.
- Tabella ruoli e permessi.
- Regole di escalation.
- Flusso standard richiesta → merge (sezione 3).

---

## 2. Standard dei repository

Struttura comune a ELS, Progetto B e progetti futuri:

```text
AGENTS.md
README.md
docs/
  00-project/
  decisions/
  specifications/
  operations/
.orchestrator/
  agents.yaml
  policies.yaml
  workflows.yaml
  prompts/
.github/
  ISSUE_TEMPLATE/
  pull_request_template.md
  workflows/
```

> Nota per il repository pilota: la struttura documentale esistente usa directory numerate, tra cui `docs/07-decisions/`. Il blueprint sarà adattato senza rinominare cartelle esistenti finché non verrà approvata una migrazione dedicata.

### 2.1 Contenuto minimo di ciascun file chiave

- **`AGENTS.md`**: regole generali di collaborazione — chi fa cosa, tono delle revisioni, cosa non deve mai fare un agente in questo repository (es. toccare `.env`, cancellare migrazioni, modificare CI senza revisione umana).
- **`policies.yaml`**: limiti operativi (vedi 2.2 — qui va anche la gestione permessi/segreti, non solo i limiti di costo).
- **`workflows.yaml`**: passaggi da seguire, mappati 1:1 sul flusso della sezione 3.
- **`docs/07-decisions/`** nel pilota, equivalente a **`docs/decisions/`** nel blueprint: Architecture Decision Records (ADR). Ogni decisione tecnica rilevante è un file, non una riga di chat. Gli agenti leggono qui, non ricostruiscono contesto dalla cronologia delle conversazioni.
- **`docs/specifications/`**: specifiche funzionali stabili, separate dalle issue, che sono operative e temporanee.

### 2.2 Permessi e segreti

Gli agenti che scrivono codice ed eseguono test hanno bisogno di accesso al runtime, ma non a tutto.

- Nessun agente ha accesso diretto a credenziali di produzione, chiavi API reali o ambienti live. Solo a un ambiente sandbox/staging con dati fittizi o anonimizzati.
- `policies.yaml` deve dichiarare esplicitamente quali variabili d'ambiente sono visibili agli agenti, quali comandi possono eseguire (es. `npm test` sì, `npm publish` no), quali directory sono in scrittura e quali in sola lettura.
- Qualunque azione che tocchi segreti, deploy o infrastruttura è automaticamente fuori dal perimetro automatizzabile e richiede intervento umano esplicito, indipendentemente da cosa dice il resto del workflow.

### 2.3 Output di questo step

Repository blueprint replicabile: ogni nuovo progetto parte con governance, documentazione e permessi AI già definiti dal primo commit.

---

## 3. Workflow pilota

Un solo flusso, completo e misurabile, su un solo repository: `els-platform`, piattaforma pilota di ELS public site.

```text
Issue con etichetta ai-ready
  → verifica leggibilità issue (criteri in 3.1)
  → controllo baseline (3.1bis)
  → analisi (Codex)
  → piano operativo (Codex)
  → creazione branch
  → implementazione (Codex)
  → test, lint, build automatici
  → draft pull request
  → revisione indipendente sulla draft PR (Claude)
  → [se servono modifiche: changes-requested → implementazione (Codex)]
  → [se conflitto: vedi 1.2 escalation]
  → approvazione umana
  → merge manuale
```

Questa sequenza risolve la contraddizione rilevata durante la revisione di `ORCH-001` / PR #6: nel flusso GitHub approvato, Claude revisiona la draft pull request usando diff, commenti e thread della PR. Se la revisione richiede modifiche, il task usa lo stato esistente `changes-requested` e torna a Codex prima di una nuova revisione o dell'approvazione umana.

### 3.1 Criteri di "issue sufficientemente chiara"

Checklist minima che l'orchestrator applica prima di assegnare l'issue a un agente:

- [ ] Contesto: cosa esiste oggi e perché va cambiato.
- [ ] Criteri di accettazione espliciti: non "migliora X", ma "X fa Y quando Z".
- [ ] Area funzionale, componente o modulo coinvolto, almeno indicativamente. L'indicazione puntuale dei file è richiesta solo quando esiste già un perimetro tecnico noto, o quando alcuni file devono essere esplicitamente esclusi — individuare i file esatti fa parte del lavoro dell'agente, non è un prerequisito per aprire l'issue.
- [ ] Nessuna dipendenza bloccante da un'altra issue non ancora chiusa.

Se manca anche uno di questi punti, tranne l'indicazione puntuale dei file che è opzionale, stato `needs-clarification`: non si procede. Questa checklist misura la chiarezza del bisogno, non la competenza tecnica di chi apre l'issue.

### 3.1bis Controllo baseline prima dell'implementazione

Prima che Codex inizi a lavorare, l'orchestrator esegue test, lint e build sul branch di partenza così com'è. I fallimenti già presenti sulla baseline vengono registrati e non attribuiti al task. Se la baseline non è verificabile, o presenta errori che impediscono di validare la modifica, il task passa a stato `blocked-by-baseline` invece di procedere: altrimenti Codex rischia di essere fermato per test che erano già rotti su `main` prima ancora di iniziare (vedi regola dei due fallimenti in 4.4).

### 3.1ter Estensione di perimetro durante il lavoro

Se durante l'implementazione l'agente scopre che servono file o componenti non previsti nell'issue originale, il task passa a stato `scope-expansion-requested`, l'attività si ferma e l'umano approva o rifiuta l'estensione. Non è necessario riscrivere l'issue: basta l'approvazione puntuale sull'estensione richiesta.

### 3.2 Vincoli operativi

- L'orchestrator limita file e aree modificabili in base a quanto dichiarato nell'issue: un agente non tocca file fuori dal perimetro assegnato senza una nuova autorizzazione.
- Merge automatico bloccato sempre, senza eccezioni, in questa fase pilota.

### 3.3 Tassonomia degli stati

Necessaria perché l'orchestrator agisca su stati definiti, non interpretando testo libero:

```text
draft
needs-clarification
ai-ready
in-analysis
in-development
in-review
changes-requested
scope-expansion-requested
blocked-by-baseline
stalled
awaiting-human-approval
completed
cancelled
```

### 3.4 Output di questo step

MVP funzionante su un solo repository, con dati reali di quante issue arrivano a draft PR, quante richiedono chiarimenti, quante vengono approvate senza modifiche.

---

## 4. Controllo, memoria e misurazione

Da introdurre dopo che il workflow pilota gira in modo stabile.

### 4.1 Memoria progettuale

- Decisioni (`docs/07-decisions/` nel pilota), convenzioni, errori già incontrati e architettura vengono letti dagli agenti a ogni task, non ricostruiti da conversazioni passate.

### 4.2 Controllo economico

- Costo massimo per attività.
- Numero massimo di iterazioni per task prima che venga escalato all'umano.
- Modelli utilizzabili per tipo di task (es. task semplici → modello più economico, revisione architetturale → modello più capace).

### 4.3 Controllo qualitativo

- Test obbligatori prima di aprire la draft PR.
- Soglie di rischio: per esempio una PR che tocca più di N file, o file critici, richiede doppia revisione.
- Limiti ai file modificati per singolo task.
- Revisione indipendente sempre presente, mai saltata per velocità.

### 4.4 Timeout e stati bloccati

- Ogni task ha un timeout massimo, espresso in tempo e numero di iterazioni. Superato il limite, il task passa automaticamente a stato `stalled` e notifica l'umano: non resta in loop silenzioso consumando costo.
- Un task che fallisce test due volte di fila su correzioni diverse va a revisione umana diretta, non a un terzo tentativo automatico. Questa regola si applica solo ai fallimenti introdotti dal task: i fallimenti già presenti sulla baseline, registrati in 3.1bis, non contano ai fini del conteggio.

### 4.5 Gestione del collo di bottiglia umano

Con un solo repository pilota, l'umano come unico approvatore funziona. Prima di estendere a più repository, va deciso:

- una soglia di PR/giorno oltre la quale si introduce un secondo approvatore umano, o approvazione automatica per categorie di rischio molto basso, per esempio modifiche alla sola documentazione;
- una vista aggregata (dashboard, sezione 4.6) che mostri PR in attesa per priorità, così l'approvazione umana resta uno scan rapido e non un collo di bottiglia che rallenta tutto il flusso.

### 4.6 Misurazione

Dashboard che risponde a:

- quale agente produce i risultati migliori (PR approvate senza modifiche / PR totali);
- quali tipi di attività possono essere ulteriormente automatizzati;
- dove si generano più errori o richieste di modifica;
- costo medio per attività, per tipo di task;
- tempo umano risparmiato rispetto a una baseline manuale.

---

## 5. Sequenza di attuazione

1. Governance (questo documento) — approvazione umana.
2. Standard dei repository (sezione 2) su `els-platform`.
3. Workflow pilota (sezione 3) su `els-platform`, con criteri di issue readiness e permessi/segreti già attivi dal giorno uno, non aggiunti dopo.
4. Controllo e scalabilità (sezione 4), inclusi timeout e gestione del collo di bottiglia umano, prima di estendere ad altri repository.

**Principio guida**: non si costruisce un orchestrator che fa tante cose. Si rende affidabile un solo processo, poi si replica su Progetto B e sui progetti successivi.

---

## Note per la revisione con Codex

Punti su cui vale la pena un confronto esplicito prima di implementare `.orchestrator/`:

- Le regole di escalation (1.2) sono compatibili con come Codex gestisce oggi i conflitti tra suggerimenti propri e revisioni esterne?
- I limiti in `policies.yaml` (2.2) su comandi eseguibili e directory in scrittura sono realizzabili con i permessi che Codex espone nell'ambiente in cui gira?
- La checklist di issue readiness (3.1) può essere applicata come check automatico prima di assegnare un task, o richiede un passaggio manuale nella fase pilota?
