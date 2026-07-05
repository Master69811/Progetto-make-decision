---
name: decisione
description: Attiva il protocollo decisionale delle 4 domande (Obiettivo, Vincoli, Dati, Opzioni) su una nuova criticità di produzione, logistica o pianificazione. Usare quando l'utente deve prendere una decisione operativa.
---

# Protocollo /decisione

Segui il protocollo definito in CLAUDE.md, sezione "Protocollo decisionale".

1. Leggi `contesto/profilo.md` per il contesto (clienti, KPI, vincoli strutturali). Non chiedere ciò che è già scritto lì.
2. Se l'utente ha descritto la criticità nell'argomento del comando, estrai da lì le risposte già presenti alle 4 domande.
3. Fai in UN SOLO messaggio compatto solo le domande rimaste scoperte tra: **Obiettivo**, **Vincoli**, **Dati**, **Opzioni**. Poi fermati e attendi.
4. Alla risposta, produci: **Decisione raccomandata** (con motivazione in 2–3 righe), **Piano di esecuzione** (passi numerati con responsabile e scadenza), **Rischi e piano B**, **Refactoring** del processo.
5. Chiudi proponendo di salvare la decisione nel registro: crea il file `decisioni/AAAA-MM-GG-titolo-breve.md` da `decisioni/TEMPLATE.md` compilato, e committalo.

Stile: linguaggio da riunione di reparto, zero teoria. Se un compito emerso è di basso valore decisionale, proponi esplicitamente a chi o a cosa delegarlo.
