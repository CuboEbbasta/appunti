> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=128&selection=25,0,29,9&color=important|Il subnetting si realizza “sacrificando” alcuni dei bit che le classi A, B e C dedicano agli host per definire un indirizzo di sottorete, SubnetlD, come mostrato nella figura 7.]]
> > Il subnetting si realizza “sacrificando” alcuni dei bit che le classi A, B e C dedicano agli host per definire un indirizzo di sottorete, SubnetlD.

**Per segmentare una rete occorre**, in fase di progettazione, **stabilire quante subnet servono** e, di conseguenza, **quanti bit occorrono per indirizzarle univocamente**. **Nel calcolo è necessario anche valutare il numero massimo di host previsto per ogni subnet e in base a ciò calibrare il quantitativo di bit da suddividere rispettivamente tra subnet e host**. Il risultato di questa attività è il [[Sistemi e reti(Internetworking).pdf#page=128&selection=94,0,94,32&color=yellow|Piano d'indirizzamento]] della rete.

Supponiamo di dover realizzare **50 subnet**: dobbiamo usare una SubnetlD di **6 bit**, essendo **2^6 = 64 maggiore di 50**, mentre **5 bit non sarebbero bastati (25 = 32 minore di 50)**.
	Se usassimo una classe B: 16bit per HostId, ne usiamo 6(2^6) quindi: 16 - 6 = 10 (indirizzi di host per ciascuna subnet) ovvero: 2^10 = 1.022 indirizzi di host per ciascuna subnet.

---
**[[Sistemi e reti(Internetworking).pdf#page=129&selection=96,2,96,14&color=yellow|SUBNET MASK]]**:

Abbiamo visto che per capire qual è l’indirizzo IP del la rete a cui appartiene un host è sufficiente considerare i bit più significativi. Per esempio:
• 130.10.67.160 è un indirizzo di classe B, dal momento che i primi 2 bit sono “1” e “0 ” (13010 = **10** 0000102);
• Sappiamo che un indirizzo di rete deve sempre avere HostID=0; • quindi l’host con indirizzo 130.10.67.160 appartiene alla rete 130.10.0.0.

Con l’introduzione del subnetting non è più così semplice, infatti lo stesso indirizzo IP 130.10.67.160 potrebbe appartenere alla seconda subnet di una rete che è stata suddivisa in 4 subnet. In questo caso l’indirizzo di rete dell’host è 130.10.64.0

---
**[[Sistemi e reti(Internetworking).pdf#page=132&selection=45,20,45,32&color=yellow|MESSA IN AND]]**:

**Il subnetting e le subnet mask svolgono un ruolo fondamentale nell’ottimizzare il traffico della rete** evitando, per esempio, che datagram IP inviati da un host a un altro host, residente nella stessa sottorete, escano e rientrino per giungere a destinazione.

Si individuano, dunque, due tecniche di inoltro dei pacchetti nella rete:
• forwarding diretto: host mittente e destinatario hanno lo stesso NetlD (incluso il SubnetlD), quindi la comunicazione avviene all’interno della stessa rete senza coinvolgere il router;
• forwarding indiretto: host mittente e destinatario hanno un diverso NetlD (in cluso il SubnetlD), quindi sono su reti differenti, il pacchetto viene inviato al router che lo inoltrerà a un altro router e così via fino a destinazione

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=132&selection=88,0,94,40&color=yellow|Il meccanismo che permette di verificare se due host appartengono alla stessa rete (e sottorete) è detto processo di messa in AND (ANDing process) bitwise, cioè bit a bit]]
> > Il meccanismo che permette di verificare se due host appartengono alla stessa rete (e sottorete) è detto processo di messa in AND (ANDing process) bitwise, cioè bit a bit

Questo processo consiste nel fare:
1. un’**operazione di AND bit a bit** tra **l’indirizzo IP del mittente** e **la subnet mask del mittente** ottenendo il NetlD e il SubnetlD del mittente e azzerando l’HostlD;
2. **un’operazione di AND bit a bit** tra **l’indirizzo IP del destinatario** e **la subnet mask del mittente** ottenendo il NetlD e il SubnetlD e azzerando l’HostlD;
3. il confronto tra i due risultati ottenuti: 
	- **se sono uguali mittente e destinatario sono nella stessa subnet** (comunicazione diretta);
	-  **se sono diversi mittente e destinatario non sono nella stessa subnet** (comunica zione attraverso il router)

197.85.100.6
197.85.197.4

- 255.255.11110000.0
- 197.85.01100100.4 =
- 197.85.96.0

- 255.255.11110000.0
- 197.85.11000101.6 =
- 197.85.192.0

Non fanno parte della stessa subnet.

---
**[[Sistemi e reti(Internetworking).pdf#page=133&selection=65,0,65,14&color=yellow|SLASH NOTATION]]**:

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=133&selection=67,0,78,54&color=yellow|È possibile riassumere la coppia indirizzo IP e subnet mask mediante la slash notation in cui all'indirizzo IP viene fatto seguire il prefix length, un numero decimale che indica il numero di bit a 1 della maschera.]]
> > È possibile riassumere la coppia indirizzo IP e subnet mask mediante la slash notation in cui all'indirizzo IP viene fatto seguire il prefix length, un numero decimale che indica il numero di bit a 1 della maschera.

Per esempio:
150.169.3.2/24

Indica che la maschera ha 24 bit a 1, e cioè vale:
255(8bit a 1).255(8).255(8).0(0) quindi: 8+8+8 = 24
**Questa notazione è stata introdotta** con **l’indirizzamento classless**, che non preve de l’uso delle classi A-B-C, introdotto con la tecnica CIDR

---
**[[Sistemi e reti(Internetworking).pdf#page=134&selection=7,1,8,36&color=yellow|ESEMPI DI PIANI DI INDIRIZZAMENTO IP]]**
---

Classe B: 172.104.0.0 
Subnet mask: 255.255.0.0
Sottoreti: 5 quindi 2^3 


| Subnet     | Indirizzo Subnet              | indirizzi di bc della subnet  | range                           |
| ---------- | ----------------------------- | ----------------------------- | ------------------------------- |
| 0(PRIMA)   | 172.104.==000==00000.00000000 | 172.104.==000==11111.11111111 | 172.104.0.1 - 172.104.31.254    |
| 1(SECONDA) | 172.104.==001==00000.00000000 | 172.104.==001==11111.11111111 | 172.104.32.1 - 172.104.63.254   |
| 2(TERZA)   | 172.104.==010==00000.00000000 | 172.104.==010==11111.11111111 | 172.104.64.1 - 170.104.95.254   |
| 3(QUARTA)  | 172.104.==100==00000.00000000 | 172.104.==100==11111.11111111 | 172.104.128.1 - 170.104.159.254 |

---

[[Supernetting]]