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

## Formato CSV/XLSX appreso

**Estrazione ERP completa (es. `conf2_*.csv`, separatore `;`)** — colonne chiave:
- `numop` = numero OP; `codart`/`desart` = codice/descrizione articolo; `desgru` = famiglia
- `dataimpegnocommessa`, `dtscap`, `datcon` = possibili date di consegna cliente (usare la prima valorizzata, in quest'ordine)
- `datric` = data richiesta/generazione (per calcolare la scadenza kanban a 10gg quando manca la consegna)
- `qtaop` = quantità; `tempores`/`TEMPOTEO` = tempo fase in formato `"Xh Y' Z\""` (sommare tutte le fasi dello stesso OP)
- `cellaancoratadescr` = linea; `descli`/`cliimp` = cliente; `criticitamancanti` = flag componenti mancanti (>0 = criticità)
- OBI: `codart` contiene `26707` o `26708`

**Foglio di sequenza reparto (es. `Schedulazione_reparto_*.xlsx`)** — formato minimale usato dal reparto per la propria sequenza:
- Colonne: `Sequenza` (ordine proposto dal reparto) · `Data consegna` (fascia larga, es. "06-08/07", spesso vuota) · `OP` (numero) · `Descrizione` (famiglia sintetica, es. "TEC 5/7/10", "P.ZAINO")
- Non contiene quantità, cliente, date precise: **incrociare per numero OP con l'ultima estrazione ERP disponibile** per recuperare data di consegna reale, cliente, criticità mancanti. Se l'estrazione ERP non è disponibile, chiedere questi dati prima di costruire il piano.
- La sequenza/raggruppamento del reparto in questo foglio riflette la loro logica di produzione (spesso per famiglia, indipendentemente dalla distanza tra le date reali) e va sempre confrontata con la regola dei 2gg: se il reparto raggruppa OP con consegne lontane nel tempo, segnalarlo come scostamento da validare, non applicarlo in automatico.

## Prossime regole

- [In attesa di risposta di Andrea: se il reparto raggruppa volutamente per famiglia oltre i 2gg (per saturare con materiale pronto), va formalizzata un'eccezione alla regola di accorpamento ("libero entro la settimana di reparto" invece di "max 2gg"), oppure resta un'anticipazione da autorizzare caso per caso?]
