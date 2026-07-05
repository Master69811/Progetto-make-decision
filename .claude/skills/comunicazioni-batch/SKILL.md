---
name: comunicazioni-batch
description: Genera in lotto comunicazioni verificate — solleciti fornitori, aggiornamenti clienti, avvisi ai reparti — con una passata di ricerca per destinatario e una di controllo su ogni bozza. Usare quando ci sono più destinatari da contattare sulla stessa base dati.
---

# Protocollo /comunicazioni-batch — la macchina: costruita una volta, gira ogni settimana

Adattamento del pattern "un agente ricercatore su ogni prospect, un agente di controllo su ogni bozza" alla supply chain.

1. Chiedi (se non forniti): la **lista destinatari** con i dati grezzi (es. estratto ordini in ritardo da ERP: fornitore, ordine, articolo, data promessa, nuovo fabbisogno) e l'**obiettivo comune** (sollecito, richiesta data confermata, avviso ritardo al cliente…).
2. **Passata ricercatore** — per ogni destinatario, raccogli SOLO dai dati forniti e dal repo (`contesto/profilo.md`, `decisioni/`): cosa gli abbiamo ordinato, cosa è in ritardo, che storia c'è (già sollecitato? recidivo?), qual è il problema reale da nominare.
3. **Bozza** — per ognuno un messaggio di massimo 3 frasi, con la voce di `contesto/stile.md`: fatto concreto → conseguenza → richiesta specifica con data.
4. **Passata di controllo** — rileggi ogni bozza come agente di verifica: ogni numero, data e affermazione deve avere riscontro nei dati forniti. Ciò che non è verificabile va rimosso o marcato `[DA CONFERMARE: …]` — mai inventato.
5. Consegna la tabella finale: destinatario → bozza → punti da confermare. L'utente approva e invia; niente parte da solo.
6. Chiusura in ottica refactoring: se lo stesso lotto va rifatto ogni settimana, proponi cosa standardizzare (estrazione ERP fissa, giorno fisso, modello messaggio) perché il giro successivo costi la metà.
