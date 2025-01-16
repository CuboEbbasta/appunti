==I**l protocollo IP fornisce l’indirizzo logico degli host di una rete TCP/IP**==**A ciascun host viene assegnato un indirizzo IP univoco rispetto alla rete su cui sta lavorando**. Quindi **l’indirizzo IP assegnato a un host** **non solo rappresenta l’host**, **ma** indica, unitamente alla subnet mask, **anche su quale sottorete logica si trovi**, **consentendo l’inoltro dei pacchetti da parte dei router solo quando è necessario** *(i concetti di sottorete e subnet mask saranno spiegati nella lezione successiva)*. **==In realtà un indirizzo IP non identifica un host, ma una sua interfaccia di rete==**. **Nel caso in cui un nodo abbia più interfacce verso la rete**, **ogni interfaccia avrà un indirizzo diverso**. Per esempio, **un computer può avere due interfacce di rete**: una wired (802.3) e una wireless (802.11), **ciascuna con un suo indirizzo IP**. La [[Sistemi e reti(Internetworking).pdf#page=122&selection=46,0,55,0&color=yellow|figura 3]] mostra un router che collega 3 reti e che quindi ha almeno 3 distinti indirizzi IP, uno per ogni interfaccia di rete.

> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=122&selection=60,0,69,59&color=important|Gli indirizzi IPv4 sono numeri di 32 bit suddivisi in 4 byte (anche detti ottetti). Vengono solitamente espressi nella notazione decimale puntata costituita da 4 numeri decimali compresi tra 0 e 255, separati da un punto.]]
> > Gli indirizzi IPv4 sono numeri di 32 bit suddivisi in 4 byte (anche detti ottetti). Vengono solitamente espressi nella notazione decimale puntata costituita da 4 numeri decimali compresi tra 0 e 255, separati da un punto.

Per esempio: 
**1 9 2 .1 6 8 .1 .2 5 4** 

Più raramente si trovano espressi nella notazione binaria:
**11000000.10101000.00000001.11111110**

---
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=122&selection=83,0,84,39&color=yellow|L’indirizzo IPv4 usa 32 bit, quindi il numero massimo, teorico, di indirizzi a disposi zione è 2 32 = 4 .2 9 4 .9 6 7 .2 9 6 ,]]
> > L’indirizzo IPv4 usa 32 bit, quindi il numero massimo, teorico, di indirizzi a disposi zione è 2 32 = 4 .2 9 4 .9 6 7 .2 9 6 ,

*Il numero è teorico, in quanto non tutti gli indirizzi possono essere usati e assegnati a un’interfaccia di rete, come si vedrà in seguito. Quando fu implementato* **l'IP si trattava di un numero elevato di indirizzi**, *ma, in realtà,* **era destinato a esaurirsi con la crescente diffusione che ebbe la rete Internet alla fine degli anni Ottanta e negli anni Novanta**. **All’inizio furono implementate delle tecniche per ottimizzare l’uso degli indirizzi IP**: **subnetting**, **CIDR**, **VLSM** (che vedremo nelle lezioni successive). **Nel tempo si studiò un nuovo protocollo di rete**, **IPv6**, **destinato a sostituire la precedente versione 4**, **che risolse il problema della carenza di indirizzi e introdusse nuove funzionalità**, *per rispondere alle mutate esigenze dovute all’enorme diffusione di Internet*. **Attualmente IPv4 e IPv6 continuano a coesistere e le schede di rete degli host usano entrambi gli indirizzi**. *Nell’Unità 4 approfondiremo il protocollo IPv6.*

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=122&selection=98,0,100,28&color=yellow|Gli indirizzi IP pubblici sono assegnati da IC A N N (Internet Corporation for Assigned Names and Numbers), che ha assunto la funzione di IAN A (Internet Assigned Numbers Authority).]]
> > Gli indirizzi IP pubblici sono assegnati da IC A N N (Internet Corporation for Assigned Names and Numbers), che ha assunto la funzione di IAN A (Internet Assigned Numbers Authority).

---

**LE CLASSI**:
---

**[[Sistemi e reti(Internetworking).pdf#page=123&selection=48,0,50,19|L’indirizzo IP di un host è diviso in due parti]]**:

- [[Sistemi e reti(Internetworking).pdf#page=123&selection=52,2,53,0&color=yellow|NetlD]] (o NetworkID): **è l’indirizzo della rete in cui si trova l’host**;
- [[Sistemi e reti(Internetworking).pdf#page=123&selection=57,2,57,8&color=yellow|HostlD]] : **è l’indirizzo dell’host all’interno della rete NetlD**.

*Se si assegna un numero di bit elevato al NetlD, avremo molte piccole reti, ciascuna con pochi host. Al contrario, se si usano pochi bit per il NetlD, si avranno poche grandi reti, ciascuna con un elevato numero di host.*

> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=123&selection=65,0,79,5&color=important|In base al valore dei bit più significativi, gli indirizzi IP sono suddivisi in 5 classi: A, B, C, D, E, ma solo le prime 3: A, B e C, possono essere utilizzate per assegnare indirizzi agli host ( figura 5 ) .]]
> > In base al valore dei bit più significativi, gli indirizzi IP sono suddivisi in 5 classi: A, B, C, D, E, ma solo le prime 3: A, B e C, possono essere utilizzate per assegnare indirizzi agli host.


---
- **[[Sistemi e reti(Internetworking).pdf#page=124&selection=6,0,6,8&color=yellow|Classe A]]**:
	-==**Ha il primo bit del primo ottetto fisso al valore 0**==;
	-Dedica il primo ottetto alla rete (N) e gli altri 3 agli host (H), è quindi nella forma NHHH;
	-Ha un range di indirizzi da 0.0.0.0 a 127.255.255.255;
	-Ha 7 bit dedicati alla rete ma può indirizzare solo 27 - 2 = 126 reti perché i valori 0 (this Network) e 127 (loopback net) non possono essere assegnati in quanto in dirizzi riservati;
	-Ha 24 bit dedicati agli host e può indirizzare 224 - 2 = 16.774.214 host per ogni rete perché i valori 0.0.0 (this host) e 255.255.255 (broadcast) non possono essere asse gnati in quanto indirizzi riservati;
	-Gli indirizzi in classe A sono adatti a network di grandi dimensioni.

- **[[Sistemi e reti(Internetworking).pdf#page=124&selection=29,0,31,1&color=yellow|Classe B]]**:
	-==**Ha i primi 2 bit del primo ottetto fissi al valore 10**==; 
	-Dedica i primi 2 ottetti alla rete e gli altri 2 agli host (NNHH); • ha un range di indirizzi da 128.0.0.0 a 191.255.255.255; 
	-Ha 14 bit dedicati alla rete e può indirizzare 214 = 16.384 reti; 
	-Ha 16 bit dedicati agli host e può indirizzare 216 - 2 = 65.534 host per ogni rete perché i valori 0.0 (this host) e 255.255 (broadcast) non possono essere assegnati in quanto indirizzi riservati; 
	-Gli indirizzi in classe B sono adatti a network di medie dimensioni.

- **[[Sistemi e reti(Internetworking).pdf#page=124&selection=51,0,51,8&color=yellow|Classe C]]**:
	-**==Ha i primi 3 bit del primo ottetto fissi al valore 110==**; 
	-Dedica i primi 3 ottetti alla rete e l’ultimo agli host (NNNH); • ha un range di indirizzi da 192.0.0.0 a 223.255.255.255; 
	-Ha 21 bit dedicati alla rete e può indirizzare 221 = 2.097.152 reti;
	-Ha 8 bit dedicati agli host e può indirizzare 28 - 2 = 254 host per ogni rete perché 1 valori 0 (this host) e 255 (broadcast) non possono essere assegnati in quanto in dirizzi riservati; 
	-Gli indirizzi in classe C sono adatti a network di piccole dimensioni.

- **[[Sistemi e reti(Internetworking).pdf#page=124&selection=75,0,77,1&color=yellow|Classe D]]**:
	-==**Ha i primi 4 bit del primo ottetto fissi al valore 1110**==; 
	-Ha un range da 224.0.0.0 a 239.255.255.255; 
	-Non sono indirizzi assegnabili ai singoli host; 
	-Servono per il multicasting cioè a indirizzare gruppi di host.

- **[[Sistemi e reti(Internetworking).pdf#page=124&selection=87,0,87,8&color=yellow|Classe E]]**:
	-**==Ha i primi 4 bit del primo ottetto fissi al valore 1111==**; 
	-Ha un range da 240.0.0.0 a 255.255.255.255, ma l’indirizzo con tutti 1 è escluso in quanto indirizzo riservato; 
	-Non sono indirizzi assegnabili ai singoli host; 
	-Sono indirizzi riservati per usi futuri o per scopi sperimentali.

---
- [[Sistemi e reti(Internetworking).pdf#page=125&selection=77,0,77,30&color=note|INDIRIZZI RISERVATI O SPECIALI]]

- [[Sistemi e reti(Internetworking).pdf#page=126&selection=14,4,14,49&color=note|INDIRIZZI PUBBLICI/PRIVATI E STATICI/DINAMICI]]

---

[[Subnetting]]