> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=302&selection=10,0,13,14&color=yellow|Da quanto emerso nelle Lezioni precedenti è chiaro che TCP sia da preferire per il trasferimento dati in cui è importante l’affidabilità della comunicazione, UDP è invece preferibile quando le prestazioni sono più importanti del ricevere i dati in modo perfetto.]]
> > Da quanto emerso nelle Lezioni precedenti è chiaro che TCP sia da preferire per il trasferimento dati in cui è importante l’affidabilità della comunicazione, UDP è invece preferibile quando le prestazioni sono più importanti del ricevere i dati in modo perfetto.

**UDP si usa**: 
- ==su una rete affidabile oppure quando l’affidabilità non è importante==, per esempio NFS (Network File System); 
- ==quando l’applicazione mette tutti i dati in un singolo datagram==, per esempio DNS (Domain Name System) o NTP (Network Time Protocol); 
- ==quando non è importante che tutti i datagram arrivino a destinazione, ma è necessario non introdurre ritardi==; questa è una tipica esigenza delle applicazioni multimediali, infatti i dati di queste applicazioni devono arrivare entro un tempo limite (un pacchetto in ritardo equivale a un pacchetto perso), inoltre non sarebbe accettabile il ritardo che si avrebbe con la ritrasmissione, tipica dei protocolli di tipo connection-oriented;
- quando eventuali meccanismi di ritrasmissione possono essere gestiti direttamen te dall’applicazione, come per esempio nel protocollo di gestione SNMP (Simple Network Management Protocol).

**TCP si usa**:
- ==quando l’applicazione richiede una comunicazione affidabile==, come per esempio la posta elettronica;
- ==quando è necessario garantire l’integrità dei dati==, per esempio nel trasferimento di file o nell’interrogazione a un database;
- ==quando è necessario garantire che le richieste e le risposte arrivino a destinazione==, per esempio la richiesta di una pagina web;
- ==quando è necessario mantenere il controllo costante della comunicazione== (ossia se ne gestisce lo “stato”)

La [[Sistemi e reti(Internetworking).pdf#page=302&selection=57,0,60,1&color=yellow|TABELLA 3]] presenta le caratteristiche più importanti di un protocollo di livello Transport e ne indica il supporto (sì/no) da parte di TCP e UDP.

Nella Tabella 3 si fa riferimento alla caratteristica path MTU discovery (letteralmente “la scoperta dell’MTU del percorso”). Si tratta della possibilità di inviare pacchetti di dimensione tale da non essere frammentati (tale valore è chiamato PMTU = Path MTU). Per scoprire qual è la PMTU, un host inizia a inviare pacchetti con di mensione pari al minore tra i valori di MTU e MSS, questi pacchetti hanno il bit DF (Don't Fragment) impostato a 1. Se lungo il cammino si trova un router con MTU più piccola, questi invia al mittente un messaggio ICMP che indica che il pacchetto è troppo grande e non può frammentarlo. Il mittente viene a conoscenza del valore di MTU da usare per quel percorso fino a quel router. L’operazione è quindi ripetuta finché il pacchetto non arriva a destinazione. In questo modo il mittente conosce il valore di MTU per quel cammino.

---
[[Sistemi e reti(Internetworking).pdf#page=304&selection=4,0,4,24&color=yellow|IL CONTROLLO DELLE PORTE]]

comando : netstat