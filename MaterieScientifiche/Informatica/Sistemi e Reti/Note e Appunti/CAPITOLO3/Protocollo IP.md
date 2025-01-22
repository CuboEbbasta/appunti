> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=118&selection=23,0,26,81&color=important|II protocollo IP, nelle versioni 4 e 6 si occupa dell’indirizzamento, della suddivi sione in pacchetti e del trasferimento dei dati che arrivano dal Transport Layer.]]
> > II protocollo IP, nelle versioni 4 e 6 si occupa dell’indirizzamento, della suddivisione in pacchetti e del trasferimento dei dati che arrivano dal Transport Layer.

> II protocollo IP, nelle versioni 4 e 6 si occupa dell’==indirizzamento==, della ==suddivisione in pacchetti== e del ==trasferimento dei dati che arrivano dal Transport Layer==. **IP è connectionless**, dunque consente a due host di scambiarsi PDU, denominate **IP *datagram*** senza stabilire una connessione fisica.

**Datagram**: Il termine datagram è ==usato per indicare la PDU di un protocollo connectionless==, come IP o UDP (protocollo di livello Transport).

---
Il protocollo IP **aggiunge ai dati (payload) un header, della lunghezza minima di 20 byte**, **per formare il pacchetto** (massimo 65.535 byte) **da inoltrare al livello Physical**. I campi più importanti dell'header sono rappresentati dagli indirizzi IP del mittente e del destinatario. [[Sistemi e reti(Internetworking).pdf#page=118&selection=76,0,78,1|figura1]]

---
Il contenuto dei singoli campi è il seguente:

- **[[Sistemi e reti(Internetworking).pdf#page=119&selection=6,2,6,9|Version]]**: **4 bit che rappresentano la versione del protocollo IP** (0100 = versione 4); **se l’host destinatario non è in grado di gestire la versione del protocollo IP specificata**, **il pacchetto verrà scartato**.

- **[[Sistemi e reti(Internetworking).pdf#page=119&selection=12,2,12,6|HLEN]]** (Header LENgth): **4 bit che indicano la lunghezza dell’header IP espressa in double word** (gruppi di 32 bit). **Tutti i campi dell’header sono di lunghezza fissa tranne Options e Padding**, **se** questi **non** sono **presenti**, **l’header è lungo 20 byte**.

- **[[Sistemi e reti(Internetworking).pdf#page=119&selection=20,3,20,5|TOS]]** (Type Of Service): **8 bit che servono a far capire all’IP come gestire il pacchetto**. È costituito da 6 sottocampi:
	-==**`PRECEDENCE`**==: **3 bit che indicano la priorità del pacchetto**, da 0 (normale) a 7 (con trollo di rete); più il numero è alto più il pacchetto è importante.
	-==**`DELAY`**==: un bit che se impostato a 1 indica che si vuole un ritardo minimo.
	-==**`THROUGHPUT`**==: un bit che se impostato a 1 indica che si vuole un throughput massimo
	-==**`RELIABILITY`**==: un bit che se impostato a 1 indica che si vuole massima affidabilità.
	-==**`MONETARY CAST`**==: un bit che se impostato a 1 indica che si vuole il percorso dal costo minimo.
	-==**`UNUSED`**==: 1 bit inutilizzato. Nella versione 4 di IP è fissato a 0.

- **[[Sistemi e reti(Internetworking).pdf#page=119&selection=87,0,87,12|Total Length]]**: **16 bit che contengono la lunghezza totale del datagram espressa in byte** (header + payload) **che potrà** quindi **essere al massimo** 216- 1 = **65.535 byte**; **di norma**, però, **un pacchetto IP è** lungo **1.500 byte**, **così da poter essere trasportato interamente come payload nel frame Ethernet**.

- **[[Sistemi e reti(Internetworking).pdf#page=119&selection=98,0,99,0|Identification (ID), Flags e Fragment Offset]]**: sono **campi relativi alla funzione di frammentazione**: **a volte può essere necessario per un router dividere un datagram in pacchetti più piccoli**, **per consentirgli di attraversare una rete con caratteristiche diverse da quella di provenienza** (Ethernet, Token Ring, Wi-Fi, ecc.). 
	-==**`ID`**==: **16 bit che identificano univocamente i frammenti di un medesimo datagram**; **tutti i frammenti in cui è suddiviso un datagram avranno lo stesso ID**.
	-==**`FLAGS`**==: **3 bit per il controllo della frammentazione**:
	 - **Il primo bit è attualmente inutilizzato**;
	 - **Il secondo bit è detto DF** (Don’t Fragment): **se impostato a 1 indica che il datagram non può essere frammentato**;
	 - **Il terzo bit è detto MF** (More Fragment): **se impostato a 1 indica che il frammento è seguito da altri frammenti**; **solo l’ultimo frammento avrà** quindi **MF = 0**.
	-==**`FRAGMENT OFFSET`**==: **13 bit che indicano l’offset del frammento rispetto all’inizio del datagram**, **il valore indicato raggruppa 8 byte alla volta**. **L’offset è fissato dal router che esegue la frammentazione**.

Nella [[Sistemi e reti(Internetworking).pdf#page=119&selection=136,0,144,1|figura 2]] viene **esemplificato il contenuto dei campi** **ID**, **Flags** e **Fragment Offset nel caso di un datagram con payload di 1.500 byte** **suddiviso in 3 frammenti** di dimensione **600 byte**, **600 byte** e **300 byte** rispettivamente.

- **[[Sistemi e reti(Internetworking).pdf#page=120&selection=43,3,43,5|TTL]]** (Time To Live): **8 bit inizializzati al numero massimo di passaggi da un router al successivo (hop) che il datagram può effettuare**. **Il suo scopo è di evitare che un pacchetto continui a circolare nella rete all’infinito**. Il **TTL** è **usato come un contatore**, il cui **valore viene decrementato di 1 ogni volta che il datagram attraversa un router** e **quando arriva a 0 viene scartato**. Il *TTL raccomandato per IPv4 è 64* (RFC 791 e RFC 1122).

- **[[Sistemi e reti(Internetworking).pdf#page=120&selection=52,3,52,10&color=yellow|Protocol]]**: **8 bit usati per indicare quale protocollo di livello superiore è stato utilizzato per creare il payload**. ***Ogni protocollo è identificato da un numero**, detto **Assigned Internet Protocol Numbers***, per esempio: 1 = ICMP, 2 = IGMP, 6 = TCP, 17 = UDP (*l’elenco completo è reperibile sul sito IANA www.iana.org/assignments/protocol-numbers*). **È noto anche come SAP** (Service Address Point). **Questo valore è usato solo nell’host di destinazione**.

- **[[Sistemi e reti(Internetworking).pdf#page=120&selection=70,2,70,17&color=yellow|Header Checksum]]**: **16 bit usati per il calcolo della checksum relativa al solo header**, **per rilevare eventuali bit errati nell’IP datagram ricevuto dal router**. *In ogni router attraversato viene ricalcolata essendosi modificato l’header per via del decremento del valore TTL*.

- **[[Sistemi e reti(Internetworking).pdf#page=121&selection=4,2,4,19|Source IP Address]]**: **32 bit dell’indirizzo IP del mittente**.
- **[[Sistemi e reti(Internetworking).pdf#page=121&selection=8,2,8,24&color=yellow|Destination IP Address]]**: **32 bit dell’indirizzo IP del destinatario**.

- **[[Sistemi e reti(Internetworking).pdf#page=121&selection=12,2,12,9|Options]]**: **ogni opzione è lunga 8 bit e un datagram può contenere più opzioni**. **Gli 8 bit di un’opzione sono suddivisi in 3 campi**:
	-==**`COPY FLAG`**==: **1 bit** che **impostato a 0** indica che, *in caso di frammentazione*, **l’opzione va copiata solo sul primo frammento**; **se impostato a 1 invece va copiata su tutti i frammenti**.
	-==**`OPTION CLASS`**==: **2 bit** che i**mpostati al valore 0** indicano che **l’opzione è di controllo del datagram o della rete**; **impostati al valore 2** indicano che **l’opzione serve per debug o misurazioni**; **i valori 1 e 3 sono riservati a usi futuri**.
	-==**`OPTION NUMBER`**==: **5 bit che identificano l’opzione nell’ambito della Option Class di appartenenza**. Per esempio:
	 - *Option Class = 0* e *Option Number = 0*: **fine delle opzioni**;
	 - *Option Class = 0 e Option Number = 1*: **riempitivo in caso di nessuna opzione impostata**;
	 - *Option Class = 0 e Option Number = 7*: ==**costringe i router ad aggiungere il proprio IP all’elenco delle opzioni**==; *è usato quando si vuole tenere traccia dei percorsi (record route)*;
	 - *Option Class = 2 e Option Number = 4*: **==costringe i router ad aggiungere un segnatempo (time stamp)== in millisecondi per ricostruire il tempo impiegato da un pacchetto lungo una strada**.
	
	*Le opzioni sono registrate sul sito IANA, dove si trova l’elenco completo e aggiornato: “IP Option Numbers” www.iana.org/assignments/ip-parameters*

- **[[Sistemi e reti(Internetworking).pdf#page=121&selection=59,0,59,7|Padding]]**: **riempitivo con dati fittizi la cui dimensione dipende dal numero di opzioni presenti**. *È usato per rendere l’header di lunghezza multipla di 32 byte*.

---
[[Struttura degli indirizzi IP]]