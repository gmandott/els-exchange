<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/practices/registry.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Registro pratiche anti-errore

Questo registro contiene pratiche operative nate da episodi reali del progetto.

## Formato canonico

Ogni voce del registro deve usare questo formato:

```markdown
## PRACT-NNN — Titolo breve

- **Stato**:
- **Effetto operativo**:
- **Data proposta**:
- **Proposta da**:
- **Approvata da**:
- **Data approvazione**:
- **Ambito di applicazione**:
- **Cosa intercetta**:
- **Episodio di origine**:
- **Come si applica**:
- **Come si verifica**:
- **Evidenza minima richiesta**:
- **Esito se non rispettata**:
- **Formalizzata in**:
- **Sostituisce / sostituita da**:
- **Ultima revisione**:
```

## PRACT-001 — Contenuto grezzo obbligatorio prima dell'approvazione

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-17
- **Ambito di applicazione**: revisioni, approvazioni, verifiche di PR, issue, workflow, configurazioni e file dichiarati come fonte di verità.
- **Cosa intercetta**: riepiloghi corretti nella forma ma non verificati nella sostanza.
- **Episodio di origine**: revisione di PR #11, verifica di `origin/main:.orchestrator/policies.yaml` tramite output grezzo di `git show`.
- **Come si applica**: prima di un verdetto finale, il revisore richiede e legge il contenuto integrale rilevante: file, diff, output API o output comando.
- **Come si verifica**: il pacchetto di revisione o il commento di approvazione contiene il contenuto grezzo o un riferimento diretto all'output grezzo usato.
- **Evidenza minima richiesta**: diff completo, file completo, risposta API grezza o output comando integrale, secondo il caso.
- **Esito se non rispettata**: blocked
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-17

## PRACT-002 — Allowlist esplicita per azioni infrastrutturali

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-17
- **Ambito di applicazione**: task che toccano o potrebbero toccare ruleset, branch protection, required checks, merge settings, default branch, permessi, secret, variables, environment, webhook, GitHub Apps, deploy key o impostazioni repository/organizzazione.
- **Cosa intercetta**: azioni eseguite per obiettivo generale invece che per autorizzazione esplicita nel task corrente.
- **Episodio di origine**: modifica del ruleset `main-pilot-protection` per rendere `pr-validation` required, poi ratificata ex post su issue #9.
- **Come si applica**: un task infrastrutturale deve contenere un blocco esplicito di azioni autorizzate; ogni azione non elencata va fermata.
- **Come si verifica**: il resoconto finale confronta azioni eseguite e allowlist del task corrente; eventuali esclusioni sono dichiarate.
- **Evidenza minima richiesta**: testo dell'allowlist corrente, comando/API usati e output di verifica post-operazione.
- **Esito se non rispettata**: blocked
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-17

## PRACT-003 — Timestamp da fonte autoritativa

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-17
- **Ambito di applicazione**: finestre pilota, scadenze, approvazioni, audit trail e ogni timestamp con valore procedurale.
- **Cosa intercetta**: date o orari stimati, arrotondati o calcolati con fuso orario sbagliato.
- **Episodio di origine**: avvio finestra pilota tramite evento GitHub `ai-ready labeled` sulla issue #12, event ID `28084898536`.
- **Come si applica**: usare il campo temporale di un evento di sistema verificabile, per esempio `created_at` GitHub, e non l'orologio locale dell'agente.
- **Come si verifica**: il resoconto include evento sorgente, timestamp UTC originale, conversione IANA e scadenza calcolata.
- **Evidenza minima richiesta**: risposta API grezza con `created_at`, conversione `Europe/Rome`, verifica che la durata richiesta sia rispettata.
- **Esito se non rispettata**: blocked
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-17

## PRACT-004 — Riconferma reale delle correzioni dichiarate

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-17
- **Ambito di applicazione**: cicli `changes-requested`, correzioni post-review, fix di sicurezza, workflow e policy.
- **Cosa intercetta**: dichiarazioni di correzione non corrispondenti al cambiamento effettivo.
- **Episodio di origine**: verifica F1 su PR #11, dove la dichiarazione di correzione richiedeva confronto con contenuto grezzo e diff reale.
- **Come si applica**: dopo una correzione dichiarata, confrontare il punto contestato con il diff o file aggiornato, non solo con il riepilogo dell'agente.
- **Come si verifica**: il revisore indica quali righe, chiavi o output confermano la correzione.
- **Evidenza minima richiesta**: diff prima/dopo o contenuto integrale del file interessato, con riferimento al finding originale.
- **Esito se non rispettata**: changes-required
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-17

## PRACT-005 — Distinzione fra non applicabile, non disponibile e non verificabile

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-17
- **Ambito di applicazione**: controlli, skip, blocchi, workflow CI, validazioni locali e report finali.
- **Cosa intercetta**: stati diversi che vengono compressi in uno skip o blocco generico.
- **Episodio di origine**: progettazione e verifica di `pr-validation` in OPS-001, con separazione fra `SKIPPED - not applicable` e `SKIPPED - not currently available`.
- **Come si applica**: ogni controllo saltato o non concluso dichiara una categoria precisa: `not applicable`, `not currently available`, `unverifiable` o `blocked-by-baseline` quando applicabile. Ogni categoria deve indicare motivo, evidenza e condizione necessaria per procedere o recuperare.
- **Come si verifica**: log, descrizione PR o report finale mostrano la categoria dello skip/blocco e la motivazione.
- **Evidenza minima richiesta**: sezione di riepilogo con categorie distinte e motivazioni esplicite.
- **Esito se non rispettata**: changes-required
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-17

## PRACT-006 — Revisione registrata dove vive l'oggetto

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-18
- **Ambito di applicazione**: approvazioni, ratifiche e decisioni operative relative a issue o Pull Request.
- **Cosa intercetta**: decisioni importanti prese solo in chat e non visibili nella storia GitHub dell'oggetto.
- **Episodio di origine**: commenti di review indipendente su PR #11 e PR #13; commento di audit su issue #9.
- **Come si applica**: registrare la decisione come commento sull'issue o PR interessata, senza sostituire il resoconto in chat.
- **Come si verifica**: l'issue o PR contiene un commento con decisione, autore operativo, riferimento e data GitHub.
- **Evidenza minima richiesta**: URL del commento GitHub sulla issue o PR.
- **Esito se non rispettata**: warning
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-18

## PRACT-007 — Dichiarazione negativa dello scope non modificato

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-17
- **Proposta da**: ChatGPT, Claude, Codex
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-18
- **Ambito di applicazione**: report finali, pacchetti di review, task amministrativi, task con confini stretti.
- **Cosa intercetta**: azioni collaterali eseguite o sospettate perché non dichiarate esplicitamente.
- **Episodio di origine**: resoconti OPS-001, PILOT-001 e PILOT-002 con conferme negative su ruleset, branch protection, file e merge.
- **Come si applica**: il report finale elenca anche cosa non è stato toccato, non solo cosa è stato fatto.
- **Come si verifica**: il report contiene una lista negativa coerente con lo scope del task e con `git diff`/API GitHub.
- **Evidenza minima richiesta**: lista negativa esplicita più output `git diff --name-status`, metadati PR o risposta API quando applicabile.
- **Esito se non rispettata**: warning
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-18

## PRACT-008 — Registrare la revisione finale sulla PR prima del merge

- **Stato**: active
- **Effetto operativo**: required-for-pilot
- **Data proposta**: 2026-07-18
- **Proposta da**: Claude
- **Approvata da**: Human Approver
- **Data approvazione**: 2026-07-20
- **Ambito di applicazione**: revisioni indipendenti di Pull Request, prima di qualunque merge umano.
- **Cosa intercetta**: un verdetto di revisione prodotto e comunicato fuori da GitHub, ma non registrato sulla Pull Request prima del merge; un verdetto riferito a un HEAD precedente rispetto a quello effettivamente mergiato; oppure una registrazione che non distingua esplicitamente il revisore indipendente dal soggetto che pubblica il commento su GitHub e dalla provenienza effettiva della revisione. Questi casi possono richiedere una trascrizione post-merge o lasciare incerto chi abbia svolto la revisione e quale versione sia stata realmente approvata.
- **Episodio di origine**: PILOT-004, PR #19 - la revisione Claude con verdetto `APPROVED` era stata prodotta prima del merge, ma non registrata sulla PR; il gap e stato recuperato soltanto mediante una trascrizione post-merge esplicitamente qualificata come tale. PILOT-005, PR #21 - il commento pre-merge conteneva verdetto e HEAD SHA corretti, ma non distingueva esplicitamente Claude come revisore dal soggetto che aveva registrato il commento. Il secondo episodio non costituisce una violazione letterale della prima versione di PRACT-008: ha evidenziato una lacuna della specifica e un criterio di audit piu stringente rispetto al testo allora vigente. PILOT-006, PR #23 — la specifica rafforzata di PRACT-008 è stata implementata correttamente, ma la revisione indipendente e la relativa attestazione sono state completate soltanto dopo il merge. L’audit post-merge ha verificato il contenuto e registrato `APPROVED (post-merge)`, ma non ha sanato il requisito temporale mancante. PILOT-007 è il primo task progettato per completare integralmente il flusso pre-merge previsto dalla pratica aggiornata.
- **Come si applica**: prima del merge, il verdetto finale deve risultare sulla Pull Request e indicare almeno: revisore indipendente, registrante GitHub, verdetto, HEAD SHA revisionato, provenienza effettiva e stato della riconferma dopo eventuali commit successivi. La provenienza deve assumere il valore `review nativa GitHub` oppure `revisione esterna trascritta su GitHub`, secondo il caso reale. Se dopo la revisione viene aggiunto un nuovo commit, il revisore deve riconfermare il nuovo HEAD prima del merge. Per una revisione esterna, la trascrizione deve riportare fedelmente il verdetto e distinguere chi ha svolto la revisione da chi l'ha registrata su GitHub.
- **Come si verifica**: prima del merge si verifica che sulla Pull Request esista una registrazione con revisore indipendente, registrante GitHub, verdetto, HEAD SHA revisionato, provenienza e stato della riconferma. L'HEAD SHA revisionato deve coincidere con l'HEAD corrente e non devono esistere commit successivi privi di riconferma. Dopo il merge, il `created_at` della registrazione deve precedere il `merged_at`, e lo SHA revisionato deve coincidere con l'ultimo HEAD della Pull Request prima del merge.
- **Evidenza minima richiesta**: URL e comment ID o review ID, `created_at`, revisore indipendente, registrante GitHub, verdetto, HEAD SHA revisionato, provenienza della revisione, stato della riconferma dopo eventuali commit successivi, ultimo HEAD SHA della Pull Request prima del merge e `merged_at`.
- **Esito se non rispettata**: blocked
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-20

## PRACT-009 — Verificare l'integrità del contenuto pubblicato

- **Stato**: proposed
- **Effetto operativo**: advisory
- **Data proposta**: 2026-07-20
- **Proposta da**: Codex
- **Approvata da**: -
- **Data approvazione**: -
- **Ambito di applicazione**: pubblicazione o aggiornamento di descrizioni, commenti e altri testi registrati tramite shell, CLI o API, in particolare quando contengono caratteri speciali, quoting, sostituzioni o interpolazioni.
- **Cosa intercetta**: un testo correttamente autorizzato che viene registrato in forma incompleta o alterata perché il meccanismo tecnico di invio interpreta caratteri speciali o espansioni della shell.
- **Episodio di origine**: PILOT-007, issue #24 - il commento `5015281230` fu pubblicato con campi mancanti per un errore tecnico di quoting e sostituito come fonte autoritativa dalla rettifica `5015283420`; PILOT-009, issue #28 - la descrizione iniziale fu alterata dall'interpretazione dei backtick, il task venne fermato e la correzione autorizzata fu pubblicata tramite file temporaneo e verificata con `body_match=exact`.
- **Come si applica**: usare un meccanismo che preservi letteralmente il testo autorizzato, per esempio un file passato con `--body-file`, evitando l'interpolazione diretta della shell; dopo la pubblicazione, rileggere il contenuto dalla fonte autoritativa e confrontarlo integralmente prima di proseguire. Un record errato già pubblicato non viene modificato o cancellato senza autorizzazione esplicita.
- **Come si verifica**: recuperare tramite API il corpo effettivamente registrato e confrontarlo integralmente con il testo autorizzato; registrare identificativo, URL, autore tecnico, timestamp, metodo di invio ed esito del confronto.
- **Evidenza minima richiesta**: testo autorizzato, comando o meccanismo di invio, ID e URL dell'oggetto pubblicato, corpo riletto tramite API e risultato esplicito del confronto, per esempio `body_match=exact`; in caso di differenza, evidenza dello stop e della successiva autorizzazione alla correzione.
- **Esito se non rispettata**: warning
- **Formalizzata in**: -
- **Sostituisce / sostituita da**: -
- **Ultima revisione**: 2026-07-20
