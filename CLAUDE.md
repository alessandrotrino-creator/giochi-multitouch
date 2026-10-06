# CLAUDE.md — note per riprendere il lavoro

Progetto **separato** dal Laboratorio dei Solidi (richiesta del docente: cartella e chat a parte).
Ultimo aggiornamento: 5 ottobre 2026.

## Chi e per cosa
- Docente di matematica e scienze, scuola secondaria di primo grado; lingua di lavoro italiano.
- La scuola avrà uno **schermo multitouch**; il docente vuole giochi a squadre che ne sfruttino il potenziale (ambito scientifico, matematico, tecnologico, ma anche altro), **uno alla volta**.
- Serve anche una **versione per LIM**, che di solito riconosce un tocco alla volta.
- Sul PC del docente non ci sono né git né node: i file si caricano dal sito di GitHub.

## Decisioni
- Ogni gioco è **un solo file HTML** senza build, come il laboratorio. Nessun dato inviato; in `localStorage` solo le preferenze (`duello-prefs`, `coppie-prefs`…), il **registro di classe** (`gm-registro`, se si indica la classe) e le domande del docente (`duello-mie`). Mai nomi di alunni.
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
- 04/10/2026: sfide `count` (Countdown, `P.cdT` 30/45/60/120 s o 0 = senza tempo) e `high` (Highlander, `HIGH_T` = 10 s a domanda, 20 per la ★); `isSv()`, stato `SV`, funzioni `sv*`. Errore o tempo scaduto = la squadra è fuori (`svOut`). Difficoltà `fissa` o `scala` (`SCALA` = 1,1,2,2…5,5 ciclico); ogni 10ª domanda ★ livello 5 da 3 punti. Multitouch: le due squadre insieme con la stessa sequenza `SV.qs[0]` (richiesta del docente: stesse domande quando si sfidano). LIM: le squadre giocano una dopo l'altra (pulsante «Via!») con domande gemelle `SV.qs[1]` (stesso `ck` e livello). Barre per metà `#hb1/#hb2` (solo Highlander). Verificato nel browser.
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
- Dal 04/10/2026 le sfide da colorare non si chiudono più da sole: pulsante «✓ Conferma» (.confirm, disattivo se non c'è nulla di colorato) chiama check(id); conferma sbagliata = blocco 2 s (penalize) con messaggio in .aid, alla LIM = limFail + esetObjs per la squadra che ruba.
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

## `tangram.html` (Tangram) — creato l'01/10/2026
- Pezzi presi dal quadrato classico di lato 8 (`RAW`), centrati sul baricentro (`LOCAL`); posizione `{type, rot (passi di 45°), flip, x, y}`, vertici con `verts`. Aree in triangoli piccoli: `UNITS` (ST 1, MT/SQ/PA 2, BT 4, quadrato 16). `SQUARE()` è il quadrato classico (secondo BT `rot:6`, secondo ST `rot:2`).
- Sagome casuali `genShape(types)`: ogni pezzo si attacca a un lato libero di uguale lunghezza (orientato al contrario), senza sovrapposizioni (`overlap`, asse separatore); si preferiscono le sagome compatte.
- Controllo `covered`: campionamento a passo 0,25 sulla sagoma; va bene se la sagoma è coperta una volta sola e nulla esce (tolleranza 1,2%) — quindi anche soluzioni diverse da quella generata. `snap` aggancia il vertice più vicino (entro 0,75) a un vertice della sagoma o di un altro pezzo.
- Gesti: trascinare (un dito per pezzo), tocco = ruota di 45°, pressione lunga sul parallelogramma = capovolgi. La sagoma ha il bordo spesso (`.sil`) per non mostrare le giunture.
- Verificato: nessuna sovrapposizione nelle sagome generate; prove nel browser con 2, 4 e 7 pezzi (ruotare + trascinare + aggancio → punto). Preferenze `tangram-prefs`, `window.__tgTest`.

## `energia.html` (Città dell'energia) — creato l'01/10/2026
- Richiesta del docente: **non un quiz** ma un gioco coinvolgente su energia, fossili, rinnovabili, centrali, nucleare; partita rapida; anche **una sola squadra**; **dati scientifici ufficiali** per CO₂, scorie e tutto il resto; richiami a documenti ufficiali (WMO, IPCC…) e a studiosi come Telmo Pievani; geotermico e maree come «botta di fortuna» rara.
- Mappa 6 × 4 (`genMap`: fiume, costa, città, montagne, colline; rari `geo` e `baia`), regole di costruzione in `canBuild`. Centrali in `PL` con fonti nel commento (IPCC AR5 2014 per la CO₂ nel ciclo di vita, WNA per petrolio e scorie, IRENA 2023 e IEA/NEA per i costi). Budget `BUDGET0`/`BUDGETDAY`.
- `simulate(team, day)`: 24 ore; prima rinnovabili non regolabili (sole, vento, geotermico, maree), poi nucleare e carbone (sempre al massimo), poi idroelettrico, gas, petrolio, batterie; l'energia in più carica le batterie o si spreca. `scoreOf` calcola i punti (blackout −2 per ora). `forecast(t)` mostra le previsioni mentre si costruisce.
- **Mai citazioni inventate**: le idee degli studiosi sono riassunte con la fonte; le citazioni testuali vanno nell'array `CITAZIONI` (le inserisce il docente). Fatti in `FATTI`, ognuno con la fonte.
- `P.nteams` (1 o 2) con `ACT()`; alla LIM con due squadre si costruisce a turno. Preferenze `energia-prefs`, `window.__enTest`.
- 01/10/2026, richieste del docente: «indicatori immediatamente percepibili, anche nel gioco», tutto «più facilmente consultabile e selezionabile», tutorial con le motivazioni delle scelte, mini giochi su ogni centrale e sui legami tra energie, «sempre fruibili e piacevoli anche graficamente».
  - **Indicatori**: `dashPlan`/`dashSim` in `#dash{t}`. In pianificazione: Notte, Mezzogiorno, Sera, CO₂, Rinnovabili. Durante la simulazione: Adesso, CO₂ finora, Batterie (`hours[h].bat/batMax`).
  - **Mappa con rendimento**: `drawMap` mostra la percentuale `effAt` quando una centrale è selezionata; grigio dove `canBuild` vieta.
  - **Tavolozza e scheda**: nomi brevi `SHORT`. Scheda in `infoCard`: trasforma, dove rende (`WHERE`), pro e contro, costo, potenza, CO₂. Pulsante `? Guida` (`guide`).
  - **Layout**: `#game.table` e `#game.solo` usano una griglia con la mappa a sinistra.
  - **Tutorial**: `startTutorial`, `TUT` (11 passi con `hl` per evidenziare e `wait` come condizione), `tutCheck`, `tutRender`. Usa `TUT_MAP`, il budget 300, e `#h2` come pannello guida; «Fatto!» compare solo dal passo `TUT_FATTO`.
  - **Laboratorio** (`#lab`, `LABS`, `labOpen`, `labLoop`): ogni mini gioco ha `init`, `step(s,dt)`, `scene(s,t)` (SVG 400 × 300), `ctrls` (range, seg, btn), `goals` `{t, f, hold, why}`, `chain`/`plant` per la catena (`s.stage` passi accesi). `catena` e `sole` sono `custom`. Le stelle restano solo durante la sessione (`L.stars`), non vengono salvate.
  - Verificato in browser: tutorial completo; tutte le sfide di tutti i mini giochi risolvibili; partita a 2 squadre, a 1 squadra, a tavolo, alla LIM, 1600 × 900 e 1366 × 768.

## `zoo.html` (Lo zoo della classificazione) — creato il 01/10/2026
- **Richiesta del docente**: «divertente e carino», sugli animali: invertebrati e phyla, vertebrati e classi, classificazione nei gruppi giusti. Il docente vuole **entrambi i nomi «cnidari» e «celenterati»**: nel gioco si scrive sempre «Cnidari (celenterati)».
- **Disegni**: `DRAW[k]()` restituisce SVG 100 × 100 in stile adesivo (contorno #2E3047). Funzioni di aiuto `fish`, `bird`, `frog`, `insect`, `dup` (tubo con contorno), `E`/`EW` (occhi), `CK` (guance). Gli artropodi sono visti dall'alto e il numero di zampe e antenne è quello giusto (aragosta e gambero 10, porcellino di terra 14, mosca 2 ali).
- **Dati degli animali**: `ROWS` contiene `[chiave, articolo, nome, gruppo foglia, d, indizio1, indizio2, x]`, dove `d` è 1 per un animale tipico, 2 per uno meno noto, 3 per un trabocchetto, e `x` è la spiegazione speciale del trabocchetto.
- **Gruppi**: `GR` (`n`, `s` singolare con articolo, `col`, `need` per il suggerimento quando si sbaglia, `why`, `traits` per l'identikit dal più vago al più preciso).
- **Argomenti**: `TOPICS` (vi, cla, phy, art, mol, pes), ognuno con la funzione `of(a)` che dice in quale recinto va l'animale per quell'argomento.
- **Chiavi dicotomiche**: `KEYTREE`. La risposta giusta si calcola con `leavesOf`.
- **Modalità**:
  - `smista`: recinti `.pen`; trascinamento per `pointerId` con copia `.ghost` e `elementFromPoint`, oppure tocco sull'animale e poi sul recinto. Alla LIM i turni sono a tempo.
  - `ident`: indizi a tempo, `clueTime`; l'ultimo indizio è la sagoma. Alla LIM a turni con rubapunto.
  - `chiave`: ogni squadra ha la sua sequenza di animali; alla LIM a turni per animale.
- **Pool degli animali**: `poolFor(topic, lv)`. Livello 1 solo `d` = 1; livello 2 `d` ≤ 2; livello 3 tutti; livelli 4 e 5 `d` ≥ 2. Se restano meno di 6 animali si allarga.
- **Preferenze e test**: preferenze in `zoo-prefs`; per le verifiche c'è `window.__zooTest`.
- **Verificato in browser**:
  - i 91 disegni;
  - le tre modalità;
  - LIM, tavolo (anche il trascinamento dalla metà capovolta) e 1366 × 768.

## Registro di classe (05/10/2026, richiesta del docente: anche l'anno, per usarlo molti anni)
- Blocco comune **identico in ogni gioco**: CSS «registro di classe e verifica formativa» in fondo allo `<style>` e `<script>` con `window.REG` prima dello script principale (per un gioco nuovo copiarlo da `duello.html`). API: `REG.field('#regField')` nel setup (classe in `gm-classe`, anno scolastico automatico set→ago, `REG.anno()` = '2026/27'); `REG.save({gioco, titolo, modo, livello, squadre:[{nome,punti}], items:[{t,l,ok,q,a}]})` salva in `gm-registro` solo se c'è la classe (`q`/`a` solo per le voci sbagliate, ripuliti dall'HTML); `REG.report('#regBox', rec)` = verifica formativa (per argomento, da riprendere sotto il 60%, domande sbagliate, classifica delle classi del gioco nell'anno).
- `registro.html`: filtri anno/classe/gioco, riquadri, argomenti, andamento mensile (SVG con tooltip), livelli, mappa di calore classi × argomenti, classifica classi (almeno 5 risposte), record squadre, domande sbagliate più spesso, elenco partite (con elimina), Esporta/Importa .json (unione per `id`), cancella anno o tutto, stampa, dati di esempio solo in memoria (`makeDemo`).
- Ogni gioco registra solo sfide concluse (non quelle interrotte con «Fine»); nessun salvataggio senza voci; tutorial, editor e laboratori liberi non registrano.

## Novità del 05/10/2026 per gioco (fatte con aiutanti in parallelo, verificate nel browser)
- **duello**: «Le mie domande» (schermata `#mine`; raccolte in `duello-mie` `{v:1, raccolte:[{id,nome,qs:[{q,a,w:[3],x,l}]}]}`; chiavi `my:<id>` in `P.cats`; `activeCats()`; `fmt()` converte `[3/4]`, `2^3`, `10^-2`, `^(…)`, `*` in «·»; incolla da testo `parseLines` con `;` o tab, 5–7 campi, intestazione scartata; Esporta/Importa con `myMerge`). Ogni raccolta pesa come un argomento in `drawQ`/`svDraw` (`myQ` preferisce il livello giusto). Registro da `G.log`; nella raffica `R.wrong` registra la domanda lasciata dopo un errore.
- **frazioni**: sfida «Retta dei numeri» (`lineChallenge`, `kind:'line'`, `line:{max,sub,toks:[{x:{n,d,w},k}]}`, `w` = f/m/dec/pct; «punto segnato» = choice con `line.mark`; `lineSVG`, `lineGeom` con costanti `NL`, `bindLine` drag per pointerId e tocco seleziona/posa, `placeTok`, `showLineSol`). Solo con «✓ Conferma». `makeChallenge(l, kinds)` = retta circa 1 su 4 + `classicChallenge`; tipi `P.kC/kS/kR` (almeno uno). `fopts` usa la chiave ridotta. Ogni sfida ha `t` per il registro. Verificate 2000 sfide della retta.
- **coppie / geopiano / tangram**: solo registro (coppie: una voce per coppia, `S.log[r].got`, `regTxt` per le carte disegnate).
- **leve / circuiti**: «Tipo di sfide» `P.mode` = classiche o `goal` (stelle 1–3 = punti, +1 a chi finisce prima se entrambe risolvono, l'altra ha `GOAL_LEFT` 45 s; `confirmGoal`, `goalDone`, `endGoal`, `starsSVG`, `starsFor`; timer su `S.dur`). leve: `makeGoal`/`goalOf`, `GL_TYPES`, `bfsMoves`, fulcro mobile `kind:'fulc'`, bilancia «⚖ Pesa» `kind:'weigh'`, `OBJ.rock`. circuiti: `GC`, `GL`, ricerca esaustiva `optSearch` (budget 30 000 tentativi; al livello 4 fino a circa 1 s), `optPic` disegna la soluzione migliore; l'interruttore posato si toglie trascinandolo; argomenti `ch.tp`. Nel registro le sfide a obiettivo hanno l'argomento «Obiettivo: …» (circuiti da `tp`, leve da `ch.gt` con la tabella `GT` in `finish`: meno oggetti, forza minima, dove va il fulcro, peso misterioso, meno mosse…), scelta del docente del 05/10/2026.
- **energia**: `P.modo` partita / `sfida`; 15 scenari `SCN` (3 per livello, `LEVELS`; giornata deterministica `scDay`; `evalSc`, `scChecks`, `scRef`, `miniMap`, `finishSfida`, `regSfida`); `__enTest.checkSfide()` dà 3 stelle a tutti (verificato). Registro della partita con `regPartita()` (5 obiettivi per squadra) e due mini giochi del laboratorio (catena, sole). Alla LIM la città dell'altra squadra è coperta. Pulsante «Inizia ▶» per saltare l'intro.
- **zoo**: modalità `catena` (`FO` con `e` = tutto ciò che mangia davvero, così le risposte sbagliate sono davvero sbagliate; `CHAINS`; `WEBS` con freccia da chi è mangiato a chi mangia; `SCEN`; motore `ch*` con stato `G.C`, «✓ Conferma», primo giusto 3 punti, secondo 2) e `inventa` (laboratorio `#lab`, `creatureSVG`, regole `classify(o)` che restituisce `{ok,g,cand,no,ex,nt}`, `CREAT`, `invOptions`). 19 disegni nuovi (produttori, decompositori, orca, volpe, falco…), 100 animali nell'album. Etichette delle caselle con `container-type` e `12cqi`. Registro con `G.items` (smistamento: conta solo il primo tentativo).
- Copia degli originali di prima di queste modifiche: cartella `Desktop\Giochi multitouch - originali 5 ottobre` (da togliere quando il docente conferma).

## Riorganizzazione del 06/10/2026 (richiesta del docente: «sono tanti, visualizzazione migliore»; scelta: tutte e tre le schede + impostazioni interne)
- `index.html`: schede `.tabs` (Per materia = sezioni di prima `#tab-mat`; Per argomento `#tab-arg` con `TOPICS` [nome, categoria, voci [gioco, come trovarlo, impostazioni nell'indirizzo]]; Per classe `#tab-cls` con `CLS[1..3]`). Le tessere riusano il disegno `.art` delle tessere della scheda per materia. Stato in localStorage `gm-home-scheda`, filtro in `gm-home-filtro`. L'escape room è un progetto separato (cartella `Desktop\Escape room`) e non compare più negli «in arrivo».
- Blocco comune `SETUP` (CSS «impostazioni ordinate» + `<script>` prima di quello di REG, identico in tutti i 9 giochi): `SETUP.hash(P)` prima di `renderSetup()` legge `#chiave=valore&…` dall'indirizzo (array separati da virgole, numeri, booleani; valgono per quell'apertura, poi si salvano come sempre quando si cambia qualcosa); `SETUP.organize()` dopo `renderSetup()` sposta in `<details class="sgrp">` i campi `n1, n2, nteams, regField` («Squadre e classe»), `screen, layout, limMode, timeC, timeT, timeR, timeM, time, speedT, aid, draw, sound` («Schermo, tempi, aiuti e suoni»), `howto, objs, parts, plist, rules` («Come si gioca»), con riassunto (`SETUP.refresh`, anche quando si torna alle impostazioni: MutationObserver sulla classe di `#setup`), e mette il pulsante `#go` (o il suo `.actions`) in una barra fissa `.startbar`. Il riquadro si trova risalendo da `#go` (`.card` nel duello, `.card0` negli altri). `opt.keep` = id da lasciare in vista.
- Verificato nel browser: i 9 giochi organizzati senza errori, riassunti aggiornati (i campi nascosti non compaiono), avvio e ritorno alle impostazioni, aperture già impostate (duello/coppie `cats`, zoo `mode/topics/level`, energia `modo`, geopiano `lvl`…).

## `index.html` (launcher)
- Pagina iniziale del sito GitHub Pages: una tessera per gioco (link relativi `duello.html`, `coppie.html`) e l'elenco "In arrivo". Ogni gioco ha in alto il link «← Tutti i giochi». Quando si aggiunge un gioco: nuova tessera `.game` qui, riga nella tabella del README.

## Idee per i prossimi giochi (dall'elenco proposto al docente)
"Costruisci insieme" a tempo (figure di area data, circuiti), geopiano collaborativo, tangram / equiscomposizione con rotazione a due dita, frazioni da spezzare, circuiti elettrici, leve e bilance, ottica, ecosistemi, linea del tempo.
