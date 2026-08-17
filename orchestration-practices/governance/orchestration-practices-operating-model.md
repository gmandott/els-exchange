# Orchestration Practices — Operating Model

**Orchestration Practices**
Real work. Human decisions. Multi-agent coordination.

Versione: 0.1
Stato: pilota
Responsabile e approvatore finale: Gianluca

## Scopo

Orchestration Practices è un progetto indipendente che raccoglie, verifica e rende trasferibili pratiche reali di collaborazione tra persone e agenti AI: decisioni, responsabilità, passaggi di consegna, revisioni, errori, correzioni e risultati.

Questo documento definisce come Orchestration Practices raccoglie segnali dai progetti operativi, li seleziona e li trasforma in pratiche sanificate, revisionate e pubblicate solo con approvazione umana.

Orchestration Practices non sostituisce i progetti operativi e non diventa la loro fonte di verità. Le pratiche pubblicate derivano dall'esperienza reale, ma restano duplicati generalizzati e autonomi.

## Principi

* Orchestration Practices è un **modulo satellite e autonomo**: collegato ai progetti operativi come fonte di pratiche, ma non integrato nei loro workflow bloccanti.
* La valutazione Orchestration Practices alla chiusura di un'attività è **sempre non bloccante**: non ritarda, non condiziona e non richiede approvazione per la chiusura del lavoro operativo.
* Nessuna pratica viene pubblicata senza sanificazione, revisione indipendente e approvazione umana esplicita.
* Durante il pilota, Gianluca è l'unico responsabile della selezione delle pratiche e dell'approvazione finale.
* Codex coordina il processo operativo e può preparare segnali, schede e materiali, ma **non può approvarli o pubblicarli autonomamente**.
* Claude svolge la revisione indipendente al termine della preparazione e dichiara sempre il perimetro effettivamente verificato.
* Gli altri agenti possono segnalare casi rilevanti e assistere nella preparazione, ma non sostituiscono la revisione indipendente né l'approvazione umana.
* Orchestration Practices non modifica automaticamente stati, permessi, workflow o Definition of Done dei progetti osservati.
* Un'eventuale integrazione tecnica futura sarà valutata solo dopo la validazione del pilota.

## Ruoli

| Ruolo | Responsabilità |
| --- | --- |
| **Gianluca** | Seleziona i segnali da promuovere, approva o rifiuta le schede pratica e autorizza la pubblicazione. Conserva l'approvazione finale e il controllo sul merge. È l'unico approvatore durante il pilota. |
| **Codex — coordinatore operativo** | Coordina il flusso Orchestration Practices, prepara segnali e schede pratica, verifica la completezza del pacchetto, registra le attività e predispone il materiale per la revisione indipendente. Non può approvare il proprio lavoro, rimuovere autonomamente lo stato Draft, effettuare merge o pubblicare senza autorizzazione. |
| **Claude — revisore indipendente** | Opera nel contesto del repository pubblico `els-exchange`. Esamina il materiale preparato al termine dell'attività. Verifica coerenza, sicurezza, sanificazione e corrispondenza alle evidenze accessibili. Dichiara il perimetro verificato e le eventuali dipendenze da verifiche altrui. Non sostituisce l'approvazione finale di Gianluca. |
| **Agenti operativi** | Al termine di un'attività valutano se ricorre un criterio di rilevanza e, solo in caso affermativo, possono produrre un segnale leggero. Non creano automaticamente schede complete e non pubblicano nulla. |

## Flusso operativo

```text
attività operativa conclusa
        │
        ▼
criterio di rilevanza rilevato? ──── no ──→ nessuna azione
        │ sì
        ▼
segnale leggero  →  signals/inbox/
        │
        ▼
selezione della pratica (Gianluca)
        │
   ┌────┴────┐
   ▼         ▼
selected/  rejected/
   │
   ▼
scheda pratica completa  →  candidates/
        │
        ▼
sanificazione + preparazione (Codex)
        │
        ▼
revisione indipendente (Claude, via els-exchange)
        │
        ▼
approvazione esplicita (Gianluca)  →  approved/
        │
        ▼
pubblicazione autorizzata  →  published/
```

Ogni passaggio da una cartella all'altra è un'azione esplicita e tracciabile, non un processo automatico.

La chiusura dell'attività nel progetto originario non dipende dal completamento di questo flusso.

## Il segnale leggero

* È un **singolo file Markdown per caso**, creato in `signals/inbox/`.
* Naming: `YYYY-MM-DD-progetto-slug-breve.md`.
* Se il nome esiste già, aggiungere un suffisso numerico progressivo prima dell'estensione (`-2`, `-3`, ecc.).
* Non sovrascrivere mai un segnale esistente.
* Non è un unico file condiviso o append-only, per evitare conflitti tra agenti concorrenti e mantenere tracciabilità e spostamenti puliti.
* Viene prodotto solo quando un agente rileva almeno uno dei criteri di rilevanza definiti sotto, non al termine di ogni attività.
* Il segnale identifica il progetto originario, ma non diventa una nuova fonte di verità sul progetto.
* La correzione di eventuali errori deve avvenire prima nel repository originario. Il duplicato pubblico potrà essere successivamente riallineato.
* `signals/inbox/` viene normalmente revisionata da Gianluca una volta alla settimana, senza impedire revisioni anticipate quando emerge un caso forte o urgente.
* La struttura è definita in `templates/orchestration-practices-signal-template.md`.

### Vincolo di riservatezza

Il segnale non deve contenere:

* dati personali o dati cliente;
* prezzi o informazioni commerciali riservate;
* credenziali, token o segreti;
* endpoint interni;
* percorsi locali;
* vulnerabilità attive;
* identificativi privati non necessari;
* evidence pack contenenti dettagli operativi non sanificati;
* altro materiale sensibile.

In caso di dubbio, deve essere registrato soltanto il criterio rilevato, senza riportare i dettagli specifici.

## Soglia di rilevanza

I criteri sono qualitativi, sì/no, senza punteggio numerico. È sufficiente che **almeno uno** sia presente perché un agente possa creare un segnale:

* decisione architetturale o organizzativa significativa;
* pratica di coordinamento multi-agente risultata utile;
* errore con impatto reale;
* disaccordo o correzione tra persona e AI, manifestato in un evento concreto e documentabile (non una divergenza di opinione generica);
* errore umano individuato dall'AI;
* errore dell'AI individuato da una persona o da un altro agente;
* passaggio di consegna tra agenti riuscito o fallito in modo istruttivo;
* modifica rilevante al metodo di lavoro;
* risultato osservabile o inatteso;
* rischio significativo di sicurezza, qualità o governance, emerso da un evento concreto e osservato, non da un rischio soltanto ipotetico;
* lezione chiaramente trasferibile ad altri progetti.

Il segnale deve indicare quale criterio è stato rilevato e perché il caso potrebbe produrre una pratica trasferibile.

La presenza di un criterio autorizza soltanto la segnalazione. **Non** autorizza la creazione automatica della scheda pratica completa né alcuna pubblicazione.

## Scheda pratica completa

La scheda pratica viene creata solo per i segnali selezionati da Gianluca, mai automaticamente.

La struttura è definita in `governance/orchestration-practices-template.md` e comprende almeno:

* problema o contesto iniziale;
* decisione o pratica adottata;
* ruoli coinvolti;
* sequenza operativa;
* evidenze effettivamente disponibili;
* risultato osservato;
* condizioni in cui la pratica può essere riutilizzata;
* limiti e aspetti non ancora validati;
* checklist di sanificazione;
* perimetro della revisione indipendente;
* approvazione umana finale.

La sanificazione automatica o assistita non sostituisce mai il controllo umano finale.

## Revisione indipendente

Claude, operante nel contesto del repository pubblico `els-exchange`, interviene quando il pacchetto è completo e stabile. La revisione è richiesta per **ogni scheda pratica completa** che entra in `candidates/`, non solo in presenza di trigger specifici: qui il gate protegge una pubblicazione esterna, non un evento del lavoro operativo interno, e il volume iniziale atteso è basso.

La revisione deve:

* riferirsi alla versione esatta del materiale esaminato;
* verificare il contenuto grezzo integrale disponibile nel proprio perimetro;
* controllare coerenza, sanificazione e corrispondenza alle evidenze accessibili;
* indicare cosa è stato verificato direttamente;
* indicare cosa non è stato verificato;
* dichiarare eventuali dipendenze da controlli eseguiti da altri.

Se una parte dell'esito dipende da verifiche non eseguite direttamente, il verdetto deve essere:

`VALIDATO CON PERIMETRO`

Ogni modifica sostanziale successiva alla revisione riapre il pacchetto e richiede una nuova verifica.

Il gate si applica esclusivamente a `candidates/`: resta non bloccante per `signals/inbox/` e per i progetti operativi originari.

## Repository e visibilità

Orchestration Practices vive nel repository pubblico `els-exchange`, separato dai repository operativi dei singoli progetti.

I progetti operativi, come `els-platform`, restano:

* fonti dell'esperienza reale;
* fonti di verità per le rispettive decisioni;
* luoghi nei quali devono essere effettuate le correzioni originarie.

I contenuti presenti in `els-exchange/orchestration-practices/` sono duplicati pubblici sanificati e generalizzati. Non devono essere modificati come se fossero la fonte primaria di una pratica ancora mantenuta nel progetto originario.

### Ciclo di vita dei contenuti in els-exchange

Non tutti i contenuti di `els-exchange` hanno la stessa durata:

* **`orchestration-practices-operating-model.md`** e gli altri documenti di governance in `governance/` sono contenuti permanenti: definiscono il progetto stesso e restano nel repository, non vengono mai cancellati periodicamente.
* **`candidates/`** è uno spazio di transito: contiene schede pratica in attesa di revisione. Una volta che una scheda riceve un esito (approvata → `approved/` → `published/`, oppure rifiutata), la sua presenza in `candidates/` non ha più motivo di persistere e può essere rimossa secondo la cadenza di pulizia definita da Gianluca.
* **`published/`** contiene le pratiche pubblicate: è l'obiettivo del progetto, non un passaggio temporaneo. Non viene cancellato — è la knowledge base trasferibile che il progetto costruisce nel tempo.
* Materiale di scambio tecnico non editoriale (es. duplicati sanificati di file `els-platform` per validazione esterna one-off, non collegati a una scheda pratica) è per natura temporaneo: va rimosso dopo che la validazione richiesta è stata completata, con cadenza da definire in base all'uso reale osservato nelle prime settimane.

La cadenza esatta di pulizia per i contenuti di transito non è fissata ora: verrà decisa dopo aver osservato il volume reale generato nel primo periodo di attività, coerente con il principio di non anticipare strutture non ancora giustificate dall'esperienza.

**Le schede pratica depositate in `els-exchange/orchestration-practices/candidates/` devono essere già sanificate e verificate da Codex prima del deposito.** Il repository è pubblico: chiunque può clonarlo in qualsiasi momento, indipendentemente dalla sottocartella. Il deposito in `candidates/` non è un mezzo per far leggere bozze non ancora pulite a Claude — presuppone che la sanificazione sia già stata completata a monte.

HITF resta un progetto distinto:

* Orchestration Practices estrae e struttura il metodo trasferibile;
* HITF può raccontare l'esperienza umana e il caso reale;
* nessuno dei due modifica automaticamente il workflow dell'altro.

## Confini espliciti

Durante il pilota, Orchestration Practices:

* non modifica automaticamente stati, permessi o Definition of Done dei progetti operativi;
* non introduce automazioni di pubblicazione;
* non introduce nuovi permessi o dipendenze;
* non modifica ruleset o branch protection;
* non introduce GitHub Actions dedicate senza una decisione successiva;
* non pubblica nulla senza approvazione esplicita di Gianluca;
* non rimuove automaticamente lo stato Draft;
* non effettua merge automatici;
* non considera validata una pratica soltanto perché è stata documentata;
* non trasforma il processo di governance nel progetto principale.

## Stato del documento

Prima versione del pilota Orchestration Practices.

Il modello deve essere riesaminato dopo i primi casi reali, senza anticipare automazioni o strutture non ancora giustificate dall'esperienza.

La prima verifica del registro delle pratiche avverrà al raggiungimento di 10 casi oppure dopo 30 giorni dall'avvio del pilota, a seconda di quale condizione si verifichi per prima.
