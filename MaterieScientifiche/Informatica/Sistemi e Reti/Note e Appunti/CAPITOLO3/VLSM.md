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

Essendo 3 i link si dovranno assegnare 3 indirizzi di rete per identificarli. A ogni router occorrono 2 indirizzi a disposizione delle sue porte per interfacciare il resto della rete, quindi basterà prevedere sottoreti con 2 bit (gli ultimi 2) per rindirizzamento. Occorre sempre fare molta attenzione che non ci siano porte di host o router con lo stesso indirizzo. Una possibile soluzione potrebbe essere:



|     | INDIRIZZI DI RETE   | SUBNET MASK              |
| --- | ------------------- | ------------------------ |
| L1  | 192.168.1.111100 00 | 255.255.255.111111 00/30 |
| L2  | 192.168.1.111110 00 | 255.255.255.111111 00/30 |
| L3  | 192.168.1.111111 00 | 255.255.255.111111 00/30 |

La [[Sistemi e reti(Internetworking).pdf#page=143&selection=69,2,74,0&color=yellow|figura 11]] mostra lo schema logico della rete.

---
### **VLSM (Variable Length Subnet Mask)**

Il **VLSM** consente di applicare subnet mask di lunghezza variabile, assegnando spazio IP in modo più efficiente in base alle esigenze di ogni sottorete.

#### Esempio

Abbiamo la rete **192.168.1.0/24** e dobbiamo assegnare:

- Sottorete 1: 50 host
    
- Sottorete 2: 30 host
    
- Sottorete 3: 10 host
    
- **Passaggi:**
    
    1. Iniziamo dalla sottorete più grande (50 host). Servono almeno 6 bit per gli host (26−2=622^6 - 2 = 6226−2=62).
        - Subnet mask: **/26** (255.255.255.192).
        - Rete: 192.168.1.0 – 192.168.1.63.
    2. La seconda sottorete richiede 30 host. Servono 5 bit (25−2=302^5 - 2 = 3025−2=30).
        - Subnet mask: **/27** (255.255.255.224).
        - Rete: 192.168.1.64 – 192.168.1.95.
    3. La terza sottorete richiede 10 host. Servono 4 bit (24−2=142^4 - 2 = 1424−2=14).
        - Subnet mask: **/28** (255.255.255.240).
        - Rete: 192.168.1.96 – 192.168.1.111.
- **Distribuzione in binario**:
	Sottorete 1: 192.168.1.0/26    (11000000.10101000.00000001.00**000000**)
	Sottorete 2: 192.168.1.64/27   (11000000.10101000.00000001.010**00000**)
	Sottorete 3: 192.168.1.96/28   (11000000.10101000.00000001.0110**0000**)

---

La confusione potrebbe sorgere dal modo in cui interpretiamo i bit della subnet mask rispetto agli indirizzi IP e ai concetti di **Net ID** e **Host ID**. Vediamo di chiarire tutto.

### **Subnet Mask, Net ID e Host ID**

La **subnet mask** determina quali parti dell'indirizzo IP appartengono al **Net ID** e quali all'**Host ID**.

- I **bit a 1** della subnet mask identificano i bit che fanno parte del **Net ID**.
- I **bit a 0** della subnet mask identificano i bit che fanno parte dell'**Host ID**.

### **Comportamento del Net ID e dell'Host ID**

Quando parliamo dell'**Indirizzo di Rete** (Network Address), la parte di **Net ID** dell'indirizzo è **fissa**, mentre la parte di **Host ID** è impostata a **tutti zero**. Questo perché l'indirizzo di rete rappresenta la rete stessa, quindi tutti i bit degli host (quelli che la subnet mask ha impostato a 0) devono essere "azzerati".

Quando invece parliamo dell'**Indirizzo di Broadcast**, la parte di **Net ID** resta invariata, mentre la parte di **Host ID** è impostata a **tutti uno**. Questo perché l'indirizzo di broadcast rappresenta tutti gli host all'interno di una rete.

---

### **VLSM e il Concetto di Net ID e Host ID in Binario**

Nel contesto di **VLSM** (Variable Length Subnet Mask), creiamo diverse sottoreti con lunghezze di subnet mask diverse, ma la logica dietro il Net ID e l'Host ID rimane la stessa.

#### Ad esempio:

Supponiamo di avere l'indirizzo **192.168.1.0/24** e di volerlo suddividere in sottoreti più piccole.

Se creiamo una sottorete con una subnet mask **/26**, questa subnet mask avrà i primi 26 bit come Net ID e i successivi 6 bit come Host ID:

- Subnet Mask /26:
    
    ```
    11111111.11111111.11111111.11000000 (255.255.255.192)
    ```
    

L'indirizzo **192.168.1.0/24** (in binario) è:

```
11000000.10101000.00000001.00000000
```

Con la subnet mask **/26**, i primi **26 bit** (quelli a 1) sono **Net ID**, mentre i **6 bit** a 0 sono **Host ID**.

---

### **Sottoreti con VLSM: Come funziona il cambiamento**

Quando suddividiamo la rete **192.168.1.0/24** in sottoreti più piccole usando **VLSM**, cambiamo la subnet mask per ogni sottorete. Vediamo come ciò influenzi la parte di **Host ID** e **Net ID**:

1. **Sottorete 1: /26 (255.255.255.192)**
    
    L'indirizzo di rete per la sottorete **192.168.1.0/26** è:
    
    ```
    11000000.10101000.00000001.00000000
    ```
    
    - Net ID: i primi **26 bit**.
    - Host ID: gli ultimi **6 bit**.
    
    La parte di **Net ID** (26 bit) rimane **fissa**. La parte di **Host ID** può variare (ma deve essere 0 per l'indirizzo di rete e tutti 1 per l'indirizzo di broadcast).
    
    **Indirizzo di Rete**: 192.168.1.0 **Indirizzo di Broadcast**: 192.168.1.63 (in binario: `11000000.10101000.00000001.00111111`)
    
2. **Sottorete 2: /27 (255.255.255.224)**
    
    La subnet mask **/27** ha i primi **27 bit** come **Net ID** e i successivi **5 bit** come **Host ID**:
    
    ```
    11111111.11111111.11111111.11100000
    ```
    
    L'indirizzo **192.168.1.64/27** è:
    
    ```
    11000000.10101000.00000001.01000000
    ```
    
    - Net ID: i primi **27 bit**.
    - Host ID: gli ultimi **5 bit**.
    
    La parte di **Net ID** (27 bit) è **fissa**, mentre la parte di **Host ID** può variare.
    
    **Indirizzo di Rete**: 192.168.1.64 **Indirizzo di Broadcast**: 192.168.1.95 (in binario: `11000000.10101000.00000001.01011111`)
    

---

### **Perché la parte di Net ID è fissa e quella di Host ID cambia**

Quando lavoriamo con l'indirizzo di rete e l'indirizzo di broadcast:

- **Net ID** (i bit a 1 della subnet mask) **resta invariato**, perché identifica la rete in cui ci troviamo.
- **Host ID** (i bit a 0 della subnet mask) **cambia**. Se lavoriamo con l'indirizzo di rete, tutti i bit di Host ID sono impostati a **0**. Se lavoriamo con l'indirizzo di broadcast, tutti i bit di Host ID sono impostati a **1**.

Quindi, quando suddividiamo l'indirizzo IP in sottoreti, la parte di **Net ID** cambia solo se modifichiamo i bit della subnet mask. Altrimenti, i bit di **Net ID** restano uguali per tutte le sottoreti, mentre la parte di **Host ID** varia per ciascun indirizzo nella rete.

---

### **Conclusione**

Quando lavoriamo con VLSM, è la **subnet mask** a determinare quante porzioni dell'indirizzo IP appartengono al **Net ID** e quante all'**Host ID**. La parte di **Net ID** è quella che **resta fissa** e non cambia per le diverse sottoreti, mentre la parte di **Host ID** cambia (specialmente per gli indirizzi di rete e broadcast, ma anche per gli host stessi).

---

[[IPv6]]