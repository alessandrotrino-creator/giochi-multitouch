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

I giochi si aggiungono uno alla volta. Tra le idee per i prossimi ci sono: caccia alle coppie, geopiano collaborativo, tangram, frazioni da spezzare, circuiti elettrici, leve e bilance, linea del tempo.

## Giochi

| File | Gioco | Come si gioca |
|---|---|---|
| `duello.html` | **Duello a squadre** | Due squadre, la stessa domanda con 4 risposte. Tre modi di gioco: **Multitouch** (lo schermo è diviso in due e si risponde tutti insieme: vince il punto chi tocca per primo la risposta giusta; chi sbaglia resta bloccato 2 secondi); **LIM a turni** con rubapunto; **LIM con prenotazione** (pulsante grande di ogni squadra, oppure tasti A e L della tastiera). |

### Duello a squadre: impostazioni
- **Argomenti** (si scelgono uno per uno, oppure "tutti / nessuno" per gruppo). Le domande sono generate a caso ogni volta.
  - *Matematica*: calcolo mentale, potenze e radici, frazioni e percentuali, equivalenze, solidi, equazioni.
  - *Scienze*: velocità e moto, densità e galleggiamento, forze peso e pressione, calore e temperatura, materia ed elementi, energia ed elettricità, viventi e corpo umano, Terra e Universo. Dal livello medio in su si usano anche le **formule inverse** (tempo da spazio e velocità, massa da densità e volume, forza da pressione e superficie…). Molte domande mostrano la **spiegazione** dopo la risposta.
- **Tipo di sfida**:
  - *Classica*: come sempre.
  - *Velocità*: sullo schermo multitouch è una **raffica**. Ogni squadra ha le sue domande, una dopo l'altra, per 1, 1½ o 2 minuti, e vince chi ne indovina di più. Alla LIM è il gioco normale, ma con 5, 8 o 10 secondi per domanda.
  - *Ragionamento*: domande su cause, confronti, proporzioni ("se raddoppio…") e problemi da impostare.
- **Difficoltà**:
  - *Fissa*: Base, Medio o Avanzato.
  - *Crescente*: si parte dal livello base e si arriva all'avanzato. Nella raffica si sale di livello ogni 4 risposte giuste.
  - *Su misura*: si sceglie quante domande per livello (es. 4 base, 6 medie, 3 avanzate).
- **Domanda bonus finale**: livello esperto, vale 3 punti e ha il doppio del tempo.
- **Domande**: 10, 15 o 20. **Tempo per domanda**: senza limite, 15, 20, 30, 45 o 60 secondi.
- **Squadre** (multitouch): affiancate (schermo a parete) oppure una di fronte all'altra (schermo appoggiato come un tavolo).
- **Suoni**: sì / no.
- A fine partita: risultato e riepilogo di tutte le domande con la risposta giusta.

## Pubblicare su GitHub
Si può creare un repository apposta (per esempio `giochi-multitouch`), caricare i file e attivare GitHub Pages (Settings → Pages → Deploy from a branch → `main` / root). Il gioco sarà poi online su `https://<utente>.github.io/giochi-multitouch/duello.html`.

## Crediti
Caratteri Google Fonts: Baloo 2 e Nunito (SIL Open Font License). Senza internet la pagina funziona comunque, con i caratteri di sistema.
