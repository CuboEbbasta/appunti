La suddivisione degli indirizzi in classi può creare un grosso spreco di indirizzi.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=139&selection=23,0,41,62&color=yellow|Per cercare di porre rimedio a sprechi e carenze, in attesa dell’IPv6, nel 1993 è stato introdotto un nuovo schema di indirizzamento, la CIDR (Classiess Inter Domain Routing, pronunciata “saider”), anche nota come supernetting perché crea una super rete composta da più reti. In pratica la CIDR non applica subnetting ed elimina il concetto di classe di indirizzi (classiess)]]
> > Per cercare di porre rimedio a sprechi e carenze, in attesa dell’IPv6, nel 1993 è stato introdotto un nuovo schema di indirizzamento, la CIDR (Classiess Inter Domain Routing, pronunciata “saider”), anche nota come supernetting perché crea una super rete composta da più reti. In pratica la CIDR non applica subnetting ed elimina il concetto di classe di indirizzi (classiess)

Supponiamo di dover indirizzare 1.500 host e che quindi un indirizzo in classe C non basti (28 - 2 = 254) e uno in classe B sia eccessivo (216 - 2 = 65.534).

Prendiamo allora 6 indirizzi in classe C consecutivi:
1° 200.45. 8.0    11001000.00101101.**00001**0==00==.00000000
2° 200.45. 9.0    11001000.00101101.**00001**0==01==.00000000 
3° 200.45.10.0   11001000.00101101.**00001**0==10==.00000000 
4° 200.45.11.0   11001000.00101101.**00001**==011==.00000000 
5° 200.45.12.0   11001000.00101101.**00001**==100==.00000000 
6° 200.45.13.0   11001000.00101101.**00001**==101==.00000000

Ciascuno di loro consentirà di indirizzare 254 host avendo l'ultimo ottetto interamente libero per gli host, per un totale di 254 x 6 = 1.524 host, quindi misuratamente oltre le richieste di pianificazione.

La maschera verrà settata al valore:
255.255.248.0 = 11111111.11111111.==11111==000.00000000

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=140&selection=22,0,28,8&color=yellow|Con la CIDR non è corretto parlare di subnet mask, in quanto non esistono sot toreti e non viene fatto il subnetting. È invece corretto far riferimento a una ma schera per l’intera rete costituita dal blocco di indirizzi IP di rete consecutivi. Tale maschera prende il nome di netmask.]]
> > Con la CIDR non è corretto parlare di subnet mask, in quanto non esistono sot toreti e non viene fatto il subnetting. È invece corretto far riferimento a una ma schera per l’intera rete costituita dal blocco di indirizzi IP di rete consecutivi. Tale maschera prende il nome di netmask.

---
Il **supernetting**, noto anche come **route aggregation**, è una tecnica utilizzata per combinare più reti IP contigue in una rete più grande (detta supernet). Questo viene fatto per ridurre il numero di rotte presenti nelle tabelle di routing, semplificando così la gestione della rete.

È importante sottolineare che il supernetting funziona solo se le reti da combinare sono **contigue** e se i loro prefissi condividono un certo numero di bit iniziali in comune.

---

### **Quando si usa il supernetting?**

1. **Riduzione della complessità del routing**: meno rotte nelle tabelle di routing, ad esempio nei router o nelle tabelle BGP.
2. **Efficienza nella gestione delle risorse IP**: si aggregano più reti per creare una rappresentazione unificata.

---

### **Esempio dettagliato**

Supponiamo di avere le seguenti reti:

- **192.168.1.0/24**
- **192.168.2.0/24**

Queste due reti sono contigue, quindi possiamo combinarle in un'unica supernet.

#### **Passaggi del supernetting:**

1. **Rappresentare gli indirizzi in binario** Rappresentiamo gli indirizzi di rete delle due subnet in binario per capire quanti bit iniziali sono comuni:
    
    - **192.168.1.0**: `11000000.10101000.00000001.00000000`
    - **192.168.2.0**: `11000000.10101000.00000010.00000000`
2. **Identificare i bit comuni** Confrontiamo i due indirizzi:
    
    ```
    192.168.1.0: 11000000.10101000.00000001.00000000
    192.168.2.0: 11000000.10101000.00000010.00000000
    ```
    
    I primi **23 bit** sono identici: `11000000.10101000.0000000`.
    
3. **Calcolare il nuovo prefisso**
    
    - Il nuovo prefisso sarà **/23** (23 bit in comune).
    - La nuova rete sarà **192.168.0.0/23**.
4. **Determinare l’intervallo IP coperto dalla supernet**
    
    - **Indirizzo di rete**: 192.168.0.0 (11000000.10101000.00000000.00000000)
    - **Broadcast**: 192.168.1.255 (11000000.10101000.00000001.11111111)
    
    La supernet **192.168.0.0/23** include **192.168.0.0 - 192.168.1.255**.
    

---

### **Altro esempio: Aggregazione di 4 reti**

Supponiamo di avere 4 reti:

- **192.168.0.0/24**
- **192.168.1.0/24**
- **192.168.2.0/24**
- **192.168.3.0/24**

1. **Rappresentazione binaria**:
    
    - 192.168.0.0: `11000000.10101000.00000000.00000000`
    - 192.168.1.0: `11000000.10101000.00000001.00000000`
    - 192.168.2.0: `11000000.10101000.00000010.00000000`
    - 192.168.3.0: `11000000.10101000.00000011.00000000`
2. **Identificare i bit comuni**: I primi **22 bit** sono comuni:
    
    ```
    11000000.10101000.000000
    ```
    
3. **Nuova rete**: La nuova supernet sarà **192.168.0.0/22**.
    
4. **Intervallo IP coperto**:
    
    - **Indirizzo di rete**: 192.168.0.0 (11000000.10101000.00000000.00000000)
    - **Broadcast**: 192.168.3.255 (11000000.10101000.00000011.11111111)
    
    La rete **192.168.0.0/22** copre **192.168.0.0 - 192.168.3.255**.
    

---

### **Condizioni per il supernetting**

1. **Contiguità delle reti**: Gli indirizzi di rete devono essere consecutivi.
2. **Potenza di 2**: Il numero di reti da combinare deve essere una potenza di 2 (es. 2, 4, 8, ecc.).
3. **Prefissi uguali per i bit iniziali**: Le reti devono condividere un prefisso comune.

---

Se vuoi un ulteriore esempio o un'applicazione pratica, fammi sapere! 😊

---
[[VLSM]]