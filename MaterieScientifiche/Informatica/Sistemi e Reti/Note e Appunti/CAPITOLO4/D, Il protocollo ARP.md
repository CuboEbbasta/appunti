> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=181&selection=80,0,95,63&color=yellow|Sistemi e reti(Internetworking), p.181]]
> > In ambito IETF è stato sviluppato **il protocollo ARP** (Address Resolution Protocol), RFC 826, che **definisce le modalità di comunicazione tra gli host di una rete locale per trovare il MAC address di una scheda di rete della quale si conosce solo l’indirizzo IP**. Questa **operazione** è **detta risoluzione dell'indirizzo IP**. *ARP è usato solamente per indirizzi IPv4, non funziona con IPv6*.

---
[[Sistemi e reti(Internetworking).pdf#page=181&selection=143,0,145,17&color=yellow|IL FORMATO DEL PACCHETTO ARP]]

==Il protocollo ARP prevede solo due tipi di messaggi==: ==ARP Request, per la richiesta di risoluzione di un indirizzo IP==, e ==ARP Reply, per la risposta contenente l’indirizzo IP richiesto==.

Formato del pacchetto ARP:  [[Sistemi e reti(Internetworking).pdf#page=182&selection=26,0,27,1&color=yellow|Figura 6]]

 ==**HEADER**==:
	 
- ==**Hardware Type**==: **indica il tipo di rete a livello Physical**, 0x0001 sta per Ethernet.
	
- ==**Protocol Type**==: **indica il tipo di protocollo a livello Network**, 0x0800 sta per IP.
	
- ==**Hardware Address Length**==: **è la lunghezza**, **in ottetti** **dell’indirizzo fisico** (6 Byte).
	
- ==**IP Address Length**==: **è la lunghezza**, **in ottetti**, **dell’IP address** (4 Byte).
	
- ==**Operation Code**==: **specifica se il pacchetto è una ARP Request** (1) **o una ARP Reply** (2).

==**PAYLOAD**==:
##  Tabella per il Payload dell'ARP

| Campo                           | ARP Request                                                                                | ARP Reply                                                                           |
| ------------------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| ==**Sender Hardware Address**== | ==Indirizzo fisico del mittente== (MAC address)                                            | ==Indirizzo fisico dell'host richiesto con la ARP Request==                         |
| **Sender Protocol Address**     | ==Indirizzo logico del mittente== (IP address)                                             | ==Indirizzo logico del mittente==                                                   |
| **Target Hardware Address**     | *Il campo non è valorizzato in quanto sconosciuto* (è l'indirizzo fisico richiesto con ARP | ==Indirizzo fisico del destinatario== (cioè dell'host che ha inviato l'ARP Request) |
| **Target Protocol Address**     | ==Indirizzo logico del destinatario==                                                      | ==Indirizzo logico del destinatario==                                               |

**Esempio:**

Immaginiamo che un dispositivo con l'IP address **192.168.1.10** voglia scoprire l'indirizzo fisico di un altro dispositivo con l'IP address **192.168.1.5**.  L'ARP Request inviato da 192.168.1.10 avrà:

* **Sender Hardware Address:** MAC address del dispositivo 192.168.1.10
* **Sender Protocol Address:** 192.168.1.10
* **Target Protocol Address:** 192.168.1.5


La risposta ARP inviata dal dispositivo con l'IP address **192.168.1.5** avrà:

* **Sender Hardware Address:** MAC address del dispositivo 192.168.1.5
* **Sender Protocol Address:** 192.168.1.5
* **Target Hardware Address:** - (non applicabile)

---
[[Sistemi e reti(Internetworking).pdf#page=182&selection=101,0,105,17&color=yellow|LA RISOLUZIONE DELL'INDIRIZZO IP]]

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=182&selection=107,0,115,11&color=yellow|Sistemi e reti(Internetworking), p.182]]
> > Un implementazione TCP/IP utilizza di norma una **cache ARP** (detta anche **ARP Table**), dove ogni host mantiene e aggiorna una tabella con tutte le coppie IP-MAC a lui note.

==Quando un host deve inviare dei pacchetti, controlla se nella cache ARP è presente l’indirizzo MAC corrispondente all’indirizzo IP del destinatario==. S==e non c’è, allora entra in gioco il protocollo ARP== che stabilisce il seguente iter basato sui due tipi di messaggi, ==ARP Request e ARP Reply==:

1. ==**Il mittente invia un pacchetto ARP contenente una ARP Request** **in cui specifica l’indirizzo IP del destinatario di cui vuole conoscere il corrispondente indirizzo MAC**==.
   ==Questo **pacchetto ARP** viene **mandato all’indirizzo MAC di broadcast Ethernet== FF-FF-FF-FF-FF-FF**, cioè a tutti i nodi della rete. **==Inoltre il mittente aggiunge anche il proprio IP e il proprio MAC affinché il destinatario possa aggiungere la coppia di indirizzi nella propria cache ARP==**.
   
2. ==**Tutti gli host della rete ricevono l’ARP Request e leggono l'IP in esso specificato**==:
	
- ==**Se l’indirizzo IP non corrisponde al proprio**==, **gli host ==ignorano il pacchetto e la sua richiesta**==.
	
- **==Se un host riscontra che l'IP specificato è il proprio indirizzo==**, **allora prepara un ==pacchetto ARP di risposta contenente una ARP Reply in cui specifica l’indirizzo MAC corrispondente al proprio IP**==; *inoltre aggiunge la coppia di indirizzi IP-MAC del mittente nella propria cache ARP*.

1. ==**Il mittente**, **ricevuta la risposta**, **aggiorna la propria cache ARP e avvia la comunicazione**==.

   ==**Il procedimento ARP è differente se utilizzato su reti remote**==. ==**Per dialogare con l’host remoto**, **l’host mittente si affida al gateway predefinito**==, *impostato nelle proprietà del TCP/IP*, **al quale ==dirige tutto il traffico indirizzato all’host che non riesce a raggiungere==**.
   ==**Se eventualmente poi si trattasse di un’implementazione TCP/IP che non prevede il gateway**, **il mittente invierebbe i pacchetti al router di rete==. In ogni caso ==il mittente può usare il pacchetto ARP per individuare gateway o router**, **qualora il loro MAC non fosse mappato nella sua cache ARP**, **nello stesso modo con cui individuava il MAC dell’host destinatario in locale**==.
   
   **È possibile conoscere il contenuto della propria cache ARP eseguendo il seguente comando** dal prompt dei comandi di Windows: **==arp -a==** ([[Sistemi e reti(Internetworking).pdf#page=183&selection=6,0,6,8&color=yellow|Figura 7]])

**Esiste anche ==il protocollo RARP**== (Reverse Address Resolution Protocol) **che ==permette l’operazione inversa**== cioè ==**consente a un host della rete che non conosce il proprio indirizzo IP**== (per esempio periferiche di rete che necessitano di un indirizzo IP) ==**di chiederlo inviando il proprio MAC**==. ==**La richiesta va inoltrata però a un server RARP**, **l’unico in grado di avere nella propria cache ARP il MAC richiesto**==. ==Anche il pacchetto RARP è costituito dai due tipi di messaggi==: **RARP Request e RARP Reply**.

--- 
[[Sistemi e reti(Internetworking).pdf#page=184&selection=7,1,8,27&color=yellow|ANALISI DI UN PACCHETTO ARP]]

Nella [[Sistemi e reti(Internetworking).pdf#page=184&selection=15,1,18,1&color=yellow|figura 8]] vediamo nel dettaglio un pacchetto ARP di tipo ARP Request (campo Opcode = 1) in cui l’host 192.168.1.1 chiede all’host 192.168.1.6 di inviargli il suo MAC address (campo Target MAC address = 00:00:00:00:00:00).

---
[[Sistemi e reti(Internetworking).pdf#page=184&selection=324,1,325,23&color=yellow|Le vulnerabilità di ARP]]

==Il protocollo ARP è uno dei più vecchi protocolli sviluppati per la suite TCP/IP==, quando ancora non si prevedeva la diffusione capillare di Internet e non sembrava necessario mettere in campo azioni preventive per la protezione delle reti.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=185&selection=22,0,30,87&color=yellow|Lo spoofing risulta relativamente semplice per un pirata informatico: è sufficiente che invii a un host di una rete X un pacchetto ARP contenente una ARP Reply in cui affermi che il proprio indirizzo MAC è associato a un indirizzo IP della rete X stessa.]]
> > **Lo spoofing risulta relativamente semplice per un pirata informatico**: **è sufficiente che invii a un host di una rete X un pacchetto ARP contenente una ARP Reply in cui affermi che il proprio indirizzo MAC è associato a un indirizzo IP della rete X stessa**.
> 

**Spoofing**: ==È la falsificazione dell'identità==. Questa ==tecnica== può essere ==utilizzata per falsificare diverse informazioni==, come per esempio ==l'identità di un host all'interno di una rete o il mittente di un messaggio==.

---
==Poiché non vi è alcun modo di verificare la veridicità di un’identità==, ==chiunque può introdursi in una rete facendo credere di esserne un legittimo utente==, ottenendo così accesso alle risorse della rete, per esempio al data base aziendale. **La scopo di questi attacchi è di ingannare lo switch, ==inquinandone la cache ARP**== (==ARP cache poisoning==), **al punto da indurlo a inoltrare pacchetti verso destinazioni altri menti non raggiungibili**.

La [[Sistemi e reti(Internetworking).pdf#page=185&selection=65,0,65,9&color=yellow|figura10]] mostra la sequenza di attacco di tipo spoofing al protocollo ARP.

---
[[E, Comandi ping]]

[[A, Routing e Routing Table]]