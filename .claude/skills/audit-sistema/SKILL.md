---
name: audit-sistema
description: Dà un voto a tutto il setup Decision Engine (CLAUDE.md, skill, contesto, registro decisioni, app) e indica cosa sistemare, unire, eliminare e la singola modifica che rende di più. Usare ogni 2-4 settimane o quando il sistema sembra appesantito.
---

# Protocollo /audit-sistema — fatti dare un voto sul setup

1. Leggi tutto il setup: `CLAUDE.md`, ogni skill in `.claude/skills/`, `contesto/profilo.md`, `contesto/stile.md`, il registro `decisioni/` e `app/index.html` (solo struttura e funzioni, non riga per riga). Se il registro decisioni è corposo, usa subagenti in parallelo per analizzarlo.
2. Dai un **voto da 1 a 10 per area** con una riga di motivazione:
   - Contesto (profilo/stile compilati e attuali?)
   - Skill (usate davvero? sovrapposte? mancanti?)
   - Registro decisioni (si accumula conoscenza o è vuoto?)
   - Coerenza CLAUDE.md ↔ skill ↔ app (i comandi promessi esistono? i protocolli combaciano?)
   - App (i dati che raccoglie servono ai prompt che genera?)
3. Report finale in 4 blocchi secchi:
   - **Da sistemare subito** — errori e incoerenze concrete.
   - **Da unire** — skill o file che si sovrappongono.
   - **Da eliminare** — ciò che non viene usato: ogni pezzo non usato è Muda di manutenzione.
   - **L'unica modifica che rende di più** — una sola, con stima del beneficio in tempo/settimana.
4. Chiedi conferma e applica le modifiche approvate (aggiorna file, committa). L'audit che non produce commit è teoria.
5. Chiudi annotando la data dell'audit in fondo a `CLAUDE.md` (riga "Ultimo audit: AAAA-MM-GG, voto medio X"), così il prossimo audit misura il progresso.
