L’architettura degli indirizzi IPv6 è specificata nell’RFC 4291. Ha poi subito successive modifiche riportate in vari RFC, tutti elencati nel 4291 come “Updated by”. **Il sistema introdotto da IPv6 richiede di distinguere gli indirizzi in 3 categorie fondamentali: unicast, anycast e multicast**.

- **[[Sistemi e reti(Internetworking).pdf#page=176&selection=27,2,27,9&color=yellow|UNICAST]]**: È un **indirizzo che riguarda un’interfaccia di rete singola**; in altri termini, un indirizzo unicast serve per raggiungere un’interfaccia di rete in modo univoco.

- **[[Sistemi e reti(Internetworking).pdf#page=176&selection=33,2,33,9&color=yellow|ANYCAST]]**: È un **indirizzo che ha le stesse caratteristiche sintattiche di quello unicast**, **attribuito** però **a diverse interfacce di altrettanti nodi**, con **lo scopo di poter raggiungere quello che risponde prima** (quello più vicino in base al protocollo di instradamento). **I pacchetti inviati a un indirizzo anycast raggiungono un’unica interfaccia di rete**, **la prima che risponde**. *Gli indirizzi anycast possono essere usati solo dai router*.

- **[[Sistemi e reti(Internetworking).pdf#page=176&selection=48,2,48,11&color=yellow|MULTICAST]]**: È **attribuito a più interfacce di rete distinte**; **i pacchetti inviati a un indirizzo multicast raggiungono tutte le interfacce di rete cui questo indirizzo è stato attribuito**.

> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=176&selection=70,0,82,54&color=important|La notazione prevede che i 128 bit vengano suddivisi in 8 gruppi di 16 bit (detti hextet) e i 16 bit di ciascun gruppo siano rappresentati con 4 cifre esadecimali. Gli 8 gruppi vengono poi separati dal carattere “ : ”.]]
> > La notazione prevede che i 128 bit vengano suddivisi in 8 gruppi di 16 bit (detti hextet) e i 16 bit di ciascun gruppo siano rappresentati con 4 cifre esadecimali. Gli 8 gruppi vengono poi separati dal carattere “ : ”.

Un esempio di indirizzo IPv6 è: **3401:0db6:0000:0000:00a9:0000:0000:000c**

È consentito omettere gli 0 iniziali (leading zero) di ciascun gruppo e sostituire con un solo 0 un hextet composto da tutti 0 (0000): 3401:db6:0:0:a9:0:0:c

Se l’indirizzo contiene una o più sequenze, contigue, di gruppi di valore 0, una di queste sequenze può essere sostituita dalla notazione “ :: ”, come segue:
3401:db6::a9:0:0:c oppure 3401:db6:0:0:a9::c

*Si noti che solo una delle sequenze 0000 può essere sostituita con ::, in caso contrario l’indirizzo IPv6 non potrebbe più essere ricostruito in modo univoco.*

---
**[[Sistemi e reti(Internetworking).pdf#page=176&selection=113,3,115,14&color=yellow|STRUTTURA INDIRIZZI IPv6]]**:

Ecco come è strutturato un generico ==indirizzo unicast IPv6== ([[Sistemi e reti(Internetworking).pdf#page=176&selection=120,1,124,2&color=yellow|figura 4]]).

- **[[Sistemi e reti(Internetworking).pdf#page=176&selection=208,2,208,23&color=yellow|Global Routing Prefix]]** (o Prefisso): **sono i primi 3 hextet e sono assegnati dagli ISP ai client IPv6**; i primi 3 bit più significativi sono sempre impostati a 001;

- **[[Sistemi e reti(Internetworking).pdf#page=177&selection=6,3,6,11&color=yellow|Subnet ID]]**: **È il quarto hextet e identifica una subnet presente nella rete**. Si possono creare fino a 65.536 subnet diverse. Se non viene usato, può essere lasciato a 0 o a 1 o a qualunque altro valore;

- **[[Sistemi e reti(Internetworking).pdf#page=177&selection=13,2,13,14&color=yellow|Interface ID]]** (IID) : **è rappresentato negli ultimi 4 hextet** e **corrisponde al campo HostlD di IPv4**.

---
**[[Sistemi e reti(Internetworking).pdf#page=177&selection=21,0,23,17&color=yellow|TIPOLOGIE DI INDIRIZZI IPv6]]**:

| Indirizzo                          | Prefisso (Bit)                                                | Descrizione                                                                                                                                                                                                                         |
| ---------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Global Unicast Address (GUA)       | 2000::/3 (prefisso 001)                                       | Indirizzi unicast pubblici e instradabili su Internet. Un'interfaccia di rete può averne assegnati anche più di uno.                                                                                                                |
| Link Local Address (LLA)           | fe80::/10      (i 54 bit successivi al prefisso sono tutti 0) | Indirizzi unicast locali, ogni interfaccia deve averne almeno uno. Si usano solo per le comunicazioni nella rete locale e non su Internet. I 54 bit successivi al prefisso sono tutti 0.                                            |
| Unique Local Unicast Address (ULA) | fd00::/8 o fc00::/7                                           | Indirizzi unicast locali univoci (simili agli indirizzi privati IPv4). Come gli indirizzi Link locali, si usano solo all'interno di una LAN, ma, a differenza di questi, gli indirizzi ULA sono unici a livello globale (RFC 4193). |
| Loopback                           | ::1/128                                                       | Indirizzo di loopback: 0:0:0:0:0:0:0:1. Viene utilizzato per il test e la comunicazione con lo stesso dispositivo.                                                                                                                  |
| Unspecified                        | ::/128                                                        | Indirizzo non specificato: 0:0:0:0:0:0:0:0, è utilizzato in fase di bootstrap come indirizzo sorgente quando l'host non conosce alcun altro suo indirizzo. Non può essere usato come indirizzo di destinazione.                     |
| Multicast                          | ff::/8                                                        | Indirizzi multicast utilizzati per la trasmissione dati a più dispositivi contemporaneamente. L'elenco degli indirizzi multicast predefiniti si trova nell'RFC 4291.                                                                |

ESEMPIO:
GUA: 2000::**/3** -> 2(**001**0),0000,0000,0000 :: 

---
**[[Sistemi e reti(Internetworking).pdf#page=177&selection=135,6,135,39&color=yellow|ASSEGNAZIONE DEGLI INDIRIZZI IPv6]]**:

**Come gli indirizzi IPv4, anche quelli IPv6 sono gestiti da IANA** e, a livello regionale dai RIR (vedi la Lezione 2 dell’Unità 3). L’elenco aggiornato degli indirizzi Global Unicast IPv6 allocati ai RIR si trova al link: www.iana.org/assignments/ipv6-unicastaddress-assignments/ipv6-unicast-address-assignments.xhtml I RIR, come **RIPE NCC per l’Europa**, **allocano gli indirizzi IPv6 agli Internet Registry locali all’area geografica in cui operano**, detti **Local Internet Registry (LIR)**, che **spesso coincidono con gli Internet Service Provider (ISP)**, che **a loro volta assegnano gli indirizzi agli utenti delle reti a cui forniscono il servizio** (provide).

---
[[C, ICMP]]