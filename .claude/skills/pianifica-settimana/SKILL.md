---
name: pianifica-settimana
description: Costruisce il piano settimanale di produzione a partire da ordini, capacità e priorità clienti. Usare a inizio settimana o quando il piano salta e va rifatto.
---

# Protocollo /pianifica-settimana

1. Leggi `contesto/profilo.md` (clienti, KPI, vincoli strutturali).
2. Chiedi in un unico messaggio, solo se non già forniti:
   - **Portafoglio ordini** della settimana (cliente, articolo, quantità, data consegna) — anche incollato grezzo da ERP/Excel.
   - **Capacità disponibile** (linee, turni, assenze note, manutenzioni programmate).
   - **Criticità già note** (ritardi fornitori, materiale mancante, urgenze cliente).
3. Produci il piano:
   - **Priorità della settimana** — ordini in sequenza, con logica esplicita (data consegna, penali, saturazione collo di bottiglia).
   - **Piano per giorno/linea** — tabella compatta giorno × linea.
   - **Rischi** — dove il piano è fragile e qual è la mossa di riserva.
   - **Cosa delegare subito** — comunicazioni e controlli da passare a capiturno/collaboratori, con testo pronto.
4. Se durante la settimana il piano salta, l'utente rilancia il comando con la novità: aggiorna solo il delta, non rifare tutto da zero.

Output pronto da portare in riunione di pianificazione: sintetico, numerato, senza teoria.
