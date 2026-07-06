# Progetto Make-Decision — Decision Engine

Sistema operativo decisionale per pianificazione e gestione produzione (Epoca SpA). Fonde due approcci:

- **"Costruisci l'app che hai sempre voluto"** (il post di image.png): un'app reale, costruita da un prompt, testata finché ogni funzione non funziona dall'inizio alla fine.
- **La logica Decision Engine (Fable 5)**: Analisi Lean → Elaborazione → Refactoring → Delegazione → Esecuzione, con il protocollo delle 4 domande (Obiettivo, Vincoli, Dati, Opzioni).

Il risultato non è una to-do list: è uno strumento che elabora le variabili del lavoro (priorità = urgenza × impatto, stato KPI automatico) e si aggancia a Claude per la parte di ragionamento.

Le altre slide del carosello sono adattate così al lavoro di produzione:

| Slide | Idea originale | Qui diventa |
|---|---|---|
| 2 | Clone che scrive come te | `contesto/stile.md` + `/comunica`: email a clienti e messaggi ai capiturno con la tua voce, sottoposti ad approvazione |
| 3 | 100 lead con agente ricercatore + controllo | `/comunicazioni-batch`: solleciti fornitori e aggiornamenti clienti in lotto, ogni affermazione verificata sui dati |
| 4 | Voto sul setup AI | `/audit-sistema`: pagella periodica del sistema, con l'unica modifica che rende di più |
| 8 | Sistema operativo agentico | Tab **Plancia** nell'app: report mattutino, skill come pulsanti a un clic, log di ogni sessione |

## Cosa c'è nel repo

| Percorso | Cosa fa |
|---|---|
| `app/index.html` | **L'app operativa, vista board stile Trello.** Un solo file, funziona offline e da telefono, dati salvati sul dispositivo (localStorage). Decisioni e Agenda sono board a colonne trascinabili (Decisioni: Aperta→Decisa→Eseguita→Verificata; Agenda: colonne per giorno); KPI a colonne per stato (Fuori target/Attenzione/OK). Tab **Plancia** con report giornaliero, comandi a un clic, log sessioni e **📐 Performance cella** (calcolatore OD vs MES: performance %, pezzi persi/guadagnati, ore-uomo, ricalcolo dinamico dello staffing con selettore rapido); guida di stile, backup JSON. |
| `app/classic.html` | **Stessa app, vista a liste** (senza drag & drop): utile se preferisci scorrere elenchi invece di trascinare schede, o su schermi molto piccoli. Dati condivisi con `index.html` (stesso localStorage). |
| `app/pc.html` | **Vista desktop per la postazione in ufficio.** Sidebar fissa, saluto con data, 5 tessere di riepilogo (decisioni aperte, KPI fuori target, agenda di oggi, ultima attività, performance celle positivo/negativo), coda priorità e colori corporate Epoca (blu navy + verde). Stessa logica dati delle altre due viste, ma pensata solo per schermo largo/mouse — non per telefono. Il log delle "Performance cella" (solo sul clic esplicito su **Calcola**, mai durante l'anteprima dal vivo dello staffing) alimenta in automatico la board KPI (le celle diventano schede con sparkline, soglia target 85-115%), il Report di oggi e le Decisioni aperte: sotto il 50% si apre da sola una criticità e il pulsante "Decidi criticità" punta dritto al prompt di approfondimento di quella cella. |
| `CLAUDE.md` | **Il cervello.** Il system prompt della Decision Engine: si attiva da solo in ogni sessione Claude aperta su questo repo — non serve più incollarlo. |
| `contesto/profilo.md` | **La memoria fissa.** Ruolo, clienti (Mesto, Davines…), sistemi ERP/MES, KPI e vincoli ricorrenti. Compilarlo una volta = non rispiegare mai il contesto (riduzione token). |
| `contesto/stile.md` | **La tua voce.** Guida di stile per email e messaggi: `/comunica` la usa per scrivere come te. |
| `.claude/skills/` | **I comandi:** `/decisione`, `/pianifica-settimana`, `/lancio-op` (piano da CSV), `/kpi`, `/refactoring-processo`, `/comunica`, `/comunicazioni-batch`, `/audit-sistema`, `/performance-cella` (diagnosi scostamento OD/MES). |
| `contesto/regole-pianificazione.md` | **Le regole di lancio OP.** Accorpamenti, vincoli OBI, formato CSV appreso: si aggiornano qui, mai rispiegate in chat. |
| `decisioni/` | **Il registro.** Ogni decisione chiusa diventa un file da `TEMPLATE.md`: è la memoria storica del sistema. |

## Come si usa

**L'app (da telefono o PC):**
1. Scarica `app/index.html` e aprilo nel browser (o attiva GitHub Pages sul repo per averla a un URL fisso).
2. Registra criticità (le 4 domande sono il modulo), KPI e piano settimana durante la giornata.
3. Quando serve ragionare: **📋 Esporta per Claude** → ottieni un prompt già formattato con lo stato attuale.

**La Decision Engine (in Claude):**
1. Apri una sessione Claude su questo repo (claude.ai/code o app mobile): la modalità si attiva da sola grazie a `CLAUDE.md`.
2. Incolla il prompt esportato dall'app, oppure lancia direttamente `/decisione`, `/pianifica-settimana` o `/kpi`.
3. Ricevi: decisione raccomandata, piano di esecuzione, rischi/piano B e **refactoring** del processo.
4. Riporta la decisione nell'app e, per quelle importanti, salvala in `decisioni/`.

## Iterazione continua

Come da approccio originale: se una risposta è troppo teorica, dillo ("Troppo teorico, semplifica per operatività di linea") — e se il difetto è ricorrente, la correzione va scritta in `CLAUDE.md` o `contesto/profilo.md`, così il sistema migliora in modo permanente, non solo per quella chat.

## Primo passo consigliato

Compila `contesto/profilo.md` con i tuoi dati reali (clienti, KPI con target, vincoli di linea): è il file che fa la differenza tra un assistente generico e il tuo.
