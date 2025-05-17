[[Sistemi e reti(Internetworking).pdf#page=296&selection=9,1,12,9&color=yellow|Instaurazione della sessione TCP: Three-Way Handshake]]

La comunicazione tra host mittente (tipicamente un client) e host destinatario (tipicamente un server) a livello TCP è di tipo connection-oriented, quindi sono previste 3 fasi:
- **instaurazione della sessione TCP** (**Three-Way Handshake**): è la fase in cui avviene il colloquio iniziale tra client e server, in cui ==si scambiano i dati di impostazione, utili al trasferimento successivo delle informazioni==; *(Connessione (lvl. 4)*
- ==trasmissione dati==: è la fase in cui avviene la trasmissione delle informazioni vere e proprie. Poiché TCP offre un servizio affidabile (reliable) si attuano meccanismi per il ==controllo degli errori==, per il ==controllo di flusso== e per il ==controllo della congestione==, al fine di prevenire la perdita dei dati trasmessi, mantenere la giusta sequenza ed eliminare eventuali duplicati;
- **abbattimento della sessione TCP** (**Doublé Two-Way Handshake**): questa fase è anche detta *disconnessione*, il protocollo prevede più modalità per terminare la comunicazione tra client e server. Principalmente si ha il Three-Way Handshake se la chiusura è contemporanea, il Double Two-Way Handshake se la chiusura avviene in tempi diversi.

Prima di vedere le 3 fasi ricordiamo che il dialogo avviene attraverso le Socket con l’utilizzo delle primitive.

La [[Sistemi e reti(Internetworking).pdf#page=296&selection=97,0,98,0&color=yellow|TABELLA 2]] mostra un tipico insieme di **primitive** usate per implementare i servizi del TCP. Mittente e destinatario comunicano mediante messaggi detti **TPDU** (Transport Protocol Data Unit), che nelle specifiche vengono anche chiamati **segmenti**

Affinché si possa instaurare una sessione TCP tra host 1 e host 2 occorre che quest’ultimo acconsenta mediante una sequenza che prevede tre passi e che viene chiamata Three-Way Handshake (stretta di mano a tre vie) illustrata in [[Sistemi e reti(Internetworking).pdf#page=297&selection=4,0,4,9&color=yellow|FIGURA 16]].
1. L’host 1 invia un segmento TCP con il flag SYN impostato a **1**. Invia inoltre un numero di sequenza, scelto in modo casuale, che diventa il suo sequence number (**X**). Primitiva usata: connect().
2. L’host 2, se acconsente a stabilire la connessione, risponde con una conferma mediante il flag ACK.F impostato a **1** e l’acknowledgment number impostato al valore ricevuto del sequence number +1 (**X** + **1**). Inoltre, per stabilire la connessione nella direzione inversa (full-duplex), l’host 2 imposta il proprio flag SYN.F a **1** e genera un suo numero di sequenza (**Y**), scelto in modo casuale, da inviare all’host 1. Primitiva usata: send().
3. L’host 1 risponde con un’ulteriore conferma mediante il flag ACK.F impostato a **1** e l’acknowledgment number impostato al valore, ricevuto dall’host 2, del sequence number incrementato di 1 (**Y** + **1**). Primitiva usata: send().

Se sull’host 2 non c’è nessun processo in ascolto sulla porta specificata nel campo destination port number, il passo **2** non viene eseguito e l’host 2 invia un segmento di risposta con flag RST = 1 per rifiutare la connessione.
Nella fase di setup è quindi importante che ogni host conosca il sequence number iniziale dell’altro. Altra informazione che si scambiano è la dimensione massima del segmento (**MSS** = Maximum Segment Size) che ogni host invierà all’altro; verrà scelta la dimensione minore e questo dato sarà particolarmente utile per il control lo della congestione. Infine si scambiano la dimensione della finestra TCP (windows size) che fornisce indicazioni sulla dimensione del buffer utilizzato per memorizzare i segmenti ricevuti.

**MTU** = ==Maximum Transfer Unit, è la dimensione massima del campo dati nel frame a livello Data Link== *(del trasmettitore)*; è un valore che caratterizza la rete di trasmissione utilizzata (per esempio per le reti Ethernet MTU = 1.500 byte). Ogni volta che IP deve inviare un pacchetto più grande della MTU è costretto a frammentare. TCP tiene conto di questo e, per avere maggiori prestazioni, fa coincidere la dimensione massima del segmento con la MTU.

**MRU** = Maximum Receive Unit, è la MTU del destinatario.

**MSS** = Maximum Segment Size, è la dimensione massima che possono avere i segmenti che si scambiano i due host, mittente e ricevente, ottenuta come il minimo tra i due valori MTU e MRU meno i 20 byte dell’header IP:

**MSS = min(MTU, MRU) - 20 byte**

In caso di mancanza di informazioni (dipende dalle implementazioni del TCP) viene utilizzato come valore di default 536 byte ottenuto nel seguente modo: 576 byte (default pacchetto IP) - 20 byte (header IP) - 20 byte (header TCP) = = 536 byte (MSS).

---
[[Sistemi e reti(Internetworking).pdf#page=298&selection=6,4,6,21&color=yellow|Trasmissione dati]]

La seconda fase della comunicazione TCP consiste nella trasmissione dei dati. TCP gestisce il **controllo di flusso** e gli **errori di trasmissione** (o perdita di pacchetti) con lo stesso meccanismo: il protocollo sliding window (a finestra scorrevole) affrontato nel volume del terzo anno.
Il protocollo utilizzato è quindi simile a quello visto per il controllo di flusso a livello Data Link. Ci sono, però, due differenze fondamentali:
- in TCP il puntatore nella finestra è al singolo byte, mentre a livello Data Link è al frame;
- in TCP la dimensione della finestra è variabile, mentre a livello Data Link è fissa.

Riprendiamo brevemente il problema che porta a utilizzare un meccanismo sliding Windows e supponiamo che:
- il destinatario abbia un buffer di ricezione di 2.000 byte; 
- il trasferimento dati tra mittente e destinatario avvenga correttamente: il processo applicativo invia dati al livello Transport che li trasmette in rete e i byte arrivano ordinatamente al livello Transport del destinatario che li riscontra (invio dell’ACK).

A un certo punto della trasmissione il processo destinatario non legge più i byte dal buffer di ricezione (perché si è bloccato oppure è impegnato in un’altra attività); che cosa succede allora quando il buffer è pieno e arriva un nuovo byte? È necessario che, prima che si verifichi questa situazione, il ricevente possa comuni care al mittente di sospendere momentaneamente la trasmissione, finché non sarà di nuovo pronto ad accettare dati. 

A livello Data Link la soluzione a questo problema è solitamente implementata nell’hardware della scheda di rete e si presuppone che i frame siano processati appena sono ricevuti.

In TCP invece la soluzione è a livello software, nel meccanismo di comunicazione tra TCP mittente e TCP destinatario:
- ogni volta che il ricevente invia un ACK indica, nel campo dell’header Windows size, il numero di byte che può accettare in quel momento;
- il mittente non invia un numero di byte superiore a quello indicato nell’ultimo ACK ricevuto;
- il ricevente non può rifiutarsi di accettare il numero di byte che aveva indicato nella finestra.

Si consideri l’esempio precedente supponendo che il buffer di ricezione sia occupa to per 1.000 byte, quindi il ricevente invia un ACK al mittente con l’indicazione che può accettare 1.000 byte. Il mittente allora invia 700 byte. Il ricevente invia un ACK per confermare la ricezione dei primi 500 byte, l’indicazione della dimensione della finestra non potrà essere inferiore a 200 byte, altrimenti vorrebbe dire che una parte dei 200 byte che sono ancora nella rete non sarà accettata.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=298&selection=90,0,95,65&color=yellow|In generale la dimensione della finestra viene scelta uguale allo spazio libero del buffer di ricezione del destinatario. Quando quest’ultimo non è in grado di rice vere altri byte perché il buffer è pieno, invia al mittente un messaggio di ACI< con dimensione della finestra pari a zero. Il mittente che lo riceve deve allora sospendere la trasmissione.]]
> > In generale la dimensione della finestra viene scelta uguale allo spazio libero del buffer di ricezione del destinatario. Quando quest’ultimo non è in grado di ricevere altri byte perché il buffer è pieno, invia al mittente un messaggio di ACK con dimensione della finestra pari a zero. Il mittente che lo riceve deve allora sospendere la trasmissione.

La conferma negativa (NACK = Not ACKnowledged, cioè non ricevuto) non esiste in TCP, quindi il protocollo prevede un meccanismo di timeout, che evita l’attesa infinita del riscontro al segmento inviato.
Tale meccanismo a finestre scorrevoli è il **Go-back-N** con timeout ([[Sistemi e reti(Internetworking).pdf#page=299&selection=4,0,4,9&color=yellow|FIGURA 17]]) che abbiamo visto nel volume di terza.
Allo scadere del timeout il segmento non riscontrato viene nuovamente inviato e sono ritrasmessi tutti i segmenti spediti successivamente, anche se alcuni di questi so no già stati ricevuti correttamente. Il mittente deve quindi mantenere in memoria i segmenti trasmessi, ma non ancora riscontrati. *(guardare su quaderno)*

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=299&selection=93,0,114,87&color=yellow|Con questa tecnica si risolve sia il problema di ricezione di segmenti danneggiati (il destinatario capisce che il segmento non è corretto dall’informazione contenuta nel campo checksum e lo scarta), sia quello di ricezione di segmenti fuori sequen za (out of order). Infatti in entrambi i casi il destinatario invia nuovamente un ACI< per l’ultimo segmento ricevuto correttamente, cioè integro e nel giusto ordine, e quando il mittente riceve un ACI< duplicato, lo interpreta come NACK per il seg mento seguente, che viene quindi ritrasmesso insieme a tutti i successivi già inviati. Anche la gestione di eventuali segmenti duplicati è risolta in modo semplice in TCP. Quando un mittente non riceve PACK prima dello scadere del timer, assume che il seg mento non sia giunto a destinazione e lo invia nuovamente. Il destinatario che riceve un segmento con lo stesso numero di sequenza di uno già ricevuto si limita a scartarlo.]]
> > Con questa tecnica si risolve sia il problema di ricezione di **segmenti danneggiati** (il destinatario capisce che il segmento non è corretto dall’informazione contenuta nel campo checksum e lo scarta), sia quello di ricezione di **segmenti fuori sequenza**(out of order). Infatti in entrambi i casi il destinatario invia nuovamente un ACK per l’ultimo segmento ricevuto correttamente, cioè integro e nel giusto ordine, e quando il mittente riceve un ==ACK duplicato==, lo interpreta come NACK per il segmento seguente, che viene quindi ritrasmesso insieme a tutti i successivi già inviati. 
> > 
> > Anche la gestione di eventuali ==**segmenti duplicati**== è risolta in modo semplice in TCP. Quando un mittente non riceve PACK prima dello scadere del timer, assume che il seg mento non sia giunto a destinazione e lo invia nuovamente. Il destinatario che riceve un segmento con lo stesso numero di sequenza di uno già ricevuto si limita a scartarlo.

Infine, può accadere che un messaggio di ACK non giunga al mittente, ma questi po trebbe non venirne a conoscenza. Infatti in TCP il meccanismo del riscontro è cu mulativo, ossia ogni riscontro conferma che il destinatario ha ricevuto correttamente tutti i dati trasmessi fino al byte specificato nel messaggio. Per esempio se il destinatario invia un messaggio con acknowledgment number = 1301, significa che tutti i byte fino al 1300 sono stati ricevuti correttamente, quindi il fatto di aver perso un riscontro con acknowledgment number = 1151 passerebbe del tutto inosservato al mittente.
Quanto sopra descritto è evidenziato nell’esempio di Figura 17 che mostra come nell’ambito di una connessione attiva tra un host mittente (sender) e un host destinatario (receiver), ci sia una stretta relazione tra la dimensione della finestra, la per dita di segmenti e la congestione.

---
[[Sistemi e reti(Internetworking).pdf#page=300&selection=11,4,13,17&color=yellow|Abbattimento della sessione TCP: Double Two-Way Handshake]]

In precedenza si è visto che una connessione TCP è bidirezionale, quindi può essere vista come composta da due flussi di dati indipendenti, uno per ciascuna direzione.
==Quando un programma applicativo non ha più dati da inviare, comunica al TCP di chiudere la connessione in una direzione e questi, dopo aver trasmesso eventuali da ti ancora presenti nel suo buffer e ricevuto il relativo riscontro, inizia la procedura di abbattimento della connessione dal “suo” lato. Il TCP ricevente comunicherà al relativo programma applicativo che non riceverà più dati dall’altro utente==. Se l’host che ha ricevuto l’informazione di chiusura della connessione ha ancora dei dati da tra smettere, questi continueranno a essere inviati e l’host che li riceve li riscontrerà (invio dell’ACK), anche se ha già chiuso la connessione dal suo lato. Terminato l’invio dei dati ancora da trasmettere, la connessione verrà chiusa anche nell’altra direzione. Questa doppia chiusura prende il nome di Double Two-Way Handshake (stretta di mano doppia a due vie) ed è mostrata in [[Sistemi e reti(Internetworking).pdf#page=300&selection=49,0,50,0&color=yellow|FIGURA 18]].

Rispetto alla fase di instaurazione si notano due particolarità: 
- l’utilizzo del flag FIN (al posto del flag SYN) impostato a **1** dall’host 1 per comunicare l’intenzione di chiudere la sessione;
- la suddivisione in due tempi del passo 2 dovuta alla necessità di confermare immediatamente, tramite ACK.N = **X** + **1**, da parte dell’host 2 il ricevimento del SEQ.N = **X**, **indipendentemente dalla richiesta di chiusura**. Mentre è generalmente necessario un po’ di tempo per confermare il ricevimento del flag FIN = 1 dovendo essere prima informato il software applicativo dell’host 2 che la connessione è stata chiusa.

Se una connessione non può essere rilasciata secondo la procedura normale sopra descritta a causa, per esempio, di un’anomalia, TCP prevede una procedura di Reset: 
si invia un segmento con il bit **RST** impostato a **1**, che comporta la chiusura immediata della connessione, senza ulteriori scambi di segmenti.

---
[[Sistemi e reti(Internetworking).pdf#page=301&selection=13,0,13,13&color=yellow|Vulnerabilità]]

Le connessioni TCP possono essere soggette a diversi tipi di attacchi informatici. Ve diamo brevemente i principali.

- [[Sistemi e reti(Internetworking).pdf#page=301&selection=19,1,20,21&color=yellow|SYN -FLOODING]]  
	- E un tipo di attacco DoS (Denial of Service) relativo all apertura della connessione con la tecnica Three-Way Handshake. Un host invia molte richieste di connessioni al ser ver oggetto dell’attacco (letteralmente “lo inonda di segmenti SYN”). Il server risponde con altrettanti segmenti SYN-ACK a cui l’host mittente ovviamente non risponde con PACK. Il server si trova ad aver raggiunto il massimo numero di connessioni che è in grado di gestire e non accetta altre richieste di connessione, rimanendo in attesa degli ACK finali che non arrivano. Allo scadere di un timer il server abbatte le connessioni non completate, ma il fatto di ricevere continuamente delle richieste blocca comunque la sua normale attività. A seguito della “messa fuori rete” dell’host oggetto del SYN-Flooding, l’attaccante può realizzare altri tipi di attacchi come IP Spoofing.
	- **Contromisure**: aumentare la dimensione della coda di connessione (SYN ACK queue) e diminuire il tempo di timeout per il completamento della fase di Three-Way Handshake.

- [[Sistemi e reti(Internetworking).pdf#page=301&selection=42,0,44,8&color=yellow|SEQUENCE GUESSING]]
	- E un attacco che consiste nel riuscire a indovinare (guess) il numero di sequenza e nel generare, di conseguenza, dei segmenti TCP con mittente falsificato e formal mente corretti. Inoltre, si deve impedire la ricezione dei messaggi di risposta (ACK) da parte del vero mittente.
	- **Contromisure**: si configurano i router per non far entrare traffico che provenga dal la rete interna (ingress filtering).

- [[Sistemi e reti(Internetworking).pdf#page=301&selection=57,1,60,9&color=yellow|SESSION HIJACKING]]
	- Questo attacco consiste nel riuscire a inserirsi in una sessione attiva, sostituendosi a uno dei due host:
		- Z spia la connessione tra X e Y e registra i numeri di sequenza dei segmenti;
		- Z blocca Y (per esempio con un SYN-Flooding);
		- Z invia un segmento con il numero di sequenza corretto, con source Y, in modo che X non si accorga di nulla.
	- **Contromisure**: si configurano i router per non far entrare traffico che provenga dal la rete interna (ingress filtering).

---
[[G, CONFRONTO TRA I PROTOCOLLI UDP E TCP]]
