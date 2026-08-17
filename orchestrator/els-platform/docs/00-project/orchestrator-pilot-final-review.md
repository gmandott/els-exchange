<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/orchestrator-pilot-final-review.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Chiusura Formale del Pilota Orchestrator

**Stato**: APPROVATO da Human Approver
**Data**: 21 luglio 2026
**Contatore finale**: 10/10 attività completate
**Finestra pilota**: 16-20 luglio 2026 (4 giorni, ben entro i 30 previsti)

---

## Decisione ufficiale

> La prima fase del pilota Orchestrator è approvata come validazione riuscita del processo manuale di autorizzazione, controllo dello scope, revisione indipendente, attestazione pre-merge e registrazione post-merge su attività documentali e procedurali.
>
> I gap rilevati in PILOT-005 e PILOT-006 sono riconosciuti come evidenze positive dell'efficacia del sistema di revisione e non vengono riclassificati retroattivamente come successi.
>
> La validazione non si estende ancora allo sviluppo applicativo reale, all'efficienza operativa, alla scalabilità, alla gestione di una reale espansione di scope, a un disaccordo formale con arbitrato umano, o all'idempotenza davanti a comandi duplicati o obsoleti.
>
> PRACT-001, PRACT-002 e PRACT-003 sono candidate alla formalizzazione, previa matrice di copertura che eviti duplicazioni normative e introduca il principio di evidenza minima sufficiente con tutela dei dati sensibili.
>
> PRACT-008 resta attiva e invariata.
>
> PRACT-009 resta `proposed / advisory / warning` fino a una nuova applicazione reale.
>
> Non è autorizzata in questa fase l'implementazione operativa completa di ORCH-003.
>
> `aidos-vision.md` non viene approvato come documento normativo.
>
> La fase successiva dovrà introdurre percorsi graduati per rischio, metriche di efficienza e una prima vertical slice di codice applicativo reale, piccola, reversibile e coperta da test.
>
> Ogni successiva modifica al repository richiederà un task e un'autorizzazione specifici.

---

## 1. Cosa il pilota ha dimostrato

Dieci attività completate (più OPS-001, fondazione tecnica esclusa dal conteggio):

| Pilot | Issue/PR | Oggetto | Esito |
|---|---|---|---|
| OPS-001 | #9 / #11 | CI `pr-validation` | Completato dopo 4 correzioni |
| PILOT-001 | #12 / #13 | Template PR | Pulito |
| PILOT-002 | #14 / #15 | Registro pratiche (PRACT-001-007) | Pulito dopo correzioni |
| PILOT-003 | #16 / #17 | Scrittura scoped `apps/**` | Pulito |
| PILOT-004 | #18 / #19 | Promozione PRACT-006/007 | Pulito, primo diff `M` |
| PILOT-005 | #20 / #21 | Introduzione PRACT-008 | **AUDIT GAP** — specifica incompleta |
| PILOT-006 | #22 / #23 | Rafforzamento PRACT-008 | **AUDIT GAP** — sequenza saltata |
| PILOT-007 | #24 / #25 | Test flusso pre-merge | **TEST PASSED** |
| PILOT-008 | #26 / #27 | Promozione PRACT-008 + template | Pulito |
| PILOT-009 | #28 / #29 | Gestione scope expansion | Pulito — `NO SCOPE EXPANSION REQUESTED` |
| PILOT-010 | #30 / #31 | Protocollo di disaccordo | Pulito — `NO SUBSTANTIVE DISAGREEMENT` |

**I due gap non sono stati nascosti in un bilancio genericamente positivo.** Hanno dimostrato che il revisore indipendente può trovare difetti non dichiarati dall'esecutore, che una specifica formalmente rispettata può essere comunque insufficiente, e che una correzione tecnica corretta non basta se la sequenza temporale del controllo è sbagliata. I quattro successi consecutivi che sono seguiti hanno valore proprio perché sono arrivati dopo questi due gap, non perché il processo sia stato pulito fin dall'inizio.

### Capacità validate

- Allowlist granulari per file e campo
- Comportamento fail-closed su ambiguità
- Distinzione fra revisore indipendente e registrante GitHub
- Attestazione riferita a un HEAD SHA esatto, invalidata da nuovi commit
- Separazione Stage 1 / Stage 2 / Stage 3 con arresti espliciti
- Merge esclusivamente umano
- Verifica post-merge
- Registrazione onesta degli audit gap, mai sanati retroattivamente
- Esiti non forzati (`NO SCOPE EXPANSION REQUESTED`, `NO SUBSTANTIVE DISAGREEMENT`) riconosciuti come validi

### Capacità non ancora testate

- Estensione di scope realmente richiesta, autorizzata e ripresa nello stesso task
- Disaccordo formale con arbitrato umano effettivo
- Sviluppo applicativo reale (nessun file sotto `apps/commerce`, `apps/admin`; `packages/**` resta vuoto)
- Gestione di test/lint/build falliti su codice reale
- Dipendenze fra più file di codice, regressioni, rollback applicativo
- **Idempotenza**: comportamento del sistema davanti a un comando duplicato, ritardato, o reso obsoleto dallo stato GitHub nel frattempo avanzato. Comportamento atteso per la fase successiva: `STALE COMMAND — CURRENT STATE ALREADY ADVANCED`, sola lettura, nessuna scrittura, nessun falso audit gap.

---

## 2. Pratiche del registro

| Pratica | Stato | Decisione |
|---|---|---|
| PRACT-001 (contenuto grezzo) | active/blocked | Mantenere. Candidata a formalizzazione con **evidenza minima sufficiente**, non file integrale sempre — principio di proporzionalità e redazione dei dati sensibili da introdurre nella formalizzazione. |
| PRACT-002 (allowlist esplicita) | active/blocked | Mantenere. Formalizzazione da fare mappando ciò che già esiste in `AGENTS.md`/`policies.yaml`, senza creare una seconda copia normativa. |
| PRACT-003 (timestamp autoritativo) | active/blocked | Mantenere. Candidata a formalizzazione esplicita della fonte temporale e delle regole di conversione. |
| PRACT-004 (riconferma correzioni) | active/changes-required | Mantenere invariata. |
| PRACT-005 (distinzione skip/blocco) | active/changes-required | Mantenere invariata. |
| PRACT-006 (revisione dove vive l'oggetto) | active/warning | **Da valutare l'innalzamento a `changes-required`** — protegge la traccia condivisa e verificabile sull'oggetto GitHub, senza dipendere dalle conversazioni esterne. |
| PRACT-007 (dichiarazione negativa scope) | active/warning | Mantenere `warning` — lo scope resta comunque verificabile via `git diff`/API indipendentemente dalla dichiarazione testuale. |
| PRACT-008 (attestazione pre-merge) | active/blocked | **Mantenere invariata.** Pratica meglio validata del pilota: due gap reali, correzione della specifica, quattro test superati consecutivamente. |
| PRACT-009 (integrità pubblicazione) | proposed/advisory | **Non promuovere.** Nata da un solo ciclo di convergenza, senza un secondo caso reale di applicazione preventiva del metodo prescritto (`--body-file`, verifica `body_match=exact`). |

Nessuna pratica da ritirare.

---

## 3. Peso operativo: efficacia dimostrata, efficienza non misurata

Il processo a tre stage ha dimostrato accuratezza — non sostenibilità economica od operativa. Pacchetti oltre mille righe, molteplici autorizzazioni e lunghe catene di verifica sono giustificati in fase di validazione, ma non possono diventare il costo standard per ogni modifica, incluse quelle a rischio minimo.

### Percorsi graduati per rischio (da introdurre nella fase successiva)

**Percorso documentale minimo** (README, copy, registro):
allowlist → diff completo → verifica contenuto → review indipendente → attestazione → merge umano. Pacchetto ridotto alle evidenze strettamente necessarie.

**Percorso applicativo ordinario** (codice a rischio limitato):
requisito → file e comportamento autorizzati → test/lint/build pertinenti → diff e file finali → review tecnica → attestazione sull'HEAD → merge umano.

**Percorso elevato** (infrastruttura, sicurezza, autenticazione, dati, pagamenti, deploy):
pacchetto completo → autorizzazioni granulari → analisi del rischio → piano di rollback → test estesi → più controlli indipendenti → eventuale approvazione umana aggiuntiva.

La classificazione del rischio resta manuale in questa fase — non delegata a un meccanismo automatico (`ORCH-003`).

### Metriche minime da introdurre nella fase successiva

- Tempo totale per task
- Tempo umano richiesto (Human Approver)
- Numero di passaggi e autorizzazioni
- Cicli di correzione
- Dimensione del pacchetto
- Controlli duplicati
- Tempo dalla prima autorizzazione al merge
- Errori realmente intercettati rispetto ai controlli eseguiti

---

## 4. ORCH-003: NO-GO per l'automazione operativa

`.orchestrator/**` contiene già stati, transizioni, access matrix e limiti di iterazione — ma restano prevalentemente dichiarativi, mai esercitati in pratica su un caso applicativo reale. Il disaccordo testato in PILOT-010 è stato un confronto leggero (classificazione indipendente → confronto), non il protocollo completo con limite di cicli ed escalation automatica concepito per `ORCH-003`.

**Decisione**: nessuna implementazione ora. È raccomandata una fase preparatoria non vincolante — definizione di input/output, mappatura delle pratiche già validate, elenco dei punti che devono restare umani, casi di errore, requisiti di audit — avviabile soltanto con task e autorizzazione separati. Nessun Policy Gate automatico finché non esiste un caso applicativo reale concluso.

---

## 5. `aidos-vision.md`: rinviato come documento normativo

Tutti i dieci pilot sono stati meta-lavoro sul processo — mai una riga di codice applicativo reale. La visione AIDOS fa affermazioni su come il sistema gestirà lo sviluppo reale di funzionalità, affermazioni oggi senza riscontro empirico. Una bozza esplicitamente non vincolante è raccomandabile, ma anche la sua stesura andrebbe avviata soltanto con un task e un'autorizzazione dedicati, non come conseguenza automatica di questo documento. Il documento ufficiale attende: una modifica reale di codice, una review tecnica vera, test applicativi, almeno una correzione richiesta dal revisore, un nuovo HEAD revisionato, un merge riuscito senza audit gap.

---

## 6. Formalizzazione di PRACT-001-003: matrice di copertura

| Pratica | Regola già presente altrove | Gap normativo | Destinazione |
|---|---|---|---|
| PRACT-001 | Parziale | Standard di evidenza minima sufficiente | Governance / prompt di revisione |
| PRACT-002 | Sostanzialmente presente in `AGENTS.md`/`policies.yaml` | Provenienza, validità e granularità dell'autorizzazione | Governance / policies |
| PRACT-003 | Assente o implicita | Fonte temporale autoritativa e regole di conversione | Governance |

La formalizzazione dovrà evitare duplicazioni: nel registro resta la scheda operativa, nella governance entra la regola normativa sintetica con rimando esplicito al registro. Il campo `Formalizzata in` dovrà indicare riferimento preciso a sezione e file, non un rimando generico.

---

## 7. Identity attribution gap

Resta backlog a priorità medio-bassa, non bloccante. Il processo distingue correttamente revisore indipendente, registrante GitHub e account tecnico nel contenuto — ma l'attribuzione nativa GitHub resta unificata su `github-account-redacted`. Non invalida l'audit (la provenienza è comunque registrata nel testo), ma limita la forza dell'attribuzione automatica. Da affrontare eventualmente in una fase di automazione futura (account tecnico o GitHub App dedicata).

---

## 8. README delle pratiche: fotografia storica preservata

Il README contiene intenzionalmente la fotografia datata alla conclusione di PILOT-008 (`8/10`). Non va sostituita: la soluzione corretta è aggiungere una nuova sezione datata di chiusura che documenti l'esito finale (`10/10`) e il risultato della revisione formale, preservando la fotografia precedente come record storico immutabile — coerente con PRACT-003 applicata alla propria conseguenza logica.

---

## 9. Rischi residui dichiarati

- Separazione dei ruoli non garantita da identità GitHub distinte (vedi punto 7).
- Processo ancora manuale e non misurato in termini di costo/efficienza.
- Nessuna prova su codice applicativo reale.
- Scope expansion e disaccordo formale solo parzialmente validati (esiti di convergenza/non-necessità, non i percorsi di divergenza reale).
- Idempotenza davanti a comandi obsoleti o duplicati non testata.

---

## 10. Sequenza approvata per la fase successiva

1. **Task di chiusura formale** (questo documento + aggiornamento README con nuova sezione datata `10/10`, preservando `8/10` storico) — breve, non un nuovo ciclo di governance.
2. **Avvio del Project Discovery per il portale ELS** — le seguenti sono aree da verificare ed esplorare durante la Discovery, non requisiti o funzionalità già approvati: obiettivo commerciale, utenti (centri estetici, agenti, amministrazione), catalogo/listini riservati, B2B, ordini, pagamenti, agenti/provvigioni, promozioni, CRM, migrazione, requisiti legali/fiscali/privacy, priorità MVP. La Discovery stessa dovrà stabilire quali di questi elementi sono effettivamente in scope e con quale priorità.
3. **Valutazione tecnica di Medusa** — esito `GO` / `GO con condizioni` / `NO-GO`, basato sui requisiti reali ELS, non sull'attualità tecnologica dello stack.
4. **Prima vertical slice applicativa reale** — piccola, reversibile, testabile, dati fittizi, senza pagamenti reali. Da isolare come sotto-pezzo minimo di un flusso più ampio (es. solo logica di prezzo riservato, non l'intero percorso autenticazione→prezzo→carrello in un solo task).
5. **Riduzione del ruolo di trasporto manuale** — schede di task unificate (issue GitHub con requisito, decisioni, allowlist, stato, evidenze, review, autorizzazione richiesta), aggiornate da Codex, lette direttamente da Claude e ChatGPT. Human Approver riceve richieste sintetiche: approva il requisito, scegli fra opzioni, autorizza la pubblicazione, esegui il merge — non più il trasporto di messaggi lunghi fra agenti.

Il processo diventa strumento al servizio del portale ELS, non il progetto stesso.
