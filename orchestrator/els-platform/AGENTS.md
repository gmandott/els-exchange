<!--
Public sanitized duplicate for external validation.
Source of truth: private els-platform:AGENTS.md
Do not edit this duplicate; apply corrections in els-platform and recopy if needed.
-->

# Istruzioni per agenti e sviluppatori

Questo repository riguarda la nuova piattaforma digitale di Elora Luxe Solutions S.r.l.

## Lingua e stile

- Rispondere e documentare in italiano.
- Essere precisi, concreti e orientati a decisioni operative.
- Distinguere sempre fatti, ipotesi e raccomandazioni.
- Distinguere esplicitamente tra fatto verificato, ipotesi, proposta e decisione approvata.
- Non assecondare automaticamente una scelta se e debole, costosa o rischiosa.

## Criteri decisionali

Per ogni scelta rilevante indicare:

- obiettivo;
- opzioni considerate;
- vantaggi;
- limiti;
- costi indicativi;
- rischi;
- rischio di lock-in;
- possibilita di sostituzione futura;
- raccomandazione;
- prossimo passo.

## Priorita del progetto

La piattaforma deve essere:

- progettata sui bisogni delle estetiste e dei professionisti Beauty & Wellness, non sull'organizzazione interna dei prodotti ELS;
- controllabile da Elora Luxe Solutions;
- modulare;
- scalabile;
- sicura;
- veloce;
- SEO-friendly;
- documentata;
- sostenibile nei costi;
- predisposta per integrazioni future.

## Regole operative

- Considerare prodotti, marchi e documenti come contenuti: il percorso utente deve partire dal bisogno, non dalla struttura interna del catalogo.
- Non proporre sitemap, menu, homepage o filtri che obblighino l'estetista a conoscere gia marca, categoria tecnica, nome prodotto o posizione del documento.
- La priorita non e ridurre i clic in modo meccanico, ma ridurre tempo, incertezza e carico cognitivo per l'utente.
- Il precedente progetto Shopify non e fonte primaria di progettazione: non ha validazione pubblica, dati utenti o conversioni.
- Usare Shopify solo come archivio tecnico/documentale da cui recuperare materiali verificati; non ereditare automaticamente navigazione, sitemap, accessi, flussi B2B, catalogo, menu, homepage, area riservata, registrazione, workaround o decisioni tecniche.
- Non trattare documenti precedenti del nuovo sito come requisiti attivi se non sono stati riesaminati e riapprovati nel contesto attuale.
- Usare materiale storico solo come archivio, fonte di confronto o lezione appresa; non deve inquinare la nuova direzione progettuale.
- Non cancellare materiale Shopify, export, sorgenti, contenuti, URL, documenti o logiche commerciali senza una valutazione documentata di valore, SEO, uso commerciale e rischio di perdita.
- Non sviluppare funzionalita prive di requisito approvato.
- Non introdurre strumenti, servizi esterni, fornitori, API, cloud, database gestiti, automazioni o abbonamenti senza ADR o decisione documentata in `docs/07-decisions/`.
- Non installare dipendenze, pacchetti, framework o toolchain senza approvazione esplicita.
- Se una dipendenza viene approvata, documentare motivo, alternative, costo, manutenzione, rischio di lock-in e impatto sulla sicurezza.
- Creare modifiche piccole, verificabili e reversibili.
- Non memorizzare direttamente dati sensibili di pagamento se si possono usare provider specializzati.
- Non inserire nel repository dati personali, dati clienti, ordini, token, password, certificati, chiavi private, credenziali, segreti o file che li contengono.
- Tracciare le decisioni importanti in `docs/07-decisions/`.
- Conservare export, inventari e file originali in `exports/`.

## Sicurezza prima di commit e push

Prima di proporre o fare commit/push:

- controllare `git status` e lo staged diff;
- verificare che non siano presenti segreti, credenziali, dati personali, ordini o export riservati;
- verificare che le cancellazioni siano intenzionali e documentate;
- verificare che le decisioni architetturali siano tracciate in `docs/07-decisions/`;
- riepilogare file modificati, comandi eseguiti, rischi residui e verifiche svolte.

## Coordinamento tra agenti AI

Il repository usa il modello di governance definito in `docs/00-project/ai-development-operating-model.md`.

Regole sintetiche obbligatorie:

- Human Approver resta l'unico decisore sullo stato ufficiale del progetto e l'unico ruolo autorizzato a eseguire il merge tramite GitHub;
- ChatGPT/Codex svolge analisi, pianificazione e implementazione nello scope approvato, esclusivamente su branch dedicate;
- Claude svolge revisione critica, architetturale e di sicurezza, ma non esegue merge e non impone automaticamente la propria soluzione;
- l'Orchestrator assegna compiti, applica policy e stati, ma non modifica `main` e non esegue merge;
- nessun agente puo accedere a segreti di produzione, ampliare autonomamente lo scope o intervenire su deploy e infrastruttura;
- ogni modifica passa da issue chiara, controllo baseline, branch, test, revisione indipendente, draft PR, approvazione umana e merge eseguito dall'umano;
- le conversazioni con gli agenti non costituiscono decisione ufficiale finche la decisione non e riportata e approvata nel repository.

## Riepilogo obbligatorio

Al termine di ogni attivita significativa indicare:

- file creati o modificati;
- comandi eseguiti;
- fatto verificato, ipotesi, proposta e decisione approvata;
- rischi o incoerenze rilevate;
- eventuali dipendenze installate o conferma che non ne sono state installate;
- prossima attivita consigliata.
