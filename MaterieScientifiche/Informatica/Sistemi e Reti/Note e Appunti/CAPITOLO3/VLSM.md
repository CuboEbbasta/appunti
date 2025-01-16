==Tutte le subnet di una stessa rete tipicamente usano la stessa subnet mask (subnetting statico)==. Tuttavia questa strategia, pur essendo semplice da implementare e facile da gestire, in alcuni casi spreca spazio di indirizzamento. Alcune subnet possono avere molti host e altre soltanto pochi, ma tutte utilizzano (consumano) l’intero spazio di indirizzi assegnato, con evidente spreco. Inoltre, ==il subnetting statico costringe a fissare sia il numero massimo di subnet nella rete sia il numero massimo di host per subnet al momento della progettazione della rete e della conseguente pianificazione degli indirizzi==. Qualsiasi eventuale evoluzione della rete stessa (come l’esigenza di più subnet rispetto al previsto o la necessità di superare il numero massimo di host preventivati in una subnet) potrebbe costringere al completo rifacimento del piano di indirizzamento. ==**In definitiva il subnetting statico non facilita la flessibilità e la scalabilità di una rete**.==

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=140&selection=89,0,98,28&color=yellow|Una tecnica che permette ai provider di utilizzare in modo più efficiente lo spa zio di indirizzi è detta VLSM (Variable Length Subnet Mask). Un provider può usare una subnet mask lunga sulle subnet con pochi host e una subnet mask breve sulle subnet con molti host.]]
> > Una tecnica che permette ai provider di utilizzare in modo più efficiente lo spa zio di indirizzi è detta VLSM (Variable Length Subnet Mask). Un provider può usare una subnet mask lunga sulle subnet con pochi host e una subnet mask breve sulle subnet con molti host.

 ==**Con questo metodo**, **si ha un indirizzamento di tipo classless**.==

---
**[[Sistemi e reti(Internetworking).pdf#page=142&selection=184,2,184,10&color=yellow|PROBLEMA]]**:

Supponiamo di avere una rete sempre con indirizzo privato in classe C, 192.168.1.0/24, che però, a differenza dell'esercizio precedente, sia costituita invece che da una LAN con 3 subnet (cioè un solo router), da 3 LAN fisicamente separate (3 router) ma che costituiscono un'unica rete logica su un territorio più ampio (una MAN). In questo caso occorre pianificare gli indirizzi anche per i link tra i router. Le 3 LAN hanno rispettivamente 50 host la prima (N1), 40 la seconda (N2) e 20 la terza (N3)

192.168.1.0/24

50/40/20 (N1,N2,N3)

N1) 2^6 = 64 > 50
N2) 2^6 = 64 > 40
N3) 2^5 = 32 > 20


|     | INDIRIZZI DI RETE   | SUBNET MASK              |
| --- | ------------------- | ------------------------ |
| 1   | 192.168.1.00 000000 | 255.255.255.11 000000/26 |
| 2   | 192.168.1.01 000000 | 255.255.255.11 000000/26 |
| 3   | 192.168.1.100 00000 | 255.255.255.111 00000/26 |

Essendo 3 i link si dovranno assegnare 3 indirizzi di rete per identificarli. A ogni router oc corrono 2 indirizzi a disposizione delle sue porte per interfacciare il resto della rete, quindi basterà prevedere sottoreti con 2 bit (gli ultimi 2) per rindirizzamento. Occorre sempre fare molta attenzione che non ci siano porte di host o router con lo stesso indirizzo. Una possibile soluzione potrebbe essere:



|     | INDIRIZZI DI RETE   | SUBNET MASK              |
| --- | ------------------- | ------------------------ |
| L1  | 192.168.1.111100 00 | 255.255.255.111111 00/30 |
| L2  | 192.168.1.111110 00 | 255.255.255.111111 00/30 |
| L3  | 192.168.1.111111 00 | 255.255.255.111111 00/30 |

La [[Sistemi e reti(Internetworking).pdf#page=143&selection=69,2,74,0&color=yellow|figura 11]] mostra lo schema logico della rete.

---

[[IPv6]]