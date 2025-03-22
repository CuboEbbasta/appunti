In questa Lezione analizzeremo i protocolli di routing di tipo **IGP** (Interior Gateway Protocol) noti come **protocolli intradominio** poiché vengono usati per regolare l’instradamento dei pacchetti tra gli host interni a un Autonomous System. Questi protocolli possono essere classificati in base all’algoritmo di routing, Distance Vector o Link State, che utilizzano. I principali IGP sono:
1. con Distance Vector:
- **RIP**, Routing Information Protocol, definito in ambito IETF, usa la metrica hop count;
- **IGRP**, Interior Gateway Routing Protocol, proprietario Cisco, è stato creato per superare le limitazioni di RIP, supportando anche più metriche (bandwidth, delay, load, reliability);
- **EIGRP**, Enhanced IGRP, proprietario Cisco, ha sostituito IGRP introducendo una serie di miglioramenti, però continua a usare le stesse metriche.

2. con Link State:
- **OSPF**, Open Shortest Path First; ( *<- Link State <- Dijkstra*)
- **Integrated IS-IS**, Integrated Intermediate System-Intermediate System, è uno standard che è stato definito prima in ISO e poi in IETF.

Analizziamone uno per tipologia, scegliendo quelli definiti come standard in ambito IETF e, come tali, usati in tutte le reti: RIP e OSPF.

--- 
[[Sistemi e reti(Internetworking).pdf#page=226&selection=65,4,65,52&color=yellow|II protocollo RIP (Routing Information Protocol)]] *-> Distance Vector*.

È uno dei protocolli più vecchi essendo stato sviluppato dalla Xerox e poi adattato alla suite TCP/IP nel 1982. ==La sua metrica è il numero di hop== (**==hop count==**), la più semplice di tutte, ma anche la meno efficiente. RIP è un protocollo Distance Vector che opera in modo molto simile all'algoritmo descritto nella Lezione 2, dove per semplicità il costo di un percorso è stato definito tra coppie di router. ==In RIP i costi sono in realtà calcolati dal router sorgente alla subnet di destinazione==. 

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=226&selection=78,0,80,29&color=yellow|Nella specifica di RIP, la distanza è definita come il numero di subnet attraversa te lungo il percorso più breve da un router sorgente a una subnet di destinazione, includendo anche quest'ultima]]
> > Nella specifica di RIP, la distanza è definita come il numero di subnet attraversa te lungo il percorso più breve da un router sorgente a una subnet di destinazione, includendo anche quest'ultima.
> 

==Solo il percorso più breve verso la destinazione viene memorizzato nella routing table. Il numero massimo di hop consentiti prima che il pacchetto venga scartato è pari a 15==. Di conseguenza, il RIP non può essere impiegato in un contesto in cui esistano subnet separate da più di 15 router. Per questo motivo il RIP è solitamente utilizzato in LAN non troppo grandi. ==Il RIP prevede che le tabelle di routing vengano aggiornate ogni 30 secondi, quindi ogni router invia la propria tabella completa a tutti i vicini direttamente collegati, generando grandi quantità di traffico su reti a bassa capacità trasmissiva==. Un’intera rete garantisce l’aggiornamento dei percorsi verso tutti i suoi router (==convergenza==) ==in circa 3 minuti==. *-> Tabella di Routing  Dopo... ; -> Tempo Medio.*

Opzionalmente il RIP applica l’==**hold down**, cioè non accetta alcun update per 60 secondi relativamente a route guaste==.

Per esempio, come mostrato nella [[Sistemi e reti(Internetworking).pdf#page=227&selection=16,0,20,0|figura 4]] , se il router "A" manda un update al router "C" comunicando che il router "D" non è più raggiungibile, dovranno passare 60 secon di prima che il router "C" accetti dal router "B" (o da qualunque altro router) update ri guardanti il router "D". Questo per evitare che "B", non ancora informato del guasto su "D", faccia credere a "C" che "D" sia tornato raggiungibile. I 60 secondi servono proprio a garantire la convergenza evitando che si propaghino informazioni inconsistenti.

Il modo con cui il RIP evita il loop tra 2 nodi adia centi è lo **==split horizon==**, tipicamente utilizzato dai protocolli basati sul Distance Vector.

In un pacchetto RIP ==non è presente alcun campo dati==, in quanto il protocollo RIP non è stato pro gettato per lo scambio di informazioni tra host. In pratica le informazioni contenute in tali pac chetti riguardano solo il routing. Vediamo in dettaglio il formato di un pacchetto RIPv1 ([[Sistemi e reti(Internetworking).pdf#page=227&selection=47,1,47,9&color=yellow|FIGURA 5]]):

Ogni pacchetto RIP contiene:
- Un campo **==Command==**: ==indica il tipo di messaggio: 1 = Request, 2 = Response== *(solo RIPv2)* ; un pacchetto Response può essere inviato come risposta a una ==richiesta o a seguito di un aggiornamento della tabella di routing== (==update==);

- Un campo **Version**: contiene il numero della versione di RIP: 1 = RIPvl e 2 = RIPv2;

- Fino a 25 **route entry**: corrispondono alle entry della routing table del mittente. Nel caso in cui ==il router avesse una routing table con più di 25 entry==, invierà più pacchetti. Ogni route entry occupa 20 ottetti che trasportano i seguenti dati:
	- **==Address Family Identifier==**: individua il tipo di indirizzo contenuto nel campo Address, ==nel caso di IP il valore è 2==;
	
	- **==Address==**: è l'indirizzo del destinatario della route (network, subnetwork o host);
	
	- ==**Metric**==: è espressa in hop count, l'unica metrica usata da RIPvl.

==Il pacchetto RIP è imbustato in UDP== (User Datagram Protocol a livello Transport) usando il numero di porta 520.

Ci sono 3 versioni del protocollo: RIPvl, RIPv2 e RIPng. La versione **==RIPv1==** (RFC 1058) effettua un routing classfull, infatti ==non trasporta la subnet mask==: ==tutte le sottoreti di una rete hanno la stessa subnet mask==. Questo problema viene risolto nella versione RIPv2 (RFC 2453): nel pacchetto ==è presente il campo Subnet Mask== che contiene appunto la subnet mask corrispondente alla sottorete considerata (f ig u r a ò). Un’ulteriore novità introdotta da ==RIPv2 riguarda i messaggi di update==: con RIPv1 tali messaggi vengono inviati in broadcast e quindi favoriscono il sovraccarico nella rete e un tempo di convergenza lento, mentre con ==RIPv2 i messaggi vengono inviati in multicast==, ==interessando così solo certi router==. Inoltre, in RIPv2 si implementano ==meccanismi per l'autenticazione==. **RIPng** (RIP next generation, RFC 2080) è un’estensione del protocollo originale ==RIPv1 per supportare IPv6==.

---
[[Sistemi e reti(Internetworking).pdf#page=229&selection=110,0,110,45&color=yellow|II protocollo OSPF (Open Shortest Path First)]]

==OSPF è un protocollo di routing== (RFC 2328 e successivi aggiornamenti) ==basato sulla creazione di un database distribuito== che rappresenti la topologia della rete sotto for ma di grafo. Utilizza quindi l’algoritmo Link State. ==I protocolli SPF-based hanno la caratteristica dell’uniformità del database relativo all’Autonomous System== (==AS==), ==cioè tutti i router dell’AS hanno le stesse informazioni relative allo stato delle connessioni==. Questa caratteristica, ovviamente, la si riscontra anche in OSPF che quindi è in grado di rispondere prontamente alle variazioni topologiche dell’AS con un rapido aggior namento delle routing information, ==mediante un traffico di protocollo assai ridotto== *<- Rispetto a RIP*.

Come per RIP, anche di OSPF è stata definita una nuova versione, **==OSPFv3==**, per il supporto di IPv6: **==OSPF for IPv6==** RFC 5340.

Il protocollo OSPF si fonda s==ul concetto di **area**==: ==un’area è costituita da una o più re ti contigue==. ==Ogni area ha il proprio database topologico ed esegue la propria copia dell’algoritmo di routing==. La caratteristica di ogni area è che la propria struttura interna è nascosta alle altre aree, così come i router interni all’area non conoscono in dettaglio la topologia del le aree esterne. La conseguenza immediata, che è anche il vantaggio di tale organizzazione distribuita, è la sensibile riduzione del traffico di routing, rispetto a un’organizzazione centraliz zata. Altra conseguenza immediata è che i router non hanno tutti lo stesso database topologico, ma ognuno possiede quello relativo alla propria area; i router collegati a più aree avranno un database per ogni area.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=228&selection=89,0,99,35&color=yellow|Con questo tipo di organizzazione si hanno due tipi di routing, anzi due livelli: routing intra-area, quando la sorgente e la destinazione dei pacchetti si trovano nella stessa area; routing inter-area, quando la destinazione si trova in un’area differente da quella della sorgente]]
> > Con questo tipo di organizzazione si hanno due tipi di routing, anzi due livelli: routing intra-area, quando la sorgente e la destinazione dei pacchetti si trovano nella stessa area; routing inter-area, quando la destinazione si trova in un’area differente da quella della sorgente.
> 
> 

Tra le aree ce n’è una particolare, detta **==backbone==** (*Termine usato ogniqualvolta si fa riferimento a una rete principale, core che collega altre reti. Il traffico dati di queste reti passa attraverso uno o più nodi del blackbone*) o **==area zero==** ([[Sistemi e reti(Internetworking).pdf#page=230&selection=1,1,8,6&color=yellow|FIGURA 7]]). ==Tale area è formata da tutte quelle reti che non appartengono a nessuna area, più i router di confine di ogni area==. È quindi possibile passare da un'area a una qualunque altra area dello stesso AS passando dalla backbone area. Nel caso un’area non sia fisi camente connessa alla backbone area si configura un collegamento virtuale (**virtual link**) attraverso un’area di transito ([[Sistemi e reti(Internetworking).pdf#page=230&selection=1,1,8,6&color=yellow|FIGURA 7]]). Dal punto di vista del grafo, si ha che il costo del link si ottiene come somma delle distanze intra-area tra i due router; si parla di distanza intra-area perché si utilizza solo il routing intra-area per i link virtuali. Dal punto di vista topologico la backbone area ha le stesse caratteristiche e proprietà di tutte le altre.

 I router si classificano come segue:
 
 - **router interni** (==**IR**==, ==Internai Router==): router che sono connessi direttamente al le reti appartenenti alla stessa area; fanno parte di questa categoria anche quei router che sono nell’area backbone;
 
 - **router di confine dell’area** (==**ABR**==, ==Area Border Router==): router collegati a più aree, una deve essere la backbone area. Essi eseguono una copia deHalgoritmo per ogni area collegata, più una copia per la backbone area, dal momento che i router di confine sono anche router di backbone (BR);
 
 - **router backbone** (==**BR**==, ==Backbone Router==): router che hanno un’interfaccia sul la backbone area. Da sottolineare che i router che hanno solo interfacce sulla backbone sono da considerare router interni;
 
 - **router di confine dell’AS** (**ASBR**, Autonomous System Boundary Router): router che scambiano informazioni con altri AS. Tutti i router dell’AS conoscono i cam mini che portano a questi router, che sono gli unici a poter instradare l’informa zione verso l’esterno.

---
[[Sistemi e reti(Internetworking).pdf#page=231&selection=77,0,81,14&color=yellow|LINK STATE ADVERTISEMENT]]

OSPF utilizza la tecnica **LSA** (Link State Advertisement) per condividere le informa zioni di instradamento tra i nodi. Questa tecnica consiste nel rendere pubbliche le informazioni sullo ==stato dei collegamenti inviando dei pacchetti==, ==detti appunto **LSA packet**==, ==ai router==. Sono stati definiti vari tipi di pacchetti LSA generati dai diversi router: interni, designated, ABR e ASBR, per inviare in ==flooding== i messaggi nella stessa area interna o nelle aree esterne.

L’header OSPF ([[Sistemi e reti(Internetworking).pdf#page=232&selection=110,0,110,8&color=yellow|FIGURA 8]]) è costituito da 24 byte suddivisi in 8 campi. 

- **Version**: 1 byte, nelle reti IPv4 si usa la versione 2, nelle reti IPv6 si usa la versio ne 3 (OSPF for IPv6); 
- **Packet Type**: 1 byte, con valori:
	- 1 Hello 
	- 2 Database Description (DD) 
	- 3 Link State Request 
	- 4 Link State Update 
	- 5 Link State Acknowledgment

- **Packet Length**: 2 byte, dimensione del pacchetto in byte, header incluso;
- **Router ID**: 4 byte, identificatore del router che ha generato il messaggio;
- **==Area ID==**: ==4 byte==, ==identificatore dell’area OSPF a cui appartiene il messaggio==, ==ogni messaggio appartiene a una sola area==;
- **Checksum**: 2 byte, calcolo della checksum, in modo simile al protocollo IP, su tutto il messaggio tranne il campo Authentication; 
- **Authentication Type**: 2 byte, indica il tipo di autenticazione usato per il messaggio:
	- 0 nessuna autenticazione;
	- 1 autenticazione tramite semplice password; 
	- 2 autenticazione con crittografia;

-  **Authentication**: 8 byte, contiene dati utili per il tipo di autenticazione da applicare, definito nel campo Authentication Type:
	- password semplice, è presente una password di 64 bit in chiaro. Questa moda lità rende vulnerabile la rete e compromette la sicurezza del dominio di routing OSPF, infatti la password può essere letta da qualunque dispositivo connesso fi sicamente alla rete;
	- uso della crittografia, in tutti i router è configurata una chiave segreta, usata per generare o verificare la stringa di autenticazione (digest) del pacchetto, che viene inserita al fondo di ogni pacchetto OSPF. Il Message Body contiene i dati relativi al tipo di pacchetto. Per esempio, nel caso di pacchetti di Hello, contiene l'elenco dei Router ID dei router vicini. Vediamo nel dettaglio i Packet Type.

Il **Message Body** contiene i dati relativi al tipo di pacchetto. Per esempio, nel caso di pacchetti di Hello, contiene l'elenco dei Router ID dei router vicini. Vediamo nel dettaglio i ==**Packet Type**==.

1. **Pacchetto Hello**: Il protocollo di Hello è usato per creare e mantenere ==le relazioni di vicinato==. Viene anche usato per l’elezione del Designated Router. ==All’accensione== il router inizializza alcune strutture dati di supporto e aspetta indicazioni dai protocolli di basso livello sulla corretta funzionalità delle sue interfacce. Appena si è assicurato che le sue interfacce funzionano usa un protocollo di ==Hello== per acquisire informazio ni sui nodi vicini: invia pacchetti di Hello e li riceve da questi. Successivamente i pacchetti di Hello sono usati come pacchetti keep-alive per verificare i vicini attivi.

---
[[SPF.pdf]]
[[U5-L2-Distance_Vector_Algorithm.pdf]]
[[U5-L2-Distance_Vector_Algorithm-count-to-infinity.pdf]]