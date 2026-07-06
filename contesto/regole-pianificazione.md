# Regole di pianificazione — Lancio OP

> Regole VINCOLANTI per `/lancio-op` (generazione piano settimana da CSV).
> Questo file è la memoria delle regole: quando ne emerge una nuova o una
> cambia, si aggiorna QUI — mai riscriverla a voce ogni volta.

## Accorpamento OP

- Accorpa gli OP della **stessa famiglia** o con **descrizione simile** quando le date di consegna distano **al massimo 2 giorni**.
- L'accorpamento **anticipa sempre** al più presto del gruppo: mai posticipare una consegna per accorpare.
- Obiettivo dell'accorpamento: ridurre i setup/cambi formato (Muda di attrezzaggio).

## Ordini quadro a scorta — codice OBI

- Articoli interessati: **26707** e **26708**.
- **Massimo 2 OP OBI a settimana.**
- Sono flessibili (scorta): si usano per **saturare capacità residua**, mai al posto di OP con data consegna cliente.
- Le OP OBI escluse slittano alla settimana successiva (segnalarle in coda al piano).

## OP senza data consegna — KANBAN a ripristino scorta

- Un OP **senza data consegna cliente** (campo data impegno/consegna vuoto) è un **kanban di ripristino scorta**: nasce quando il magazzino scende sotto scorta minima.
- Vincolo: **massimo 10 giorni** dalla data di generazione/richiesta (`datric`/`dtscap` nel CSV) per il reintegro — trattarla come una scadenza vera, non come priorità bassa.
- **Vanno accorpati anch'essi** con le regole normali (stessa famiglia/descrizione simile, entro 2 giorni), usando come "data consegna" la scadenza di reintegro calcolata (data generazione + 10gg), non l'assenza di data.
- Non confonderli con gli OBI (26707/26708): un OP può essere kanban senza essere OBI (altri articoli a scorta) — le due regole si applicano insieme quando coincidono.

## Priorità generali

1. Prima le date di consegna cliente (mai pianificare oltre la data).
2. Poi le scadenze kanban di reintegro scorta (max 10gg dalla generazione).
3. Poi la sequenza per famiglia (minimizzare i cambi).
4. Poi il riempimento con OBI.

## Formato CSV appreso

- [Da compilare al primo lancio: colonne riconosciute e loro significato,
  così i lanci successivi non richiedono conferme.]

## Prossime regole

- [aggiungere qui man mano che emergono]
