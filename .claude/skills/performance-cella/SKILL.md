---
name: performance-cella
description: Calcola la performance/OEE di una cella di assemblaggio confrontando il tempo teorico da OD (Prod. Oraria Prevista) con il tempo effettivo da MES, quantificando pezzi persi/guadagnati e ore-uomo di impatto. Usare quando l'utente incolla o fotografa un Ordine di Produzione e i tempi macchina/MES di una fase, o chiede un controllo scostamento produzione.
---

# Protocollo /performance-cella

Ruolo: analista Lean Manufacturing / controllo produzione. Obiettivo: alimentare la Dashboard Daily Decision Support con un'analisi quantitativa e monetizzabile (in ore-uomo e pezzi) dello scostamento tra tempo teorico e tempo reale di una fase/cella.

Se l'utente ha già usato il calcolatore "📐 Performance cella" nell'app, i numeri arrivano già calcolati nel prompt: non rifare la matematica, vai diretto al punto 3 (diagnosi) e 4 (output).

## 1. Dati di input necessari

Estrai da OD (ordine di produzione) e MES (o chiedi se mancano, in un unico messaggio):
- Cella di lavoro
- Numero operatori in cella (se non indicato, chiedilo — serve per il calcolo ore-uomo; senza, salta quella parte)
- Quantità richiesta da OP (PZ)
- Produzione oraria prevista da OD (PZ/ora)
- Tempo Linea Totale da MES (minuti totali) — è il campo "tempo linea totale" del MES — se il MES mostra più intervalli inizio/fine per lo stesso OP/fase, SOMMALI tutti (non prendere solo l'ultimo)

## 2. Calcoli (formule esatte, arrotonda solo alla fine)

- Tempo Unitario Teorico (min/pz) = 60 / Prod. Oraria Prevista
- Tempo Totale Teorico (min) = Tempo Unitario Teorico × Quantità Richiesta
- Performance Rate (%) = (Tempo Totale Teorico / Tempo Effettivo MES) × 100
- Delta Minuti = Tempo Effettivo MES − Tempo Totale Teorico

Se Delta > 0 (Effettivo > Teorico → INEFFICIENZA):
- Pezzi Equivalenti Persi = Delta Minuti / Tempo Unitario Teorico
- Ore-Uomo Sprecate = (Delta Minuti × Numero Operatori) / 60

Se Delta < 0 (Effettivo < Teorico → EXTRA-PRODUZIONE):
- Pezzi Guadagnati / Capacità Rilasciata = |Delta Minuti| / Tempo Unitario Teorico
- Ore-Uomo Risparmiate = (|Delta Minuti| × Numero Operatori) / 60

Sempre:
- Ore Uomo Teoriche Impegnate = (Tempo Totale Teorico × Numero Operatori) / 60
- Ore Uomo Effettive Pagate = (Tempo Effettivo MES × Numero Operatori) / 60

## 3. Diagnosi (solo se inefficienza)

Incrocia con `contesto/profilo.md` e buon senso Lean per la causa più probabile:
- Molti micro-fermi (tanti intervalli brevi e distanti nel tempo nel MES) → probabile mancanza materiale o micro-fermi macchina
- Un solo intervallo molto più lungo del previsto → probabile fermo macchina/attrezzaggio o sotto-organico
- Performance vicina al 100% ma leggermente sotto → normale variabilità, nessuna azione
- Performance <60% → è una criticità, non una nota: proponi di aprire `/decisione`

## 4. Output (pronto per i widget della dashboard)

1. **RIEPILOGO FLASH**: OP · Cella · Performance %
2. **TEMPI**: teorico · Tempo Linea Totale (MES) · delta (in minuti, con segno)
3. **IMPATTO PRODUTTIVO**: pezzi persi/guadagnati · ore-uomo in eccesso/risparmiate
4. **BILANCIAMENTO**: ore-uomo teoriche vs effettive
5. **ALERT DECISIONALE**: una frase diretta, senza giri di parole (es. "La linea ha impiegato 3 volte il tempo previsto: verificare mancato carico pezzi su MES o fermo su AP1.")

Se la performance è sotto soglia critica o si ripete sulla stessa cella, proponi di aprire `/decisione` o di registrare un refactoring in `decisioni/`.

## 5. Correzione tempo ciclo a gestionale

L'app calcola già in automatico (sezione "Tempo ciclo a gestionale" del calcolatore) se lo scostamento è ricorrente (≥3 letture coerenti nello storico della stessa cella) e in tal caso suggerisce la Prod. oraria corretta da riportare a gestionale. Se il prompt arriva con questo dato già presente, non ricalcolarlo: usalo per raccomandare o meno la correzione a gestionale, spiegando il perché in una riga.
