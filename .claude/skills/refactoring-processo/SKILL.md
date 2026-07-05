---
name: refactoring-processo
description: Post-mortem di un problema chiuso e miglioramento del processo perché non si ripresenti. Usare dopo che una criticità è stata risolta, o quando lo stesso problema si ripete.
---

# Protocollo /refactoring-processo

1. Se il problema è nel registro, leggi il relativo file in `decisioni/`; altrimenti fatti raccontare in breve cosa è successo e come è stato risolto.
2. Applica i 5 perché in forma compatta: risali alla causa radice in massimo 5 passaggi, senza cerimonia.
3. Produci:
   - **Causa radice** — una frase.
   - **Contromisura strutturale** — la modifica al processo, alla regola ERP/MES o alla routine di reparto che elimina o attenua la ricorrenza. Deve essere qualcosa che funziona anche quando nessuno ci pensa.
   - **Chi la implementa e entro quando.**
   - **Segnale di controllo** — come ci si accorge entro 2 settimane se la contromisura sta funzionando.
4. Aggiorna la sezione "Refactoring del processo" e "Verifica a posteriori" del file in `decisioni/`, o crealo da `decisioni/TEMPLATE.md` se non esiste. Committa.
5. Se la causa radice è un vincolo strutturale ricorrente, proponi di aggiungerlo a `contesto/profilo.md`.

Regola: una contromisura che dipende dal "ricordarsi di fare attenzione" non è un refactoring, è un rischio rimandato.
