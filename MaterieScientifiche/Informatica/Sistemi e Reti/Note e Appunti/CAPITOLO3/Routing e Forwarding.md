
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=117&selection=61,3,63,43&color=yellow|Sistemi e reti(Internetworking), p.117]]
> > Forwarding: è l’attività di inoltro dei dati nella rete

**Forwarding:**

* Si occupa di inoltrare i pacchetti di dati da un dispositivo all'altro lungo il percorso stabilito dal routing.
* È come consegnare una lettera: una volta che la strada è stata determinata, il forwarding si occupa di assicurarsi che la lettera arrivi al destinatario corretto.
* I dispositivi che eseguono il forwarding sono generalmente **switch** e **router**.

**Esempio:** Dopo che il routing ha stabilito il percorso per l'email del tuo amico, lo switch nel tuo ufficio inoltrerà il pacchetto di dati al router locale, che a sua volta lo invierà al router della città dell'amico.

---
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=117&selection=77,3,79,39&color=yellow|Sistemi e reti(Internetworking), p.117]]
> > Routing: il livello Network determina il percorso
> 
> 

**Routing:**

* Si occupa di determinare il percorso ottimale per i pacchetti di dati attraverso una rete complessa. 
* È come la navigazione su una mappa: il router analizza le informazioni sulla destinazione e sceglie la strada più efficiente, tenendo conto del traffico, della distanza e delle risorse disponibili.
* I router utilizzano **tabelle di routing** per memorizzare le informazioni sui percorsi verso diverse destinazioni. Queste tabelle vengono aggiornate in tempo reale in base al flusso di dati e alle condizioni di rete.

**Esempio:** Immagina di inviare un'email a un amico che vive in una città diversa. Il tuo computer utilizza il routing per determinare il percorso migliore per il pacchetto di dati, passando attraverso diversi router fino ad arrivare al server del tuo amico.


In sintesi, il **routing** pianifica il percorso migliore per i dati, mentre il **forwarding** li inoltra lungo quel percorso. Entrambi sono essenziali per garantire una comunicazione fluida e efficiente nella rete.

---
**NETWORK LAYER**
---
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=117&selection=107,0,113,13&color=yellow|Sistemi e reti(Internetworking), p.117]]
> > Per meglio affrontare la realizzazione di questi due importanti compiti, nelle moderne reti SDN (Software-Defined Network) il Network Layer è strutturato in due sottolivelli:

**Immagina una rete come una città con strade e auto.** 

**Il [[Sistemi e reti(Internetworking).pdf#page=117&selection=115,2,115,12&color=yellow|Data Plane]] (Piano dei Dati)** è come il sistema stradale stesso, dove le auto (i pacchetti di dati) viaggiano da un punto all'altro. Ogni "intersezione" della città rappresenta un router, che gestisce il flusso delle auto in base alle regole predefinite:

* **Forwarding:** Il router decide quale strada prendere per far proseguire l'auto verso la sua destinazione finale. Gestito dal Data Plane. 
* **Esempio:** Un router riceve un pacchetto con destinazione "Piazza Duomo". Consultando le sue tabelle di routing, il router determina che la strada migliore per raggiungere Piazza Duomo è via "Via Roma" e inoltra il pacchetto in quella direzione.

**Il [[Sistemi e reti(Internetworking).pdf#page=117&selection=124,2,124,15&color=yellow|Control Plane]] (Piano del Controllo)** è come il traffico cittadino, responsabile della pianificazione e gestione del flusso delle auto. 

* **Routing:** Il Control Plane definisce le migliori strade da seguire per ogni destinazione, tenendo conto del traffico, degli incidenti e delle condizioni meteo.
* **Algoritmi e Protocolli:**  Il Control Plane utilizza algoritmi di routing (come OSPF o BGP) e protocolli di comunicazione (come TCP/IP) per coordinare le azioni dei router e garantire un flusso efficiente dei dati.

**In sintesi:**

* Il ==**Data Plane**== **gestisce il ==flusso fisico== dei dati tra i dispositivi**, mentre il ==**Control Plane== definisce ==le regole e le rotte== da seguire**.
* Il Data Plane è come la rete stradale, mentre il Control Plane è come il traffico cittadino.

---
Il **==Network Layer==** può ==offrire== sia ==servizi== connessi (==connection-oriented==) sia servizi non connessi (==connectionless==). **I primi sono solitamente implementati tramite circuiti virtuali** e si ritrovano nelle reti di estrazione telefonica, quali X.25, Frame Relay e ATM . **I secondi sono offerti dalle reti TCP/IP, come Internet, che sono attualmente le reti più diffuse**. **II Network Layer è il primo strato dello stack TCP/IP in grado di garantire una con nettività a livello WAN**; **deve** quindi **poter identificare univocamente ogni host della rete mediante un identificativo apposito**. ***Un protocollo di livello Network deve conoscere la topologia della rete, scegliere di volta in volta il cammino migliore, gestendo le problematiche derivanti dalla presenza di più reti realizzate con tecnologie diverse a livello Physical***.

---
> [!PDF|] [[Sistemi e reti(Internetworking).pdf#page=118&selection=6,0,18,34|Il principale protocollo del livello Network nelle reti TCP/IP è Internet Protocol (IP), usato per trasferire i dati nella rete WAN. Sempre in questo livello sono stati specificati anche alcuni #protocolli di controllo come ARP, RARP, ICMP, i pro tocolli di routing e altri ancora.]]
> > Il principale protocollo del livello Network nelle reti TCP/IP è Internet Protocol (IP), usato per trasferire i dati nella rete WAN. Sempre in questo livello sono stati specificati anche alcuni **protocolli di controllo** come ARP, RARP, ICMP, i protocolli di routing e altri ancora.

---
[[Protocollo IP]]