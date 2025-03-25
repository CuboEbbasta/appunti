> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=178&selection=16,0,24,86&color=yellow|Sistemi e reti(Internetworking), p.178]]
> > L’**ICMP** (**Internet Control Message Protocol**), RFC 792, **fornisce un meccanismo di monitoraggio della rete**, utilizzato **prevalentemente dai router o dagli host destinatari per segnalare agli host mittenti eventuali insuccessi nell'instradamento dei pacchetti**.

---
[[Sistemi e reti(Internetworking).pdf#page=178&selection=92,0,98,2&color=yellow|Il pacchetto ICMP viene incapsulato nel pacchetto IP ed è caratterizzato da 4 campi, come mostrato nella figura 5]].

Vediamo in dettaglio i vari campi:

- **[[Sistemi e reti(Internetworking).pdf#page=179&selection=8,3,8,8&color=yellow|Type]]**: ==è il più significativo==, ==8 bit che **indicano il tipo di pacchetto ICMP trasmesso==**:

## ICMP Message Types(forse fatto bene, controllare libro)

| Type                                        | Description                                                                                                                             | Example Use Case                                                                            |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **0 Echo Reply**                            | A response to an Echo Request (ping). Used for basic network connectivity checks.                                                       | You ping a website, and the server responds with an Echo Reply.                             |
| **10 Router Solicitation**                  | A message sent by a device requesting information about available routers on the network.                                               | A new device joining a network sends a Router Solicitation to find a gateway.               |
| **20-29 Reserved (for robustness testing)** | These types are reserved for specific testing purposes and shouldn't be used in regular communication.                                  | Network engineers might use these types for stress testing or analyzing network behavior.   |
| **1 Not Assigned**                          | This type is not assigned to any specific ICMP message.                                                                                 | N/A                                                                                         |
| ==**11 Time Exceeded**==                    | **Inviato quando un pacchetto ha superato il tempo massimo consentito** per viaggiare attraverso la rete.                               | A router might send this if a packet takes too long to reach its destination.               |
| **30 Traceroute (D)**                       | Used for tracing the path a packet takes across the internet.                                                                           | Network administrators use Traceroute to identify bottlenecks or issues in network routing. |
| **2 Not Assigned**                          | This type is not assigned to any specific ICMP message.                                                                                 | N/A                                                                                         |
| **12 Parameter Problem**                    | Indicates an error with the parameters of an incoming ICMP packet.                                                                      | A router might send this if it encounters a malformed or invalid ICMP message.              |
| **31 Datagram Conversion (D)**              | Used for converting datagrams between different protocols.                                                                              | This type is primarily used in legacy network environments.                                 |
| ==**3 Destination Unreachable**==           | **Inviato quando un pacchetto non riesce a raggiungere la destinazione per vari motivi**, come un host inesistente o un errore di rete. | A router might send this if it can't find the requested IP address.                         |
| **4 Source Quench (D)**                     | Used to inform the sender that their traffic is overwhelming the network and they should reduce transmission rate.                      | This type helps prevent network congestion.                                                 |
| **13 Timestamp Request**                    | A request for the current timestamp from a remote host.                                                                                 | Used for measuring network latency or synchronizing clocks across devices.                  |
| **14 Timestamp Reply**                      | A response to a Timestamp Request, providing the requested timestamp.                                                                   | Used in conjunction with Timestamp Requests to measure network delay.                       |
| **32 Redirect on Host Mobile (D)**          | Used to redirect mobile hosts to a different IP address.                                                                                | This type is relevant for mobile network routing and handover procedures.                   |
| **5 Routing Redirect**                      | Informs a router about a new route to a specific destination.                                                                           | Used for dynamic routing updates in networks.                                               |
| **6 Alternate Host Address (D)**            | Provides an alternative IP address for a host.                                                                                          | This type can be used for load balancing or failover scenarios.                             |
| **15 Information Request (D)**              | A request for specific information from a remote host, such as its capabilities or configuration.                                       | Used for network discovery and service identification.                                      |
| **16 Information Reply (D)**                | A response to an Information Request, providing the requested information.                                                              | Used in conjunction with Information Requests to gather network details.                    |
| **33 IPvó Where-Are-You (D)**               | Used by mobile hosts to locate their home agent on a network.                                                                           | Relevant for mobile IP routing and location management.                                     |
| **34 IPvó l-Am -Here (D)**                  | A response to an IPvó Where-Are-You request, indicating the location of the home agent.                                                 | Used in conjunction with IPvó Where-Are-You requests for mobile host registration.          |
| **35 Mobile Registration Request (D)**      | Sent by a mobile host to register its presence on a network.                                                                            | Used for mobile IP authentication and routing setup.                                        |
| **36 Mobile Registration Reply (D)**        | A response to a Mobile Registration Request, confirming the registration of the mobile host.                                            | Used in conjunction with Mobile Registration Requests for successful registration.          |
| **37 Domain Name Request (D)**              | A request for the domain name associated with a specific IP address.                                                                    | Used for resolving IP addresses to human-readable domain names.                             |
| **38 Domain Name Reply (D)**                | A response to a Domain Name Request, providing the corresponding domain name.                                                           | Used in conjunction with Domain Name Requests for DNS resolution.                           |

**Note:** "D" indicates that the type is deprecated and not commonly used in modern networks.


- **[[Sistemi e reti(Internetworking).pdf#page=179&selection=103,2,104,0&color=yellow|Code]]**: ==fornisce indicazioni aggiuntive non comprese nel campo Type== (8 bit).

- **[[Sistemi e reti(Internetworking).pdf#page=179&selection=107,2,107,10&color=yellow|Checksum]]**: ==contiene i bit per il controllo degli errori di trasmissione== (16 bit).

- **[[Sistemi e reti(Internetworking).pdf#page=179&selection=111,3,111,20&color=yellow|Type Specific Data]]**: ==contiene informazioni che dipendono dal tipo di servizio che l’ICMP sta offrendo==. *Per esempio* le più comuni *Echo Request/Echo Reply comprendono un identificatore e un numero sequenziale che servono a identificare ciascuna richiesta di eco e ciascuna risposta* (32 bit).

---
[[Sistemi e reti(Internetworking).pdf#page=179&selection=121,1,122,26&color=yellow|Le funzioni svolte da ICMP]]

Le principali funzioni che il protocollo ICMP può svolgere sono:

- ==Fornire messaggi== di eco per ==verificare la corretta configurazione di host sulla rete e che quindi una qualsiasi destinazione sia raggiungibile==: *Echo Request* (Type 8) del mittente, *Echo Reply* (Type 0) del destinatario. ==Si realizza con il comando ping==;

- ==Segnalare una destinazione non raggiungibile== ==perché sconosciuta o perché un pacchetto è troppo grande ma non è consentito frammentarlo==: *Destination Unreachable* (Type 3);

- ==Avvertire il mittente di rallentare l’invio dei pacchetti per problemi di congestione==: Source Quench (Type 4);

- ==Reindirizzare il traffico per fornire un instradamento efficiente in caso di router congestionato da traffico eccessivo==: Routing Redirect (Type 5);

- ==Avvertire il mittente che il tempo di vita di un suo pacchetto è scaduto== (TTL = 0) ==e che quindi il pacchetto viene scartato==: *Time Exceeded* (Type 11);

- ==Valutare le prestazioni di una rete misurando il tempo di attraversamento==: Timestamp Request (Type 13) del mittente, Timestamp Reply (Type 14) del destinatario;

- ==Rilevare la lista dei nodi (router) attraversati da un pacchetto per giungere a destinazione==: Traceroute (Type 30). *Si realizza con il comando tracert*.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=180&selection=11,0,33,26&color=yellow|ICMP consente ai router di scambiarsi informazioni di servizio (messaggi router-to-router) e di tenere sotto controllo le modalità con cui gli host ge nerano pacchetti, inviando loro messaggi per rallentare o dirottare altrove un flusso di pacchetti (messaggi router-to-host). Per quanto riguarda gli host invece, ICMP consente loro di scambiarsi informazio ni di servizio (messaggi host-to-host) e di richiedere ai router informazioni utili sul funzionamento e la topologia della rete (messaggi host-to-router).]]
> > ICMP consente ai router di scambiarsi informazioni di servizio (**messaggi router-to-router**) e di tenere sotto controllo le modalità con cui gli host generano pacchetti, inviando loro messaggi per rallentare o dirottare altrove un flusso di pacchetti (**messaggi router-to-host**). Per quanto riguarda gli host invece, ICMP consente loro di scambiarsi informazioni di servizio (**messaggi host-to-host**) e di richiedere ai router informazioni utili sul funzionamento e la topologia della rete (**messaggi host-to-router**).
> 

---
[[Sistemi e reti(Internetworking).pdf#page=180&selection=40,1,41,6&color=yellow|ICMPv6]]

==Una nuova versione di ICMP è stata definita per lavorare con la versione 6 di IP==, descritta nella Lezione 1. Infatti, lo sviluppo di IPv6 ha reso necessaria una riorganizzazione dei tipi e dei codici esistenti in ICMP e la definizione di nuovi. I==l formato del pacchetto ICMPv6 è, però, rimasto lo stesso di ICMPv4==. ICMPv6 è specificato in RFC 4443 e successivi aggiornamenti.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=180&selection=57,0,62,31&color=yellow|La versione ICMPvó è stata potenziata rispetto alla ICMPv4, aggiungendo nuo ve funzionalità e incorporandone altre derivanti da protocolli IPv4 come IGMP e ARP. I numeri dei messaggi e dei tipi sono diversi da quelli ICMPv4, rendendo così incompatibili i due protocolli.]]
> > **La versione ICMPv6 è stata potenziata rispetto alla ICMPv4**, **aggiungendo nuove funzionalità e incorporandone altre derivanti da protocolli IPv4 come IGMP e ARP**. I numeri dei messaggi e dei tipi sono diversi da quelli ICMPv4, rendendo così **incompatibili i due protocolli**.
> 

---
In ICMPv6 si distinguono due categorie di messaggi:

- **[[Sistemi e reti(Internetworking).pdf#page=180&selection=66,2,66,15&color=yellow|Error message]]**: ==Riportano errori relativi all’inoltro di pacchetti IPv6==, *generati dal destinatario o dai nodi intermedi della rete*; ==questi messaggi hanno il campo Type con valori da 0 a 127== (*bit più significativo = 0*), per esempio:
	- Type 1, Destination Unreachable 
	- Type 2, Packet Too Big (in IPv6 non è più prevista la frammentazione del pacchetto) 
	- Type 3, Time Exceeded

- **[[Sistemi e reti(Internetworking).pdf#page=180&selection=80,3,80,23&color=yellow|Informational message]]**: ==Forniscono informazioni di tipo diagnostico e sugli host della rete==; questi messaggi hanno il ==campo Type con valori da 128 a 255== (**bit più significativo = 1**), per esempio.
	- Type 128, Echo Request 
	- Type 129, Echo Reply

---
[[D, Il protocollo ARP]]

