# Giochi multitouch

**▶ Gioca online: [alessandrotrino-creator.github.io/giochi-multitouch](https://alessandrotrino-creator.github.io/giochi-multitouch/)**

Giochi a squadre per lo schermo multitouch della scuola e per la LIM, pensati per la scuola secondaria di primo grado.
Ogni gioco è una sola pagina web: si apre con il browser, senza installare nulla, e non salva né invia dati.

## Il progetto
L'idea è sfruttare uno schermo multitouch grande come spazio di gioco condiviso: più studenti toccano lo schermo **nello stesso momento** e le squadre si sfidano faccia a faccia, invece di aspettare il proprio turno. Ogni gioco ha anche una **versione per la LIM**, che di solito riconosce un tocco alla volta.

- **Per chi:** classi della scuola secondaria di primo grado, soprattutto per matematica e scienze. Altri ambiti verranno aggiunti in seguito.
- **Come si usa in classe:** per ripassare, come attività di apertura o di chiusura della lezione, o come sfida tra squadre. Le domande sono generate a caso ogni volta, quindi si può rigiocare senza ripetere le stesse domande.
- **Dosare la difficoltà:** si scelgono gli argomenti e il livello. Il livello può restare fisso, salire durante la partita oppure essere composto su misura, con una domanda bonus finale. Dopo molte risposte compare una breve spiegazione, così anche l'errore diventa un'occasione per imparare.
- **Senza complicazioni:** niente account, niente installazioni, nessun dato degli studenti. Serve solo un browser: si apre il file dal computer oppure dal sito, se il progetto è pubblicato con GitHub Pages.
- **Scritto in italiano**, con la notazione usata a scuola: `·` e `:` per moltiplicazione e divisione, virgola decimale, frazioni in colonna.

I giochi si aggiungono uno alla volta e si aprono tutti dalla pagina iniziale `index.html` (il launcher). Tra le idee per i prossimi ci sono: linea del tempo.

## Giochi

La pagina `index.html` è il **launcher**: mostra tutti i giochi con una tessera grande da toccare. Ogni gioco ha in alto il link «← Tutti i giochi» per tornare lì.

| File | Gioco | Come si gioca |
|---|---|---|
| `duello.html` | **Duello a squadre** | Due squadre, la stessa domanda con 4 risposte. Tre modi di gioco: **Multitouch** (lo schermo è diviso in due e si risponde tutti insieme: vince il punto chi tocca per primo la risposta giusta; chi sbaglia resta bloccato 2 secondi); **LIM a turni** con rubapunto; **LIM con prenotazione** (pulsante grande di ogni squadra, oppure tasti A e L della tastiera). |
| `coppie.html` | **Caccia alle coppie** | Carte da abbinare (figura–nome, operazione–risultato, grandezza–unità, strumento–che cosa misura…). **Multitouch**: ogni squadra ha le sue carte e tutti giocano insieme; si trascina una carta sulla compagna oppure si toccano una dopo l'altra, e chi finisce per primo il round prende 2 punti in più. **LIM**: un solo tabellone, a turni, con carte **scoperte** oppure **coperte** (memory). |
| `leve.html` | **Leve e bilance** | Oggetti veri da trascinare (bottiglia d'acqua da 1 kg, mattone 2 kg, zucca 3 kg, pesetto 4 kg, anguria 5 kg, secchio d'acqua 10 kg) per mettere in equilibrio una bilancia a piatti o una leva: **peso × distanza** uguale dai due lati. **Multitouch**: ogni squadra ha la sua leva con la stessa sfida; vince il punto chi la mette per prima in equilibrio. **LIM**: una leva, a turni, con rubapunto (anche con il pulsante «Passa»). |
| `frazioni.html` | **Frazioni da spezzare** | Pizze, tavolette di cioccolato, nastri e biscotti da dividere e colorare con le dita (tocco o strisciata, anche più dita insieme), oppure risposte da scegliere. **Multitouch**: stessa sfida per le due squadre, vince il punto chi risolve per primo. **LIM**: a turni, con rubapunto e pulsante «Passa». |
| `circuiti.html` | **Circuiti elettrici** | Pezzi da trascinare dal vassoio nei buchi del circuito (o da toccare: prima il pezzo, poi il buco); gli interruttori si aprono e chiudono con un tocco. **Multitouch**: stessa sfida per le due squadre. **LIM**: a turni, con rubapunto e «Passa». In più, un **editor libero** per costruire qualsiasi circuito. |
| `energia.html` | **Città dell'energia** | Gioco di strategia, non un quiz: ogni squadra costruisce centrali sulla mappa con un budget e poi guarda scorrere la giornata (alba, giorno, sera, notte) con il grafico della richiesta e della produzione ora per ora. **Multitouch**: due squadre insieme, stessa mappa e stesso tempo. **LIM**: le squadre costruiscono a turno. Anche **una sola squadra** (tutta la classe) a schermo intero. |
| `tangram.html` | **Tangram** | I sette pezzi classici da trascinare sulla sagoma grigia: un tocco ruota il pezzo di 45°, tenendo premuto il parallelogramma lo si capovolge; i pezzi si agganciano da soli agli angoli vicini. Ogni modo corretto di riempire la sagoma va bene. **Multitouch**: stessa sagoma per le due squadre, più dita insieme. **LIM**: a turni, con rubapunto e «Passa». |
| `geopiano.html` | **Geopiano** | Una tavoletta con 9 × 9 chiodini: si tende l'elastico toccando un chiodino dopo l'altro (o trascinando il dito) e si chiude toccando il primo. Il gioco controlla da solo area, perimetro, lati, angoli retti, parallelismi e simmetrie. **Multitouch**: stessa sfida per le due squadre, ognuna sul suo geopiano. **LIM**: a turni, con rubapunto e «Passa». |

### Città dell'energia: impostazioni e fonti
- **Partita**: rapida (1 giorno) oppure campagna di 3 o 5 giorni (ogni giorno nuovi soldi, la città consuma di più, il tempo cambia: nuvole, niente vento, vento forte, siccità, ondata di caldo, inverno). **Tempo per costruire**: 45, 60, 90 secondi o senza limite. **Squadre in gioco**: due oppure una.
- **Centrali**: fotovoltaico, eolico, idroelettrico (rinnovabili); carbone, petrolio, gas naturale (combustibili fossili); piccola centrale nucleare; batterie di accumulo. Ogni centrale ha la sua scheda con la **catena delle trasformazioni di energia**, i pro e i contro. Il terreno conta (diga solo sul fiume, nucleare vicino all'acqua per il raffreddamento, pale più efficienti su costa e montagna, pannelli sulle colline).
- **Botte di fortuna** (rare, compaiono a caso): una sorgente geotermica ★ (centrale geotermica, produce sempre) e una baia con forti maree ★ (centrale mareomotrice, produce con la marea).
- **Cosa tenere d'occhio**: gli **indicatori** sotto la mappa. Notte, Mezzogiorno e Sera diventano verdi quando l'energia basta, oppure rossi con scritto quanti MW mancano. Ci sono anche il termometro della CO₂ (verde, giallo o rosso) e la barra delle rinnovabili. Mentre la giornata scorre, l'indicatore «Adesso» confronta ora per ora l'energia prodotta con quella richiesta e mostra la carica delle batterie.
- **Dove rende una centrale**: quando la tocchi nella tavolozza, sulla mappa ogni riquadro mostra la percentuale di rendimento. I riquadri sono verdi se va bene, gialli se rende poco, grigi se non si può costruire. La scheda della centrale dice che cosa trasforma, dove rende, pro e contro, costo, potenza e g di CO₂ per kWh. Il pulsante **? Guida** riassume le regole in qualsiasi momento.
- **🎓 Impara a giocare**: un tutorial guidato in 11 passi su una mappa fissa. Spiega perché i pannelli vanno sulle colline, le pale sulla costa, la diga sul fiume, a cosa servono le batterie e il gas la sera. Poi si guarda insieme la giornata e i punti.
- **🔬 Laboratorio delle centrali**: 10 mini giochi, ognuno con 2 o 3 sfide e una spiegazione dopo ogni sfida. Ogni mini gioco mostra la **catena dell'energia**, che si illumina mentre l'energia si trasforma.
  - **Il Sole sui pannelli**: ora del giorno, inclinazione e nuvole.
  - **Il vento e la pala**: si accende con circa 3 m/s; a vento doppio la potenza diventa 8 volte; oltre 25 m/s scatta il freno di sicurezza.
  - **La diga e la turbina**: si apre la paratoia; con la diga più alta si produce di più (Eₚ = m · g · h).
  - **Fuoco, vapore e turbina**: carbone, petrolio e gas a confronto con una tabella della CO₂. Si tocca ripetutamente il pulsante, anche con più dita.
  - **Dentro il reattore**: barre di controllo, reazione a catena, spegnimento di sicurezza, scorie.
  - **Il calore della Terra**: circa 3 °C in più ogni 100 m; nella zona normale non basta, a Larderello sì.
  - **Le maree**: il mare sale e scende, la corrente è più forte a metà marea.
  - **Le batterie e la sera**: la classe gestisce la rete e conserva il Sole di mezzogiorno per la sera.
  - **Le catene dell'energia**: si mettono in ordine le trasformazioni di 5 centrali; due carte non c'entrano.
  - **Tutto viene dal Sole?**: si dividono le fonti in due cesti, da una parte quelle che vengono dall'energia del Sole, dall'altra nucleare, geotermia e maree.
- **Punti del giorno**: energia fornita, nessun blackout (ogni ora al buio toglie punti), quota di rinnovabili, soldi risparmiati; si perdono punti per la CO₂ e per le scorie radioattive.
- **Dati usati (fonti ufficiali)**: emissioni di CO₂ nel ciclo di vita in g/kWh, valori mediani IPCC AR5 2014 (carbone 820, gas 490, fotovoltaico 48, geotermico 38, idroelettrico 24, maree 17, nucleare 12, eolico 11; petrolio 733 dalla World Nuclear Association); combustibile nucleare esaurito circa 25–28 t all'anno per un reattore da 1000 MW (World Nuclear Association); costi di costruzione IRENA 2023 (fotovoltaico 758 $/kW, eolico 1160 $/kW, idroelettrico 2806 $/kW, geotermico 4589 $/kW, batterie 273 $/kWh) e IEA/NEA (nucleare 2157–6920 $/kW; carbone e gas: intervalli OCSE, valori indicativi); consumi elettrici Terna 2023. Il costo della centrale mareomotrice e della centrale a petrolio è stimato. Nelle schede «Lo sapevi?»: Organizzazione Meteorologica Mondiale, IPCC, Accordo di Parigi, Agenda 2030, NOAA, e un'idea di Telmo Pievani (*La Terra dopo di noi*, Contrasto, 2019) riassunta, non citata alla lettera. Nel file c'è un elenco `CITAZIONI` dove il docente può aggiungere citazioni testuali dai libri usati in classe.

### Tangram: impostazioni
- Le sagome vengono **create dal gioco ogni volta** unendo i pezzi lato contro lato: c'è sempre una soluzione, e ogni sfida è nuova.
- **Livello** (sagome da comporre e domande sulle aree, estratte a caso):
  - *Base*: sagome di 2 pezzi; quanti triangoli piccoli servono per coprire un pezzo?
  - *Medio*: sagome di 3 pezzi; che frazione del quadrato intero è un pezzo? (il triangolo grande è un quarto, il triangolo piccolo un sedicesimo…)
  - *Avanzato*: sagome di 4 o 5 pezzi; due figure hanno la stessa area? (equiscomposizione)
  - *Esperto*: sagome di 6 pezzi; se il triangolo piccolo vale 1, quanto vale l'area della sagoma?
  - *Campione*: sagome con tutti e 7 i pezzi oppure «ricomponi il quadrato»; che frazione del quadrato è la sagoma?
  - *Crescente*: dal base al campione.
- **Aiuto «linee dentro la sagoma»**: nei livelli base e medio si vedono i contorni dei pezzi dentro la sagoma.
- **Tempo**: per sfida (multitouch) oppure per turno (LIM). A tempo scaduto i pezzi vanno da soli al loro posto, per mostrare una soluzione.

### Circuiti elettrici: impostazioni
- Un vero simulatore: le lampadine brillano di più o di meno secondo come sono collegate (legge di Ohm), il motore gira, il cicalino suona; un cortocircuito viene riconosciuto e segnalato.
- **Disegno del circuito**: realistico (tavoletta verde, fili di rame, lampadine che si illuminano) oppure **schema elettrico** con i simboli normalizzati dei libri di testo (pila con trattino lungo + e corto −, lampadina ⊗, resistore rettangolare, motore M, interruttore aperto/chiuso).
- **Livello** (3–4 tipi di sfida per livello, estratti a caso):
  - *Base*: chiudi il circuito; trova l'oggetto conduttore (chiave, moneta, graffetta, forchetta) tra gli isolanti (gomma, plastica, legno, vetro, carta); fai suonare il cicalino.
  - *Medio*: due lampadine in serie; accendi solo le lampadine richieste con gli interruttori; che cosa succede se apri un interruttore?; motore e lampadina.
  - *Avanzato*: due lampadine in parallelo che brillano al massimo; tre lampadine e quattro interruttori; trova e togli il cortocircuito; quante lampadine sono accese?
  - *Esperto*: due interruttori in serie (servono chiusi tutti e due); due interruttori in parallelo (ne basta uno); lampadina sempre accesa e motore comandato; che cosa succede con tre lampadine?
  - *Campione*: legge di Ohm, I = V/R (scritta con la linea di frazione); resistori in serie; quale lampadina brilla di più?; interruttore generale più un interruttore per ogni lampadina.
- **Editor libero** (pulsante «Apri l'editor» nelle impostazioni): si costruisce qualsiasi circuito sul reticolo con pila, filo, lampadina, interruttore, motore, cicalino, resistore e oggetti; a lato si leggono le misure (intensità di corrente in ampere in ogni componente) e l'eventuale cortocircuito.
- **Aiuto «mostra la corrente»**: la corrente scorre animata nei fili.

### Geopiano: impostazioni
- **Livello** (3–4 tipi di sfida per livello, estratti a caso):
  - *Base*: copia la figura del modello; rettangolo con l'area data; figura con un certo numero di lati.
  - *Medio*: figura con l'area data (anche «che non sia un rettangolo»); figura con il perimetro dato (lati orizzontali e verticali); triangolo rettangolo con l'area data; che area ha questa figura?
  - *Avanzato*: rettangolo con area e perimetro dati; quadrato «storto»; figura simmetrica rispetto a un asse; parallelogramma non rettangolo.
  - *Esperto*: area data con il perimetro più piccolo possibile; triangolo isoscele; trapezio; triangolo ottusangolo.
  - *Campione*: area data con un numero preciso di chiodini interni (teorema di Pick); Pitagora (ipotenusa o lato obliquo lungo 5); perimetro di una figura con lati obliqui; stessa area ma perimetro più grande.
  - *Crescente*: dal base al campione.
- **Aiuto «mostra area e perimetro»**: sì (si vedono lati, area e perimetro, e il motivo per cui una figura non va bene) o no.
- **Sfide**: 5, 8 o 10. **Tempo**: per sfida (multitouch) oppure per turno (LIM). Riepilogo finale con una soluzione per ogni sfida.

### Frazioni da spezzare: impostazioni
- **Livello** (ogni livello ha 3–4 tipi di sfida, estratti a caso; nelle domande a scelta ci sono sempre 2 risposte plausibili e 1 molto sbagliata):
  - *Base*: colora la frazione su un oggetto già diviso; che frazione è colorata?; colora la frazione di un gruppo di biscotti.
  - *Medio*: dividi tu l'oggetto (pulsanti + e −) e colora (vale anche una frazione equivalente); quale figura mostra la frazione?; frazione di una quantità (i 3/4 di 12 biscotti).
  - *Avanzato*: frazioni equivalenti (2/3 su una tavoletta da 12 quadretti); confronto tra due frazioni; frazione equivalente con un denominatore diverso; riduzione ai minimi termini.
  - *Esperto*: addizioni e sottrazioni da colorare su nastro o pizza; problemi inversi («6 biscotti sono i 2/5 della scatola: quanti in tutto?»).
  - *Campione*: frazioni maggiori dell'intero (7/4, «1 e 1/3») su due pizze o due nastri; frazione di una frazione; «quanto resta?»; la frazione più grande.
  - *Crescente*: dal base al campione, sfida dopo sfida.
- **Sfide**: 5, 8 o 10. **Aiuto «mostra la frazione colorata»**: sì / no. **Tempo**: per sfida (multitouch) oppure per turno (LIM).
- A fine partita: riepilogo con la soluzione di ogni sfida.

### Leve e bilance: impostazioni
- **Livello** (ogni livello ha 3 tipi di sfida, estratti a caso):
  - *Base*, bilancia a piatti: stessi chili dai due lati; piatto già in parte occupato da completare; minor numero di oggetti possibile.
  - *Medio*, leva con un oggetto a sinistra: bilancialo con un solo oggetto diverso; hai un solo tipo di oggetto e scegli la distanza; la tacca è decisa e scegli l'oggetto.
  - *Avanzato*, due oggetti a sinistra: oggetti liberi; minor numero di oggetti; un oggetto fisso anche a destra.
  - *Esperto*: usa tutti e soli gli oggetti dati; usa esattamente 3 oggetti; oggetti dati più un oggetto fisso a destra.
  - *Campione*, scatole misteriose: dopo l'equilibrio bisogna dire quanto pesa la scatola (una scatola con o senza un altro oggetto, due scatole uguali, oppure gli oggetti obbligati).
  - *Crescente*: dal base al campione, sfida dopo sfida.
- **Sfide**: 5, 8 o 10. **Aiuto «mostra i calcoli»**: sì (si vede peso × distanza dei due lati) o no (si vede solo da che parte pende).
- **Tempo**: per sfida (multitouch) oppure per turno (LIM). Quando nessuno ci riesce, compare una soluzione possibile.
- A fine partita: riepilogo di tutte le sfide con una soluzione per ciascuna.
### Caccia alle coppie: impostazioni
- **Coppie da cercare**:
  - *Matematica*: operazioni e risultati, frazioni-decimali-percentuali, potenze e radici, equivalenze, figure piane (disegno, nome, formula dell'area), solidi (disegno, nome, facce-vertici-spigoli, formula del volume), equazioni e soluzioni.
  - *Scienze*: grandezze e unità di misura (anche formula ↔ grandezza), strumenti di misura, formule in azione (es. "120 km in 2 h" ↔ "60 km/h", anche con formule inverse), materia ed elementi, energia ed elettricità, viventi e corpo umano, Terra e Universo.
- **Difficoltà**: Base, Medio, Avanzato, Esperto, Campione, oppure Crescente (dal primo all'ultimo round). A livello **Esperto** e **Campione** ogni round contiene «famiglie» di coppie che si somigliano apposta (per esempio x + 3 = 12, x − 3 = 12, 3x = 12, x : 3 = 12; oppure Na, N, Ne, Ni; oppure area e perimetro delle stesse figure): la soluzione è una sola, ma bisogna ragionare. **Round**: 1, 3 o 5. **Coppie per round**: 4, 6 o 8.
- Nello stesso round non compaiono mai due coppie con lo stesso valore (per esempio 3² → 9 e √81 → 9), così ogni carta ha una sola compagna.
- **Tempo**: per round (multitouch) oppure per mossa (LIM).
- A fine partita: risultato e riepilogo di tutte le coppie, round per round.

### Duello a squadre: impostazioni
- **Argomenti** (si scelgono uno per uno, oppure "tutti / nessuno" per gruppo). Le domande sono generate a caso ogni volta.
  - *Matematica*: calcolo mentale, potenze e radici, frazioni e percentuali, equivalenze, solidi, equazioni.
  - *Scienze*: velocità e moto, densità e galleggiamento, forze peso e pressione, calore e temperatura, materia ed elementi, energia ed elettricità, viventi e corpo umano, Terra e Universo. Dal livello medio in su si usano anche le **formule inverse** (tempo da spazio e velocità, massa da densità e volume, forza da pressione e superficie…). Molte domande mostrano la **spiegazione** dopo la risposta.
- **Tipo di sfida**:
  - *Classica*: come sempre.
  - *Velocità*: sullo schermo multitouch è una **raffica**. Ogni squadra ha le sue domande, una dopo l'altra, per 1, 1½ o 2 minuti, e vince chi ne indovina di più. Alla LIM è il gioco normale, ma con 5, 8 o 10 secondi per domanda.
  - *Ragionamento*: domande su cause, confronti, proporzioni ("se raddoppio…") e problemi da impostare.
- **Difficoltà**:
  - *Fissa*: Base, Medio, Avanzato, Esperto o Campione. Il livello Campione è il più difficile: problemi a più passaggi, formule inverse combinate, trabocchetti.
  - *Crescente*: si parte dal livello base e si arriva al campione. Nella raffica si sale di livello ogni 4 risposte giuste.
  - *Su misura*: si sceglie quante domande per livello (es. 4 base, 6 medie, 3 avanzate, 1 esperta).
- **Risposte**: nelle domande con risposta numerica, tra le 3 sbagliate ce ne sono sempre **2 plausibili** (gli errori tipici) e **1 molto sbagliata**.
- **Domanda bonus finale**: livello campione, vale 3 punti e ha il doppio del tempo.
- **Domande**: 10, 15 o 20. **Tempo per domanda**: senza limite, 15, 20, 30, 45 o 60 secondi.
- **Squadre** (multitouch): affiancate (schermo a parete) oppure una di fronte all'altra (schermo appoggiato come un tavolo).
- **Suoni**: sì / no.
- A fine partita: risultato e riepilogo di tutte le domande con la risposta giusta.

## Pubblicare su GitHub
Si può creare un repository apposta (per esempio `giochi-multitouch`), caricare i file e attivare GitHub Pages (Settings → Pages → Deploy from a branch → `main` / root). Il launcher sarà poi online su `https://<utente>.github.io/giochi-multitouch/` e da lì si aprono tutti i giochi.

## Crediti
Caratteri Google Fonts: Baloo 2 e Nunito (SIL Open Font License). Senza internet la pagina funziona comunque, con i caratteri di sistema.
