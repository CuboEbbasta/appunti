
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=284&selection=16,0,21,42&color=yellow|User Datagram Protocol è un protocollo del livello Transport che non prevede l'uso di una connessione tra host mittente e host destinatario: infatti ciascun da tagram UDP è trattato in modo indipendente]]
> > **User Datagram Protocol**, ==UDP è un protocollo== del livello Transport ==che non prevede l'uso di una connessione tra host mittente e host destinatario==: ==infatti ciascun datagram UDP è trattato in modo indipendente==

==ll servizio offerto da UDP è di tipo Best Effort== (come va, va): ==i datagram UDP possono essere persi o arrivare fuori sequenza==, ==non si ha== quindi ==alcuna garanzia sulla consegna dei dati trasmessi== ([[Sistemi e reti(Internetworking).pdf#page=284&selection=52,0,52,8&color=yellow|FIGURA 9]]). A prima vista quindi sembrerebbe non offrire un servizio significativamente diverso da quello offerto dal protocollo IP, in realtà non è così: ==UDP fornisce le funzionalità tipiche del livello Transport in termini di **multiplexing**, grazie all’uso delle porte, e di controllo dell’**integrità dei dati**== (il campo Checksum, però, è opzionale).

---
[[Sistemi e reti(Internetworking).pdf#page=285&selection=5,1,6,15&color=yellow|II datagram UDP]]

La [[Sistemi e reti(Internetworking).pdf#page=285&selection=29,1,31,1&color=yellow|FIGURA 10]] mostra il formato del datagram del protocollo UDP, i cui campi sono:
- **source port number** (16 bit): numero di porta sull'host del mittente;
- **destination port number** (16 bit): numero di porta sull’host del destinatario;
- **length** (16 bit): **contiene la lunghezza totale in byte del datagram** UDP (header + dati); 
- **checksum** (16 bit, **opzionale**): **contiene il codice di controllo del datagram** UDP. L’algoritmo di calcolo è definito nell’RFC del protocollo e copre il datagram UDP e parte dell’header IP. ==Se dal calcolo della checksum risulta che il datagram UDP è stato danneggiato, esso viene scartato==; 
- **data**: contiene le informazioni trasmesse/ricevute.

==La dimensione massima di un datagram UDP è 65.508 byte==. Infatti ==deve essere contenuto in un pacchetto IP che ha al massimo 64 KB (65.536 byte)== ai quali si devono togliere i 20 byte minimi dell’header IP, che porta ad avere un campo dati IP al massimo di 65.516 byte ai quali si devono ancora togliere gli 8 byte dell’header UDP. L’opzionalità del campo checksum consente alle implementazioni di lavorare con la massima velocità quando usano UDP su una rete altamente affidabile (come le reti LAN). Dal momento, però, che il protocollo IP non calcola la checksum sulla parte dei dati del pacchetto, ==il calcolo della checksum UDP permette di verificare se tutti i dati sono arrivati integri==. Quindi ==omettere questo campo vuol dire eliminare del tutto la possibilità di sapere se il messaggio è arrivato a destinazione in modo corretto==.

**Per quanto riguarda il multiplexing/demuitiplexing connectionless del protocollo UDP, possiamo distinguere le due fasi**: trasmissione in multiplexing e ricezione in demultiplexing. I passi e l’utilizzo dei campi del datagram nelle due fasi sono le seguenti.

- **Multiplexing**: il ==**datagram UDP** viene formato **aggiungendo l’header al messaggio ricevuto** dal livello applicativo==:
	- ==il campo source port viene preso dalla socket== attraverso cui è stato inviato il messaggio;
	- ==il campo destination port è un parametro della primitiva Data_Request== ricevuta dal livello applicativo;
	- ==viene calcolato il campo length==;
	- ==viene calcolato il campo checksum==
	- ==**ll datagram UDP così costruito viene inviato al livello Network, che vi aggiunge il proprio header in cui inserirà il numero 17 che identifica il protocollo di trasporto UDP**==.

- **Demultiplexing**:
	- ==viene ricevuto dal livello Network un datagram UDP==; 
	- se ne ==verifica l’integrità calcolando il suo valore di controllo e confrontandolo con quello contenuto nel campo checksum==;
	- si ==cerca la socket UDP associata al numero di porta contenuto nel campo destination port==;
	- ==la parte data, del datagram UDP, viene inviata alla socket individuata==; **se non viene trovata allora il datagram è respinto e viene generato un messaggio ICMP di porta non raggiungibile**
---
[[Sistemi e reti(Internetworking).pdf#page=286&selection=30,0,32,6&color=yellow|VANTAGGI DI UDP]]

 Alcuni dei vantaggi derivanti dall’uso di UDP sono:
 - ==non richiede di stabilire una connessione==: *non introduce un ritardo dovuto alla fase di setup della connessione*;
 - ==non mantiene lo stato della connessione==: *un server può supportare molti più client attivi*;
 - ==il sovraccarico dovuto all’intestazione del pacchetto è minimo==: *solo 8 byte contro i 20 di un protocollo connection-oriented*;
 - ==il controllo del livello applicativo è più efficace==: *in mancanza di un controllo della congestione, il mittente non viene mai bloccato*.
 ---
 [[Sistemi e reti(Internetworking).pdf#page=286&selection=53,0,53,8&color=yellow|UDP-Lite]]

Nel corso degli ultimi anni è sorta ==l’esigenza di non scartare i datagram UDP che risultano errati dopo il controllo del campo checksum==. Infatti, per certi tipi di applicazioni ==ricevere parte dei dati è meglio che non ricevere nulla==. Tipici ==esempi sono le applicazioni VoIP e di streaming audio/video che usano pacchetti con una gran quantità di dati==. Con il protocollo UDP tradizionale, **è sufficiente avere un byte errato per scartare tutto il datagram**, con conseguente impatto sulla qualità delle informazioni ricevute; ==con UDP-Lite, invece, si può salvare la parte di dati arrivata correttamente==. Per esempio, in una comunicazione *VoIP il ricevente riesce comunque a capire il contenuto informativo trasmesso da chi gli sta parlando*.

UDP-Lite fa parte del kernel di Linux dalla versione 2.6.20 in poi. Nella [[Sistemi e reti(Internetworking).pdf#page=286&selection=55,0,55,9&color=yellow|FIGURA 11]] è mostrato il formato del datagram UDP-Lite.

==Il controllo checksum come minimo si deve applicare agli 8 byte dell’header, al massimo a tutto il datagram UDP, in quest’ultimo caso il protocollo UDP-Lite si comporta esattamente come il protocollo UDP==.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=287&selection=11,0,21,36&color=yellow|Per soddisfare questa esigenza si è dovuto dare un’interpretazione diversa al campo length dell’header, che nel protocollo UDP-Lite assume il significato di checksum coverage length, ossia si deve specificare quanti byte del datagram UDP saranno controllati: solo 8 (header) o tutti]]
> > Per soddisfare questa esigenza si è dovuto dare un’interpretazione diversa al campo length dell’header, che nel protocollo UDP-Lite assume il significato di **checksum coverage length**, ossia si deve **specificare quanti byte del datagram UDP saranno controllati: solo 8 (header) o tutti**.

Si noti che non si *perde nessuna informazione* circa l**a lunghezza del datagram UDP** (che era il significato originario del campo length), in quanto questa **può essere dedotta dalla lunghezza del pacchetto IP ricevuto a cui si devono sommare gli 8 byte dell’header UDP**.

---

[[D, UN PROTOCOLLO DI TRASPORTO CONNECTION-ORIENTED TCP]]