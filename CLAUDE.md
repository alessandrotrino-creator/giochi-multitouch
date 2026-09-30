# CLAUDE.md — note per riprendere il lavoro

Progetto **separato** dal Laboratorio dei Solidi (richiesta del docente: cartella e chat a parte).
Ultimo aggiornamento: 30 settembre 2026.

## Chi e per cosa
- Docente di matematica e scienze, scuola secondaria di primo grado; lingua di lavoro italiano.
- La scuola avrà uno **schermo multitouch**; il docente vuole giochi a squadre che ne sfruttino il potenziale (ambito scientifico, matematico, tecnologico, ma anche altro), **uno alla volta**.
- Serve anche una **versione per LIM**, che di solito riconosce un tocco alla volta.
- Sul PC del docente non ci sono né git né node: i file si caricano dal sito di GitHub.

## Decisioni
- Ogni gioco è **un solo file HTML** senza build, come il laboratorio. Nessun dato salvato o inviato; solo le preferenze in `localStorage` (`duello-prefs`).
- Notazione italiana: `·` per moltiplicare, `:` per dividere, virgola decimale (`Intl.NumberFormat('it-IT')`), frazioni disegnate in colonna.
- Multitouch vero: le risposte usano `pointerdown` (non `click`), così più dita contemporanee funzionano; `touch-action:none`, niente zoom, niente menu con la pressione lunga.
- Modalità LIM proposte dal docente e da Claude: **a turni con rubapunto** e **con prenotazione** (pulsante per squadra o tasti A / L, anche con due tastiere USB).

## `duello.html` (Duello a squadre)
- Schermate: `#setup`, `#game` (multitouch, due metà `.half` + barra centrale), `#lim` (domanda al centro, squadre ai lati `.side`), `#end` (risultato e riepilogo).
- Domande: `CATS`, gruppo `g:'mat'` (calc, pot, fraz, equiv, solidi, equaz) e `g:'sci'` (moto, dens, forze, calore, materia, energia, viventi, terra; il vecchio `scienze` unico è stato diviso e le preferenze salvate vengono convertite). Ogni argomento ha `gen(l)` per le domande classiche, `rc(l)` (ragionamento calcolato, può restituire `null`) e `cp[l]` (domande di concetto `[domanda, giusta, sbagliate…]`). Livelli 1–3 + **4 esperto** usato solo per il bonus. Risultato `{q, a, opts, x?}`: `x` è la spiegazione mostrata dopo la risposta e nel riepilogo. `numQ` arrotonda a 4 decimali e crea le risposte sbagliate; `txtQ` per le risposte a parole; `cmpQ` per i confronti A/B; `genQ` riprova finché le 4 risposte sono diverse.
- Verificato (30/09/2026) generando 400 domande per argomento, livello e modalità (classica e ragionamento): nessun errore, 4 risposte diverse, quella giusta presente. `window.__duelloTest` espone `CATS`, `genQ`, `P` per ripetere la verifica.
- Impostazioni nuove: `sfida` (`classica` / `veloce` / `ragion`), `diff` (`fissa` / `cresc` / `mix`), `mix` [base, medio, avanzato], `bonus`, `speedT` (secondi per domanda nella velocità alla LIM), `rafT` (durata della raffica).
- Velocità multitouch = **raffica** (`R`, `rafStart`, `rafNext`, `rafAnswer`, `rafClock`): ogni squadra ha le sue domande; con difficoltà crescente sale di livello ogni 4 risposte giuste. Alla LIM la velocità usa solo un tempo breve (`curT`). Il bonus vale 3 punti (`q.pts`) e ha il tempo doppio.
- Stato: `P` (impostazioni), `G` (partita), `LG` (fasi della LIM: `book`, `answer`, `end`), `R` (raffica).
## Idee per i prossimi giochi (dall'elenco proposto al docente)
Caccia alle coppie simultanea (formula–figura, solido–sviluppo…), "Costruisci insieme" a tempo (figure di area data, circuiti), geopiano collaborativo, tangram / equiscomposizione con rotazione a due dita, frazioni da spezzare, circuiti elettrici, leve e bilance, ottica, ecosistemi, linea del tempo.
