
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=288&selection=14,0,33,16&color=yellow|Transmission Control Protocol è un protocollo di trasporto molto diffuso, più dell’UDP, in quanto offre un servizio connection-oriented e affidabile, garan tendo quindi la consegna dei dati in modo ordinato (infatti si parla di data stream inteso come flusso di byte).]]
> > ==Transmission Control Protocol== è un protocollo di trasporto molto diffuso, più dell’UDP, in quanto offre un servizio ==connection-oriented e affidabile==, garantendo quindi la consegna dei dati in modo ordinato (infatti si parla di d*ata stream* inteso come *flusso di byte*).
> 

La [[Sistemi e reti(Internetworking).pdf#page=288&selection=37,0,40,0&color=yellow|FIGURA 12]] mostra come i numeri di sequenza dei segmenti TCP siano usati per ricostruire il messaggio originale ponendo i segmenti nel giusto ordine.

La connessione che TCP stabilisce tra mittente e destinatario offre all’applicazione, che si trova al livello superiore, l’impressione di usufruire di una linea dedicata. ==La connessione può==, quindi, ==essere intesa come un canale logico== le cui caratteristiche sono:
- **full-duplex**: ==sulla stessa connessione si può trasmettere e ricevere in contemporanea==; 
- **point-to-point**: ==un solo mittente e un solo destinatario==;
- ==richiede l’inizializzazione di **variabili di stato** da parte del mittente e del ricevente== (i due processi si devono accordare prima di iniziare il trasferimento dati).

==TCP usa più risorse del computer host rispetto al protocollo UDP==, sia in termini di CPU (l’elaborazione è piuttosto complessa), sia in termini di memoria (ci sono maggiori informazioni di stato da memorizzare). Inoltre ==necessita di maggiore capacità trasmissiva== (banda) ==per via della ritrasmissione e dell’header più grande== (20 byte rispetto agli 8 di UDP).

==TCP si usa con applicazioni che richiedono una trasmissione affidabile dei dati==, per esempio le applicazioni che utilizzano i protocolli FTP (trasferimento file), SMTP (posta elettronica) e HTTP (trasferimento pagine web) che verranno descritti nell’Unità 8 dedicata all’Application Layer. Nel corso degli anni, sono stati definiti molti standard per TCP, tra questi: RFC 793, la prima specifica stabile; RFC 7323, che prende in considerazione il problema delle prestazioni (performance) definendo delle estensioni per migliorare l’efficienza; RFC 5681, che descrive gli algoritmi per il controllo della congestione della rete.

--- 
[[Sistemi e reti(Internetworking).pdf#page=289&selection=105,0,105,47&color=yellow|La comunicazione tra TCP e processo applicativo]]

Di regola i Sistemi Operativi permettono di accedere alle porte in modo sincrono, ciò implica che l’esecuzione del processo si interrompa durante un’operazione di accesso alla porta. 

A volte i dati ricevuti vengono scartati perché: 
- il processo di destinazione non è pronto a riceverli o il numero di porta di destinazione non esiste;
- non c’è spazio sufficiente nel buffer di ricezione per contenere tutti i dati.

**Un processo**, che vuole inviare un messaggio, **scrive il testo da spedire in un buffer nel suo spazio in memoria**, **inserisce le informazioni di controllo** (header) **e passa il controllo a TCP**. Analogamente, **un processo che deve ricevere un messaggio**, **definisce un buffer di ricezione nel suo spazio di memoria e passa il controllo a TCP** ([[Sistemi e reti(Internetworking).pdf#page=289&selection=128,1,130,2&color=yellow|FIGURA 13]]).

Le informazioni di controllo, che il processo deve passare al TCP, comprendono:
- **source address**: ==indirizzo completo del mittente== (network + host + port);
- **destination address**: ==indirizzo completo del destinatario== (network + host + port);
- **next packet sequence number**: ==il numero di sequenza che TCP deve assegnare al prossimo pacchetto che trasmetterà da quella porta==;
- **current buffer size**: ==la dimensione del buffer del mittente==;
- **next write position**: ==indirizzo dell’area del buffer in cui il processo pone i nuovi dati da trasmettere==;
- **next read position**: ==indirizzo dell’area del buffer da cui TCP deve leggere i dati per costruire il prossimo segmento da inviare==;
- **timeout/flag**: ==indica il tempo dopo il quale i dati non riscontrati (unacknowledged) devono essere ritrasmessi==; **il flag è usato per sincronizzare TCP e processo** (per esempio tramite l’uso di semafori), per segnalazioni di stato, ecc.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=290&selection=13,0,20,84&color=yellow|Quando un’applicazione passa dei dati a TCP, questi può salvarli in un buffer oppure spedirli subito; la bufferizzazione consente di migliorare l’efficienza della comuni cazione: i dati verranno spediti quando si raggiunge una certa quantità (Figura 13).]]
> > Quando un’applicazione passa dei dati a TCP, questi può salvarli in un **buffer** oppure **spedirli subito**; ==la bufferizzazione consente di migliorare l’efficienza della comunicazione: i dati verranno spediti quando si raggiunge una certa quantità== ([[Sistemi e reti(Internetworking).pdf#page=289&selection=128,1,130,2&color=yellow|FIGURA 13]]).

Lo standard prevede due eccezioni alla bufferizzazione:
- ==l’applicazione richiede che i dati vengano spediti immediatamente==, allora **imposta** a **1 il flag PUSH**, nell’header TCP, per indicare a questi di non bufferizzare e di inviare subito i dati; 
- ==l’applicazione imposta a 1 il flag URG dell’header TCP==: **i dati non vengono accumulati nel buffer e TCP trasmette immediatamente tutto ciò che riguarda quella connessione**. ==In ricezione==, quando arrivano i dati con il flag ==URG = 1==, ==l’applicazione interrompe la sua attività per esaminare immediatamente i dati urgenti==.

---
[[Sistemi e reti(Internetworking).pdf#page=290&selection=42,0,42,14&color=yellow|II segment TCP]]

I campi del segmento TCP ([[Sistemi e reti(Internetworking).pdf#page=290&selection=68,1,69,1&color=yellow|FIGURA 14]]) sono:
- **source port number** (16 bit): ==numero di porta sull’host del mittente==;

- **destination port number** (16 bit): ==numero di porta sull’host del destinatario==;

- **sequence number** (32 bit): ==numero di sequenza progressivo del primo byte di dati contenuto nel segmento==;

- **acknowledgment number** (32 bit): **numero di riscontro**, ==ha significato solo se il flag ACK è impostato a 1==, **conferma la ricezione di una parte del flusso di dati** ==indicando il valore del prossimo sequence number atteso== (implicitamente si conferma che i byte precedenti sono stati ricevuti correttamente);

- **header length** (4 bit): ==indica la lunghezza== (in *word da 32 bit*) ==dell’header del segmento TCP==; tale lunghezza può variare da 5 word (20 byte) a 15 word (60 byte) a **seconda della presenza e della dimensione** del ==campo facoltativo Options==. Serve quindi a indicare l’inizio dei dati del segmento;

- **not used** (4 bit): ==bit attualmente non utilizzati==; devono essere impostati a zero; 

- **flags** (8 bit): ==bit utilizzati per il controllo del protocollo==:
	- **CWR** (Congestion Window Reduced) se impostato a 1 indica che l’host sorgente ha ricevuto un segmento TCP con il flag ECE impostato a 1 e ha di conseguen za abbassato la sua velocità di trasmissione per ridurre la congestione ed evitare la perdita di pacchetti;
	- ECE (ECN-Echo) se impostato a 1 indica che l’host supporta ECN (Explicit Congestion Notification) durante il Three-Way Handshake;
	- ==**URG**== ==se impostato a 1== indica che ==nel flusso sono presenti dati urgenti e quindi si deve leggere il campo urgent pointer==;
	- ==**ACK**== se ==impostato a 1== **indica che il segmento TCP in questione è in risposta a un altro ricevuto**, che conteneva dati, di conseguenza indica ==che il campo acknowledgment number è valido e si devono leggere le informazioni in esso contenute==;
	- PSH (push) se impostato a 1 indica che i dati in arrivo non devono essere bufferizzati, ma passati subito ai livelli superiori dell’applicazione;
	- ==**RST**== (reset) ==se impostato a 1 indica che la connessione non è valida==; viene utilizzato in caso di ==grave errore==; a **volte utilizzato insieme al flag ACK**, per la ==chiusura di una connessione==;
	- ==**SYN**== (SYNchronize sequence numbers) è **usato nella fase di instaurazione di una connessione**; ==se impostato a 1 indica che l’host mittente del segmento vuole aprire una connessione== TCP ==con l’host destinatario e specifica nel campo sequence number il valore dell’Initial Sequence Number== (ISN), **per sincronizzare i numeri di sequenza dei due host**. *L’host ricevente invia poi la risposta SYN-ACK con SYN = 1*. Questo flag deve essere usato solo in questi due casi;
	- ==**FIN**== (final) ==se impostato a 1== indica che ==l’host mittente del segmento non ha più dati da inviare e vuole *chiudere la connessione*== TCP. **Il ricevente invia la conferma di chiusura con un FIN-ACK**. A questo punto la connessione è ritenuta chiusa in un verso: ==l’host che ha inviato il FIN non potrà più inviare dati==, **mentre l’altro host ha il canale di comunicazione ancora disponibile**. *Quando anche l’altro host invierà il pacchetto con FIN = 1 la connessione, dopo il relativo FIN-ACK, sarà considerata completamente chiusa*;

- **window size** (16 bit): ==è usato dall’host ricevente per dire al mittente quanti dati può ricevere in quel momento== (**finestra di ricezione**), **cioè il numero di byte che il mittente può spedire a partire dal byte confermato** (specificato dall’acknowledgment number). I*l valore 0 indica di non inviare altri dati per il momento*; ==quando il ricevente sarà di nuovo in grado di ricevere dati invierà al mittente un segmento con window size diverso da 0 ma con lo stesso acknowledgment number==;

- **checksum** (16 bit): ==è utilizzato== per la ==verifica della validità del segmento==. L’algoritmo di calcolo è definito nell’RFC ed è del tutto simile a quello di ==UDP==, ==l'unica differenza è che per TCP il campo è obbligatorio==. Se dal calcolo della checksum risultasse che il segmento TCP è stato danneggiato, non verrebbe riscontrata la sua ricezione e quindi il mittente lo dovrebbe ritrasmettere;

- **urgent pointer** (16 bit): ==ha significato solo se il flag URG = 1== **contiene il numero che deve essere sommato** (offset) **al sequence number per ottenere il numero dell’ultimo byte urgente nel campo dati del segmento**. *Questo campo consente all’applicazione di usare messaggi che* ==interrompono la normale elaborazione==; 

- **options**: ==campo facoltativo== che può avere dimensione variabile da 0 a 10 word (word = 32 bit). **L’opzione più importante è** quella che ==consente a un host di specificare la dimensione massima del segmento== che è in grado di accettare. Il default è 536 byte di dati e 20 byte di header (quindi ogni host deve poter gestire segmenti di almeno 556 byte); ==*contiene MSS (maximum segment size)*==

- data: ==contiene i dati da trasmettere provenienti dal livello superiore o, nell’altra direzione, i dati ricevuti dal livello inferiore==

---
[[E, LA GESTIONE DELLA CONGESTIONE]]