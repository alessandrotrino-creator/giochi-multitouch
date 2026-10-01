# CLAUDE.md — note per riprendere il lavoro

Progetto **separato** dal Laboratorio dei Solidi (richiesta del docente: cartella e chat a parte).
Ultimo aggiornamento: 30 settembre 2026.

## Chi e per cosa
- Docente di matematica e scienze, scuola secondaria di primo grado; lingua di lavoro italiano.
- La scuola avrà uno **schermo multitouch**; il docente vuole giochi a squadre che ne sfruttino il potenziale (ambito scientifico, matematico, tecnologico, ma anche altro), **uno alla volta**.
- Serve anche una **versione per LIM**, che di solito riconosce un tocco alla volta.
- Sul PC del docente non ci sono né git né node: i file si caricano dal sito di GitHub.

## Decisioni
- Ogni gioco è **un solo file HTML** senza build, come il laboratorio. Nessun dato salvato o inviato; solo le preferenze in `localStorage` (`duello-prefs`, `coppie-prefs`).
- Il docente carica i file a mano dal sito di GitHub (Add file → Upload files): la cartella di lavoro è `Desktop\giochi multitouch`. Non lasciarci file di servizio (es. `.claude/`).
- Notazione italiana: `·` per moltiplicare, `:` per dividere nei calcoli, virgola decimale (`Intl.NumberFormat('it-IT')`), frazioni disegnate in colonna.
- **Richiesta del docente (01/10/2026): notazioni e accortezze da docente di scuola media, riconosciute, «da manuale».** Le formule si scrivono con la **linea di frazione** (helper `frac`): v = s/t, d = m/V, p = F/S, I = V/R, aree b · h fratto 2, volumi fratto 3, Pick A = I + B/2 − 1. Niente «×» per moltiplicare (solo negli incroci di genetica Aa × Aa); le dimensioni si scrivono a parole («con le dimensioni di 3 cm, 4 cm e 5 cm», «rettangolo di lati 2 e 5»). Termini da libro: «intensità di corrente», «resistore», «braccio» della leva (F₁ · b₁ = F₂ · b₂), «indice» nelle formule chimiche, interruttori «in serie / in parallelo». Simboli normalizzati per gli schemi elettrici.
- Il Laboratorio dei Solidi resta fuori da questo progetto (il docente ha detto di lasciarlo stare).
- Multitouch vero: le risposte usano `pointerdown` (non `click`), così più dita contemporanee funzionano; `touch-action:none`, niente zoom, niente menu con la pressione lunga.
- Modalità LIM proposte dal docente e da Claude: **a turni con rubapunto** e **con prenotazione** (pulsante per squadra o tasti A / L, anche con due tastiere USB).

## `duello.html` (Duello a squadre)
- Schermate: `#setup`, `#game` (multitouch, due metà `.half` + barra centrale), `#lim` (domanda al centro, squadre ai lati `.side`), `#end` (risultato e riepilogo).
- Domande: `CATS`, gruppo `g:'mat'` (calc, pot, fraz, equiv, solidi, equaz) e `g:'sci'` (moto, dens, forze, calore, materia, energia, viventi, terra; il vecchio `scienze` unico è stato diviso e le preferenze salvate vengono convertite). Ogni argomento ha `gen(l)` per le domande classiche, `rc(l)` (ragionamento calcolato, può restituire `null`) e `cp[l]` (domande di concetto `[domanda, giusta, sbagliate…]`). Livelli 1–3 + **4 esperto** usato solo per il bonus. Risultato `{q, a, opts, x?}`: `x` è la spiegazione mostrata dopo la risposta e nel riepilogo. `numQ` arrotonda a 4 decimali e crea le risposte sbagliate; `txtQ` per le risposte a parole; `cmpQ` per i confronti A/B; `genQ` riprova finché le 4 risposte sono diverse.
- Verificato (30/09/2026) generando 400 domande per argomento, livello e modalità (classica e ragionamento): nessun errore, 4 risposte diverse, quella giusta presente. `window.__duelloTest` espone `CATS`, `genQ`, `P` per ripetere la verifica.
- Impostazioni nuove: `sfida` (`classica` / `veloce` / `ragion`), `diff` (`fissa` / `cresc` / `mix`), `mix` [base, medio, avanzato], `bonus`, `speedT` (secondi per domanda nella velocità alla LIM), `rafT` (durata della raffica).
- Velocità multitouch = **raffica** (`R`, `rafStart`, `rafNext`, `rafAnswer`, `rafClock`): ogni squadra ha le sue domande; con difficoltà crescente sale di livello ogni 4 risposte giuste. Alla LIM la velocità usa solo un tempo breve (`curT`). Il bonus vale 3 punti (`q.pts`) e ha il tempo doppio.
- Stato: `P` (impostazioni), `G` (partita), `LG` (fasi della LIM: `book`, `answer`, `end`), `R` (raffica).
- **5 livelli** (dal 30/09/2026, richiesta del docente): 1 Base, 2 Medio, 3 Avanzato, 4 Esperto, 5 Campione. Il livello 5 sta in `L5[k]()` (chiamato all'inizio di ogni `gen` con `if(l===5)`) e `CP5` (domande di concetto). Il bonus usa il livello 5; crescente = 1 → 5; `mix` ha 5 valori (le preferenze vecchie a 3 valori vengono allungate).
- **Risposte sbagliate** (richiesta del docente): in `numQ` sempre 2 plausibili (gli errori candidati più vicini, distanza relativa < 1,6) + 1 molto sbagliata (distanza ≥ 4, altrimenti ×25 o simile). Verificato: circa il 94% delle domande numeriche ha esattamente questa forma; le altre hanno comunque 2 vicine e 1 lontana, con soglie un po' diverse.

## `coppie.html` (Caccia alle coppie) — creato il 30/09/2026
- Schermate come il Duello: `#setup`, `#game` (due metà con tabellone `.board` ciascuna), `#lim` (tabellone al centro), `#end`. Preferenze in `localStorage` (`coppie-prefs`).
- Coppie: `CATS` con `one(livello)` → `{a, b, v}`; `v` è il "valore" della coppia e `buildPairs` scarta le coppie con stesso `v` o stessa etichetta nello stesso round (una carta = una sola compagna). Aiuti: `numP`, `txtP`, `bank({1:[…],2:[…],3:[…]})`, `equivP` (unità in `UN`). Disegni SVG in `FIG` (figure piane) e `SOL` (solidi), classe `.fig`.
- Multitouch: trascinamento con un dito per carta (`S.drags` per `pointerId`, `setPointerCapture`), oppure tocco-tocco (`S.sel` per squadra). Nella disposizione "tavolo" la metà blu è ruotata di 180° e gli spostamenti vengono invertiti. Coppia +1, chi finisce il round +2; una coppia sbagliata blocca le due carte per 1 s.
- LIM: `limTap`; scoperte (il turno passa dopo ogni tentativo) o memory (chi trova una coppia rigioca).
- Il testo delle carte si adatta con `container-type:size` e unità `cqi/cqh`; classi di lunghezza `len2` / `len3` (non usare `.mid`: è la colonna centrale).
- Verificato: 300 coppie per argomento e livello senza errori; round da 8 coppie completi con tutti gli argomenti; prove nel browser di trascinamento, tocco-tocco, memory alla LIM e riepilogo. `window.__coppieTest` espone `CATS`, `buildPairs`, `P`.
- **5 livelli**: ai livelli 4 e 5 `buildPairs` usa prima le **famiglie** `FAM[k](l)`, gruppi di coppie che si somigliano apposta (stessi numeri con operazioni diverse, simboli chimici simili, area/perimetro, V/R/I…), poi completa con `one(3)`. Attenzione a non creare ambiguità vere: ogni carta deve avere una sola compagna (es. calcare e arenaria sono entrambe sedimentarie → descrizioni diverse). Crescente: dal livello 1 al 5 distribuiti sui round.

## `leve.html` (Leve e bilance) — creato il 30/09/2026
- Richieste del docente: dettaglio grafico, **oggetti reali** come masse, **varietà** e diversi livelli. Oggetti SVG in `OBJ`: 1 bottiglia 1 L, 2 mattone, 3 zucca, 4 pesetto, 5 anguria, 10 secchio 10 L, `mys` scatola misteriosa.
- Scena: cielo + prato, asse di legno `.beam` ruotata con la variabile CSS `--a`, fulcro di pietra; livello base = bilancia a piatti (`.stage.scale`, `.slot.pan` controruotati così restano orizzontali). Tacche = distanze 1..N.
- Sfida `makeChallenge(l)` → `{N, left, rload, M, tray, limited, count, onlyD, mys, task, sol}`: 3 tipi per livello (vedi README). `solsK` trova le soluzioni con k oggetti; verificato: 400 sfide per livello, tutte risolvibili rispettando i vincoli.
- Tabelloni `BD[1]`, `BD[2]`, `BD.L` (LIM) creati da `mkBoard`; trascinamento per `pointerId` con un "fantasma" nel `body` (ruotato di 180° per la squadra girata nel modo tavolo); tocco su un oggetto già piazzato = lo toglie. Successo quando momento destra = sinistra e i vincoli sono rispettati; al livello 5 poi `ask` (4 risposte: giusta, 2 vicine, ×10).
- LIM: a turni, rubapunto dopo tempo scaduto, «Passa» o risposta sbagliata; la seconda squadra riparte dalla leva com'è.
- Preferenze `leve-prefs`. `window.__leveTest` per le verifiche.

## `frazioni.html` (Frazioni da spezzare) — creato l'01/10/2026
- Oggetti SVG disegnati da `drawWhole(type, p, on, off)`: `pizza` (spicchi), `choc` (tavoletta, griglia da `chocGrid`), `bar` (nastro), `set` (biscotti). Parti `.part[data-i]`, decorazioni `.deco` senza eventi; la parte colorata prende `--tc` (colore della squadra; alla LIM `#lim.turn1/2`). Più interi (`wholes`) = frazioni maggiori di 1.
- Sfide `makeChallenge(l)`: `kind:'color'` (successo quando colorate/parti = n/d, anche equivalente; `cut` = divisione libera con + e −; `notSame` = denominatore diverso da d) oppure `kind:'choice'` (4 risposte: giusta, 2 plausibili, 1 molto sbagliata; `fopts`, `nopts`, miniature con `mini`). 3–4 tipi per livello (vedi README).
- Colorare: `pointerdown` su una parte la cambia; strisciando si applica lo stesso cambio (per `pointerId`); il controllo `check` avviene quando si alza il dito.
- `sizeObjs` adatta i disegni alla scena; più nastri vanno uno sotto l'altro, lunghi uguali (per confrontare a occhio).
- Verificato: 400 sfide per livello, tutte risolvibili, risposte sempre 4 e diverse con una sola giusta; prove nel browser di strisciata, divisione libera, confronto. Preferenze `frazioni-prefs`, `window.__frazTest`.

## `geopiano.html` (Geopiano) — creato l'01/10/2026
- Griglia 9 × 9 chiodini (`G = 8` quadretti), disegnata in SVG da `geoSVG` (legno, chiodini, asse `axis`, figura modello `model`, elastico `band`). L'SVG viene ridisegnato a ogni chiodino: per le coordinate usare sempre `st.querySelector('svg').getScreenCTM()` (funziona anche con la metà ruotata).
- Elastico: tocco su un chiodino = aggiungi; trascinando si vede l'elastico tirato (`.pre`) e si aggiunge il chiodino dove si alza il dito; toccando il primo chiodino si chiude e parte il controllo. «Annulla» riapre / toglie l'ultimo, «Ricomincia» libera tutto.
- Geometria: `simplify` (toglie punti doppi e allineati), `isSimple` (niente incroci), `area2`, `perim`, `rectil`, `isRect`, `isSquare`, `isPara`, `isTrap`, `isRightTri`, `isObtuse`, `isIso`, `interior` (Pick), `canon` (confronto di forme, con o senza spostamento). Figure modello in `TPL`.
- Sfide `makeChallenge(l)`: `kind:'build'` con `test(a)` che restituisce '' oppure il motivo (mostrato se l'aiuto è attivo), oppure `kind:'choice'` (area o perimetro della figura grigia). Verificato con 2640 figure di prova: tutte le sfide hanno almeno una soluzione.
- Preferenze `geopiano-prefs`, `window.__geoTest`.

## `circuiti.html` (Circuiti elettrici) — creato l'01/10/2026
- Reticolo di nodi 5 × 4 (`X(c)`, `Y(r)`), ogni componente sta su un lato tra due nodi: `{a, b, t, id?, on?, o?, r?, v?, placed?}` con `t` = `wire`, `bat` (il + è sul nodo `a`), `lamp`, `sw`, `motor`, `buzz`, `res`, `obj` (oggetti in `OBJ`, `c` = conduttore), `slot` (buco da riempire).
- Simulazione `solve`: metodo dei nodi con eliminazione di Gauss; pila = 4,5 V con resistenza interna 0,1 Ω; lampadina 10 Ω, motore 8 Ω, cicalino 12 Ω. `sim` restituisce accese (`lit`), potenze (`P`), correnti (`I`) e `short` (corrente nella pila > 8 A). `truth` prova tutte le combinazioni degli interruttori (serie/parallelo).
- Disegni: `partSVG` (realistico, corpi ingranditi con `SC = 1.45`) e `symSVG` (simboli normalizzati, sfondo bianco, classe `paper`); scelta con `P.draw` (`real` / `sym`), anche nell'editor.
- Sfide `makeChallenge(l)`: `build` con `els`, `tray` e `test(els)` → '' o motivo; `choice` con 4 risposte. Verificato con un risolutore automatico (tutte le combinazioni di pezzi e interruttori): tutte risolvibili, nessuna già risolta all'inizio.
- Editor libero (`#editor`, oggetto `ED`): tutti i 31 lati del reticolo sono buchi; tavolozza `TOOLS`; misure a lato (I in A per pila e utilizzatori).
- Richiesta del docente: **notazioni da manuale** e **formule con la linea di frazione** (I = V/R con `frac`), «resistore», «intensità di corrente», «interruttori in serie / in parallelo» (non «circuito E/O»).
- Preferenze `circuiti-prefs`, `window.__circTest`.

## `index.html` (launcher)
- Pagina iniziale del sito GitHub Pages: una tessera per gioco (link relativi `duello.html`, `coppie.html`) e l'elenco "In arrivo". Ogni gioco ha in alto il link «← Tutti i giochi». Quando si aggiunge un gioco: nuova tessera `.game` qui, riga nella tabella del README.

## Idee per i prossimi giochi (dall'elenco proposto al docente)
"Costruisci insieme" a tempo (figure di area data, circuiti), geopiano collaborativo, tangram / equiscomposizione con rotazione a due dita, frazioni da spezzare, circuiti elettrici, leve e bilance, ottica, ecosistemi, linea del tempo.
