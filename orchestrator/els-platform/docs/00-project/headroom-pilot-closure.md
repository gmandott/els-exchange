<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:docs/00-project/headroom-pilot-closure.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Chiusura del Micro-Pilot Headroom

**Stato**: PARCHEGGIATO (non abbandonato, non adottato) — decisione di Human Approver
**Data**: 12 agosto 2026
**Perimetro**: valutazione isolata di Headroom (context compression layer di terze parti) come possibile componente opzionale, mai integrata in AIDOS/Orchestrator.

---

## Decisione ufficiale

> La valutazione del micro-pilot Headroom si chiude senza adozione. Il pilota ha verificato che un design a doppia istanza del proxy (una ottimizzata, una in modalità passthrough per contenuto protetto) garantisce integrità byte-per-byte, ma non ha prodotto alcuna misura reale del beneficio economico che ne giustificherebbe l'adozione.
>
> Il progetto non prosegue ora per squilibrio tra sforzo investito nella verifica di sicurezza e assenza di dati sul risparmio reale, non per un problema di sicurezza riscontrato: nessun problema di sicurezza è stato trovato nel design verificato.
>
> Nessuna dipendenza è stata introdotta nel repository `els-platform` (verificato: nessun riferimento a Headroom in `package.json`, `pyproject.toml`, `requirements*.txt`, `.orchestrator/policies.yaml`, `.orchestrator/agents.yaml`).
>
> La riapertura è condizionata a un evento specifico, non a tempo: vedi criterio di riapertura sotto.

---

## 1. Cosa il pilota ha verificato (FATTO, con evidenza)

- **Integrità byte-per-byte confermata**: con Headroom in modalità passthrough (`--no-optimize`), contenuto protetto passa identico — hash SHA-256 verificato su tre punti (originale, inviato, ricevuto upstream). Dettaglio in `.orchestrator/pilots/headroom/evidence/2026-08-12-off-tampered-test.md`.
- **`--no-optimize` è una flag di avvio del processo, non selettiva per richiesta**: nessuna variabile d'ambiente equivalente esiste. Un'unica istanza non può ottimizzare parte del traffico e fare passthrough su un'altra parte contemporaneamente.
- **Nessun meccanismo di esclusione per path/file** trovato nella CLI o in configurazione. Esiste `--protect-tool-results` (protezione per nome di tool), ma non è stato testato e non è granulare per contenuto/file.
- **Integrità dei binari Codex verificata**: firme legittime OpenAI, nessun indizio di sostituzione. Il binario `[local-toolchain-path]` va evitato per certificato di firma revocato (motivo mondano, non un incidente di sicurezza).
- **La run economica originale (B1) non ha mai misurato nulla**: il proxy registrava `api_requests:0` — il traffico bypassava Headroom, non lo attraversava. Nessuna baseline (A1) con prova grezza recuperabile esiste. Dettaglio in `.orchestrator/pilots/headroom/evidence/2026-08-12-evidence-pack.md`.

## 2. Cosa NON è mai stato misurato

- Risparmio reale in token/costo su contenuto rappresentativo di questo progetto, con Headroom effettivamente attivo e funzionante (non simulato con gzip, non a proxy bypassato).
- Qualità della compressione semantica reale di Headroom (la simulazione nell'harness originale usava gzip come stand-in, non l'algoritmo reale del tool).
- Costo operativo ricorrente di mantenere due istanze del proxy in produzione.

## 3. Perché si chiude ora e non si prosegue

Sproporzione tra sforzo investito (più sessioni di ricostruzione forense, verifica di sicurezza, integrità binari, discussione di governance) e risultato economico ottenuto (zero). Prima di valutare Headroom o alternative, manca un dato più a monte: una misura reale della spesa attuale in token/costo su questo progetto, che stabilirebbe se il problema che Headroom vorrebbe risolvere è abbastanza grande da giustificare la complessità.

## 4. Criterio di riapertura

Non a scadenza fissa. Riaprire solo se si verifica una delle due condizioni:

- emerge una misura reale (non stimata) di spesa token/costo su Codex/Claude in questo progetto che renda il problema economicamente rilevante;
- oppure il progetto richiede esplicitamente un'ottimizzazione di questo tipo per un motivo diverso dal risparmio (es. limiti di context window raggiunti in modo ricorrente).

Se riaperto, il design da usare come punto di partenza è quello già verificato in questo pilota (doppia istanza, `--no-optimize` per contenuto protetto), non una nuova archeologia su A1/B1.

## 5. Materiale di riferimento

- `.orchestrator/pilots/headroom/README.md`: scope originale, esecuzione, conclusione di design.
- `.orchestrator/pilots/headroom/evidence/`: evidence pack completo e test decisivo (non tracciati da git, contengono percorsi locali).
- Nessuna modifica a `.orchestrator/policies.yaml`, `agents.yaml`, `workflows.yaml`, `states.yaml`, `AGENTS.md` o `ai-development-operating-model.md` in nessuna fase del pilota.

---

Prossimo progetto attivo: **Human in the Field** (repository separato), nessuna dipendenza da questa chiusura.
