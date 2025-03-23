Nonostante la serie di tecniche messe in campo per sopperire al limitato spazio degli in dirizzi offerto da IPv4 (indirizzi dinamici, indirizzi privati, la CIDR, le VLSM), la grande diffusione della rete Internet spinse, fin dagli anni Novanta, a progettare una nuova ver sione di IP che garantisse un numero di indirizzi sufficiente a soddisfare tutte le richieste.

> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=171&selection=20,0,28,36&color=important|La nuova versione è stata definita dalle RFC 1883 e 1887 con il nome di IPv6, la cui caratteristica fondamentale è quella di quadruplicare lo spazio degli indirizzi portandolo da 4 a 16 byte (128 bit).]]
> > La nuova versione è stata definita dalle RFC 1883 e 1887 con il nome di IPv6, la cui caratteristica fondamentale è quella di quadruplicare lo spazio degli indirizzi portandolo da 4 a 16 byte (128 bit).

Questo consente di avere 2^128 indirizzi possibili: circa 340 miliardi di miliardi di miliardi di miliardi di indirizzi contro i circa 4 miliardi di indirizzi consentiti da IPv4.
È quindi possibile collegare in rete non solo qualsiasi host ne faccia richiesta, ma anche ogni tipo di dispositivo intelligente(IoT).

Gli altri principali cambiamenti introdotti di IPv6 sono: 
- ==**Semplificazione dell’header IP**== con una **riduzione dei campi e una conseguente più rapida elaborazione delle informazioni in esso contenute**;
- ==**Flessibilità dell’header IP**== **per quanto riguarda i campi opzionali per garantire l’inserimento in futuro di nuove opzioni senza che si debba riprogettare l’intero formato dell’header**;
- **==Miglior controllo del flusso== inserendo nell’header la possibilità di richiedere una migliore qualità del servizio o un minimo di larghezza di banda garantita a disposizione o una trasmissione in tempo reale**;
- **==Maggiore sicurezza== attraverso estensioni dell’header** per **supportare l’autenticazione del mittente e quella del destinatario o richiedere la crittografia dei dati da trasmettere**;
- **==Maggiore efficienza==** e==liminando dall’header il campo checksum il cui ricalcolo== (dovuto alla modifica del campo TTL a ogni hop) ==costringeva ogni volta i router a elaborare i pacchetti più lentamente==

> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=171&selection=95,0,97,59&color=important|Pur non essendo retro compatibili (backward compatible) i due protocolli IPv4 e IPv6 possono coesistere grazie alla creazione di un tunnel.]]
> > Pur non essendo retro compatibili (backward compatible) i due protocolli IPv4 e IPv6 possono coesistere grazie alla creazione di un tunnel.

 La [[Sistemi e reti(Internetworking).pdf#page=172&selection=20,0,21,0&color=yellow|figura 1]] mostra la tecnica di **[[Sistemi e reti(Internetworking).pdf#page=171&selection=74,0,74,9&color=yellow|Tunneling]]** descritta in RFC 2473 e in RFC 4213. ==**Un tunnel serve a trasmettere i pacchetti IPv6 inserendoli nel campo dati all’interno di un pacchetto IPv4**==. L’indirizzo di destinazione del pacchetto IPv4 è l’indirizzo di un sistema su cui sono attivi entrambi i protocolli. **Il destinatario del pacchetto IPv4 estrae il pacchetto IPv6 e lo inoltra verso la destinazione IPv6 finale** (che può essere lui stesso). Inoltre:
- **Il traffico IPv4 in una rete non subisce alcun inconveniente all’attivazione di IPv6**;
- **Tutti gli attuali Sistemi Operativi consentono l'utilizzo contemporaneo dei due protocolli**;
- **Molte applicazioni**, **quando si trovano su un computer dotato di indirizzo IPv6**, **scelgono il trasporto IPv6 quando anche il destinatario possiede un indirizzo IPv6**: *può dunque capitare di essere collegati alla rete Internet IPv6 senza saperlo*.

---
**[[Sistemi e reti(Internetworking).pdf#page=172&selection=38,0,38,13&color=yellow|L'HEADER IPv6]]**:

**Il formato dell’header IPv6** (opzioni escluse) **è costituito da 40 byte**: 
- **[[Sistemi e reti(Internetworking).pdf#page=172&selection=75,3,75,11&color=yellow|VERSION]]**: **4 bit**, **contiene il numero della versione IP**, è impostato su 6 (0110);

- **[[Sistemi e reti(Internetworking).pdf#page=172&selection=77,3,78,0&color=yellow|TRAFFIC CLASS]]** (o Priority): **8 bit**, **indica la priorità del pacchetto IPv6** (è **simile al campo Type of Service di IPv4**). **Permette ai router di gestire il traffico in base alla priorità del pacchetto**. *Se si verifica una congestione sul router, i pacchetti con la priorità minore verranno scartati*. **Le priorità maggiori sono quelle da 8 a 15 e sono utilizzate per il traffico real time che non deve subire rallentamenti**. **Le priorità da 0 a 7 indicano invece i tipi di traffico che in caso di congestione possono anche subire rallentamenti**;

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=29,3,29,12&color=yellow|FLOW LABEL]]**: ==**20 bit**, viene **utilizzato dalla sorgente per etichettare i pacchetti appartenenti allo stesso flusso al fine di richiedere una gestione speciale da parte dei router IPv6 intermedi**, **come il servizio in tempo reale**==. **Se un host o un router non supportano il servizio richiesto**, **il campo viene impostato a 0**, mentre **viene ignorato se è il destinatario a non supportare il servizio**;

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=39,3,39,16&color=yellow|PAYLOAD LENGTH]]**: **16 bit**, **indicano la lunghezza del pacchetto dati** in ottetti, **senza l’header**;

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=45,2,45,13&color=yellow|NEXT HEADER]]**: **8 bit**, **identificano il tipo di header che si trova immediatamente dopo l’header IPv6 di base** (vedi descrizione sugli extension header);

- [[Sistemi e reti(Internetworking).pdf#page=173&selection=50,2,50,11&color=yellow|HOP LIMIT]]: **8 bit**, **rappresentano il numero massimo di hop consentiti al pacchetto per giungere a destinazione senza esser scartato**. **Equivale al campo TTL** (Time To Live) di IPv4

- [[Sistemi e reti(Internetworking).pdf#page=173&selection=57,2,61,19&color=yellow|SOURCE ADDRESS e DESTINATION ADDRESS]]: **128 bit ciascuno**, **rappresentano l’indirizzo IPv6 del mittente e del destinatario**.

---
**[[Sistemi e reti(Internetworking).pdf#page=173&selection=69,1,74,7&color=yellow|EXTENSION HEADER DI IPv6]]**:

Una grossa innovazione di IPv6 è la gestione delle opzioni.
*Il campo Options di IPv4 è stato eliminato a causa delle complicazioni che introduce: con le opzioni il tempo di elaborazione dei pacchetti IPv4 aumenta, in quanto ogni router attraversato deve processarle tutte prima di inoltrare il pacchetto.*
**Per soddisfare l’esigenza di poter specificare comunque delle opzioni**, in modo più efficiente rispetto al passato, si è pensato al meccanismo degli **extension header**.

L’elenco aggiornato degli extension header è mantenuto da IANA: www.iana.org/assignments/ipv6-parameters

**Una implementazione completa di IPv6** **include i 6 header di seguito elencati** (gli altri presenti su IANA sono per contesti applicativi specifici, per esempio il Mobility header si usa per la gestione della mobilità di un host):

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=103,3,103,28&color=yellow|Hop-by-Hop OPTION HEADER]]**: L’header Hop-by-Hop Options **contiene informazioni che possono essere elaborate da ogni router della rete attraversata dal pacchetto**. **Le opzioni che possono interessare tutti i router** riguardano di solito **funzioni di gestione o di debugging**. **Questa opzione può anche indicare un cosiddetto pacchetto jumbo** cioè un **pacchetto superiore ai 65.536 byte** (216).

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=118,3,118,17&color=yellow|ROUTING HEADER]]**: Il Routing header è **usato da una sorgente per elencare uno o più router che un pacchetto deve attraversare prima di giungere a destinazione**.

- **[[Sistemi e reti(Internetworking).pdf#page=173&selection=123,3,123,18&color=yellow|FRAGMENT HEADER]]**: Una **novità introdotta da IPv6 è l’eliminazione della frammentazione del pacchetto da parte dei router**. **Col nuovo protocollo la frammentazione è gestita dal mittente e non più dai router intermedi**. **Se le dimensioni del pacchetto superano la dimensione massima consentita su un canale sul quale tale pacchetto deve transitare**, **il router lo scarta e invia al mittente un messaggio ICMP di errore**. **A quel punto il mittente frammenta e rispedisce il pacchetto tenendo conto che i router IPv6 garantiscono almeno 1280 byte per pacchetto**.

- **[[Sistemi e reti(Internetworking).pdf#page=174&selection=6,3,6,24&color=yellow|AUTHENTICATION HEADER]]**: IPv6, **attraverso questo header**, **fornisce un servizio che assicura l’autenticità** (cioè garantisce l’identità del mittente) **e l’integrità del pacchetto** (cioè che non sia stato modificato nel tragitto mittente-destinatario).

- **[[Sistemi e reti(Internetworking).pdf#page=174&selection=12,3,12,40&color=yellow|Encapsulating Security PAYLOAD HEADER]]**: L'Encapsulating Security header, invece, **fornisce un meccanismo di crittografia** per trattare i dati in modo che possano essere letti solo al termine del percorso dal destinatario che possiede la chiave appropriata per decrittografare i dati.

- **[[Sistemi e reti(Internetworking).pdf#page=174&selection=19,3,19,29&color=yellow|DESTINATION OPTIONS HEADER]]**: ==permette di includere informazioni aggiuntive destinate al destinatario==, **è l’unico extension header che può comparire due volte nello stesso pacchetto**, **anche se in due posizioni diverse**. **Se è posto tra l’Hop-by-Hop e il Routing header potrà essere letto da ogni nodo intermedio**. **Altrimenti è visibile solo dal destinatario**. **Il Destination Option header può contenere anche un campo padding**, al fine di rendere i pacchetti di lunghezza pari a multipli di 64 byte. **Gli extension header sono inseriti subito dopo l’header IPv6**; in questo modo, **per i router che non li devono processare**, **essi fanno parte del payload del pacchetto e non sono analizzati**. **Per questo motivo si ha un miglioramento delle prestazioni di forwarding**. **Ogni pacchetto può contenere più di un extension header**. **In ognuno di essi c'è un campo Next Header in cui viene specificato il tipo del prossimo header**, **formando** quella che viene chiamata **catena di header**[[Sistemi e reti(Internetworking).pdf#page=174&selection=69,0,73,1&color=yellow|figura 3]].

**Nel formare tale catena occorre rispettare un ordine ben preciso**, **in cui l’ultimo Next Header (Upper Layer) indica il protocollo di livello superiore trasportato nel payload**.
Questo protocollo è indicato con un numero, che è lo stesso per IPv4 e IPv6 e si trova nel registro di IANA (www.iana.org/assignments/protocol-numbers).

NelPRFC 8200 è anche indicato **l’ordine in cui devono comparire nel pacchetto IPv6 gli extension header**, nel caso ne siano presenti più di uno:
1. IPv6 header;
2. Hop-by-Hop Options header;
3. Destination Options header (con opzione di instradamento);
4. Routing header;
5. Fragment header;
6. 6.Authentication header;
7. Encapsulating Security Payload header;
8. Destination Options header;
9. Upper Layer header.

**L’ordinamento corretto e la non ripetizione degli extension header è fondamentale**: si sono registrati casi di nodi di rete andati in crash nell elaborare pacchetti IPv6 formattati in modo errato. ==In origine gli extension header==, tranne l’Hop-by-Hop, ==erano stati definiti per essere trasparenti ai router intermedi ed essere processati solo dall’host di destinazione==. ==Nelle reti attuali esistono apparati intermedi==, come i firewall, ==che esaminano anche questi header==, ==rallentando così il trasferimento del pacchetto==, ==o addirittura lo scartano== se non riconoscono un extension header. La specifica di IPv6 raccomanda di non definire nuovi extension header, a meno che proprio nessuno di quelli già presenti possa essere usato per specificare la nuova opzione. Eventuali nuove informazioni che devono essere esaminate solo dal destinatario, devono essere trasportate usando il Destination Options header, in quanto fornisce una gestione ottimale e garantisce la compatibilità con le release precedenti ([[Sistemi e reti(Internetworking).pdf#page=175&selection=4,0,4,32&color=yellow|Backward compatibility]]).

---
[[B, Indirizzi IPv6]]