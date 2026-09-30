# Giochi multitouch

Giochi a squadre per lo schermo multitouch della scuola e per la LIM, pensati per la scuola secondaria di primo grado.
Ogni gioco è una sola pagina web: si apre con il browser, senza installare nulla, e non salva né invia dati.

## Il progetto
L'idea è sfruttare uno schermo multitouch grande come spazio di gioco condiviso: più studenti toccano lo schermo **nello stesso momento** e le squadre si sfidano faccia a faccia, invece di aspettare il proprio turno. Ogni gioco ha anche una **versione per la LIM**, che di solito riconosce un tocco alla volta.

- **Per chi:** classi della scuola secondaria di primo grado, soprattutto per matematica e scienze. Altri ambiti verranno aggiunti in seguito.
- **Come si usa in classe:** per ripassare, come attività di apertura o di chiusura della lezione, o come sfida tra squadre. Le domande sono generate a caso ogni volta, quindi si può rigiocare senza ripetere le stesse domande.
- **Dosare la difficoltà:** si scelgono gli argomenti e il livello. Il livello può restare fisso, salire durante la partita oppure essere composto su misura, con una domanda bonus finale. Dopo molte risposte compare una breve spiegazione, così anche l'errore diventa un'occasione per imparare.
- **Senza complicazioni:** niente account, niente installazioni, nessun dato degli studenti. Serve solo un browser: si apre il file dal computer oppure dal sito, se il progetto è pubblicato con GitHub Pages.
- **Scritto in italiano**, con la notazione usata a scuola: `·` e `:` per moltiplicazione e divisione, virgola decimale, frazioni in colonna.

I giochi si aggiungono uno alla volta e si aprono tutti dalla pagina iniziale `index.html` (il launcher). Tra le idee per i prossimi ci sono: geopiano collaborativo, tangram, frazioni da spezzare, circuiti elettrici, linea del tempo.

## Giochi

La pagina `index.html` è il **launcher**: mostra tutti i giochi con una tessera grande da toccare. Ogni gioco ha in alto il link «← Tutti i giochi» per tornare lì.

| File | Gioco | Come si gioca |
|---|---|---|
| `duello.html` | **Duello a squadre** | Due squadre, la stessa domanda con 4 risposte. Tre modi di gioco: **Multitouch** (lo schermo è diviso in due e si risponde tutti insieme: vince il punto chi tocca per primo la risposta giusta; chi sbaglia resta bloccato 2 secondi); **LIM a turni** con rubapunto; **LIM con prenotazione** (pulsante grande di ogni squadra, oppure tasti A e L della tastiera). |
| `coppie.html` | **Caccia alle coppie** | Carte da abbinare (figura–nome, operazione–risultato, grandezza–unità, strumento–che cosa misura…). **Multitouch**: ogni squadra ha le sue carte e tutti giocano insieme; si trascina una carta sulla compagna oppure si toccano una dopo l'altra, e chi finisce per primo il round prende 2 punti in più. **LIM**: un solo tabellone, a turni, con carte **scoperte** oppure **coperte** (memory). |
| `leve.html` | **Leve e bilance** | Oggetti veri da trascinare (bottiglia d'acqua da 1 kg, mattone 2 kg, zucca 3 kg, pesetto 4 kg, anguria 5 kg, secchio d'acqua 10 kg) per mettere in equilibrio una bilancia a piatti o una leva: **peso × distanza** uguale dai due lati. **Multitouch**: ogni squadra ha la sua leva con la stessa sfida; vince il punto chi la mette per prima in equilibrio. **LIM**: una leva, a turni, con rubapunto (anche con il pulsante «Passa»). |

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
