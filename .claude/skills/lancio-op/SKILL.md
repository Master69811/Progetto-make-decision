---
name: lancio-op
description: Genera il piano di produzione settimanale ottimizzato da un CSV/estratto di ordini di produzione (OP), applicando le regole di accorpamento per famiglia e i vincoli OBI definiti in contesto/regole-pianificazione.md. Usare quando l'utente allega o incolla la lista OP.
---

# Protocollo /lancio-op — Generazione piano settimana da CSV

1. Leggi `contesto/regole-pianificazione.md` (regole VINCOLANTI: accorpamento entro 2 giorni per famiglia/descrizione simile, max 2 OP OBI art. 26707/26708 a settimana) e `contesto/profilo.md` (clienti, vincoli di linea).
2. Prendi il CSV allegato o incollato. Identifica le colonne (numero OP, articolo, descrizione, famiglia, quantità, data consegna, cliente…). Se il mapping è ambiguo, mostra l'interpretazione e chiedi conferma UNA sola volta; poi salva il formato riconosciuto nella sezione "Formato CSV appreso" di `contesto/regole-pianificazione.md`, così dal secondo lancio non serve più.
3. Applica le regole nell'ordine: date di consegna → accorpamenti (anticipando, mai ritardando) → riempimento con OBI (max 2/settimana).
4. Consegna il piano così:
   - **Piano per giorno** — tabella: giorno → OP (quelle accorpate sulla stessa riga) → articolo/famiglia → quantità → data consegna → note.
   - **Accorpamenti fatti** — quali OP e perché (setup risparmiati).
   - **OBI** — le 2 inserite e quelle che slittano alla settimana dopo.
   - **⚠ Criticità** — OP non pianificabili entro la data, dati mancanti, conflitti; ognuna con la mossa proposta.
5. Se per pianificare servono capacità/turni/assenze non presenti nel CSV, chiedili in un unico messaggio insieme alle eventuali conferme di mapping — una sola andata e ritorno, poi il piano.
6. Chiusura: se il piano ha comportato scelte vere (cosa slitta, cosa si anticipa), proponi di salvarle in `decisioni/`; se è emersa una regola nuova, proponi di aggiungerla a `contesto/regole-pianificazione.md` e committa.

Output pronto da portare in riunione: tabella asciutta, niente teoria. Le regole non si rispiegano mai in chat: vivono nel file regole.
