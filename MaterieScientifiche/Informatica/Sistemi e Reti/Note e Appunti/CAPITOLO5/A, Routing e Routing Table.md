Nell’Unità 3 abbiamo visto come il routing (instradamento) sia una funzione fondamentale del livello Network dell’architettura TCP/IP. Tale funzione viene svolta dal router (intermediate System), che, per poter ottimizzare il percorso dei pacchetti da instradare, deve conoscere ed eventualmente aggiornare una serie di informazioni:
- l’indirizzo del destinatario;
- i router adiacenti; 
- l’insieme dei possibili percorsi (route) verso tutte le reti remote;
- il percorso migliore per ciascuna rete remota; 
- il modo di mantenere e di verificare le informazioni necessarie per il routing.

Il router deve quindi costruire, nella propria memoria, una tabella di instradamento, detta routing table, che gli permetta di memorizzare i dati indispensabili per individuare il percorso ottimale verso le reti remote da raggiungere.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=209&selection=71,0,78,44&color=yellow|Sistemi e reti(Internetworking), p.209]]
> > La routing table è una lista di tutte le reti che il router può raggiungere insie me a inform azioni sulle modalità di instradam ento. Quando il router effettua il forwarding di un pacchetto, ricerca nella routing table l'indirizzo di rete corrispondente all'indirizzo IP di destinazione.
> 

Il formato della tabella di routing varia a seconda del protocollo di routing utilizzato. In generale ogni riga (detta entry) della tabella presenta 4 campi:

- **Network address**: contenente l’indirizzo IP di ciascuna rete raggiungibile;

- **next hop**: l’indirizzo del router successivo nel percorso verso il destinatario;

- **interface**: interfaccia del router a cui deve essere inoltrato il pacchetto per rag giungere il next hop (un router può avere più interfacce di rete);

- **metric**: è una misura utilizzata dal router per decidere quale percorso inserire nel la routing table quando ci sono più alternative. Alla metrica si associa il concetto intuitivo di “costo”: nella routing table si inserisce il percorso a costo minore (vedremo che il protocollo di routing OSPF sostituisce il termine “metric” proprio con “cost”). La metrica più semplice è quella del numero di hop necessari per raggiungere la destinazione (hop count, mostrato nella [[Sistemi e reti(Internetworking).pdf#page=209&selection=118,0,120,1&color=yellow|figura1]] ). Altre metriche considerano parametri quali: l'ampiezza di banda, il numero di pacchetti persi o errati, il ritardo nella trasmissione.

---
[[Sistemi e reti(Internetworking).pdf#page=211&selection=12,0,14,6&color=yellow|DEFAULT ROUTER]]

Il router deve estrarre dall’header IP del datagram l’indirizzo del destinatario e ana lizzare i bit dedicati all’indirizzo di rete. Nel caso più semplice in cui l’indirizzo di rete del destinatario sia presente nel campo network address della routing table, il pacchetto viene instradato verso la sua destinazione, in modo diretto o indiretto, co me visto nell'esercizio precedente.

Può però succedere che il destinatario appartenga a una rete non presente nella tabella di routing. In questo caso il router inoltrerà il pacchetto verso un router di default che lo prenderà in carico col compito di farlo giungere a destinazione. Se nella routing table non è definita questa default route, il router invia al mittente un messaggio ICMP Destination Unreachable.

---
[[Sistemi e reti(Internetworking).pdf#page=211&selection=39,0,45,13&color=yellow|ROUTING STATICO E ROUTING DINAMICO]]

Il funzionamento di un router è caratterizzato dal modo in cui la tabella di routing viene creata:
- **manualmente**, se la tabella di routing è inserita dall’amministratore; in questo caso si parla di routing statico (utilizzabile per piccole reti);
- **automaticamente**, se il router costruisce da solo la tabella di routing in funzione delle informazioni ricevute attraverso i protocolli di routing; in quest’altro caso si parla di routing dinamico.

Il routing statico ha il vantaggio di non richiedere che i router si scambino informazio ni per aggiornare i percorsi o eventualmente individuarne di nuovi, limitando così l’uso di banda. Inoltre essendo i percorsi già determinati una volta configurata la tabella, non è richiesto altro sforzo computazionale da parte del router stesso per calcolare i percorsi ottimali. Il routing statico ha però l’inconveniente di richiedere sempre la riconfigurazione da parte dell’am m inistratore tutte le volte che si devono modificare le entry, sia in seguito a guasti, sia per inserire nuove route; inoltre tale metodo comincia a di venire abbastanza oneroso quando l’Internetwork contiene parecchi percorsi. Per questi motivi il routing statico viene usato quando il numero dei segmenti di LAN non è elevato.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=211&selection=84,0,97,0&color=yellow|Il routing dinamico permette ai vari router di scambiarsi le informazioni neces sarie a determinare i possibili percorsi per raggiungere destinazioni remote me diante dei protocolli, chiamati appunto routing protocol, che usano appropriati algoritmi di routing.]]
> > Il routing dinamico permette ai vari router di scambiarsi le informazioni neces sarie a determinare i possibili percorsi per raggiungere destinazioni remote me diante dei protocolli, chiamati appunto routing protocol, che usano appropriati algoritmi di routing.
>
> 

Il vantaggio di tale metodo è che richiede un minor controllo da parte dell’am m i nistratore; per contro richiede un maggior uso di banda rispetto al routing stati co perché, oltre al traffico relativo ai pacchetti, c’è un traffico relativo allo scam bio delle informazioni indispensabili ai routing protocol. Inoltre, un altro notevole beneficio è dato dalla capacità di adattarsi automaticamente ai cambiamenti della topologia di rete: se si verifica un guasto lungo una connessione oppure ne viene attivata una nuova, gli aggiornamenti dei vari percorsi vengono automaticamente propagati a tutti i router.
Nella [[Sistemi e reti(Internetworking).pdf#page=212&selection=6,0,7,1&color=yellow|TABELLA 1]] si mettono a confronto routing statico e dinamico sulla base delle principali caratteristiche del processo di routing.

---
[[Sistemi e reti(Internetworking).pdf#page=212&selection=71,4,71,49&color=yellow|II problema della ricerca nella routing table]]

Un problema molto comune e assai studiato in letteratura è il cosiddetto Routing Table Lookup Problem (RTLP), cioè il problema di dover decidere molto in fretta dove in stradare i pacchetti per evitare rallentamenti e relative congestioni. La difficoltà di RTLP risiede nel numero estremamente elevato di pacchetti che devono essere esaminati ogni secondo. Supponiamo di avere un canale da 1 Gbps, avremo che possono arrivare 1 milione di pacchetti da 1 kb in un secondo, quindi non è possibile de dicare più di 1 microsecondo a ciascun pacchetto per contenere il ritardo nell’ordine di un secondo. Il problema assume dimensioni ancora maggiori se si considera che un qualsiasi router ha più interfacce e che il tempo di accesso per una cache veloce è dell’ordine dei 50 nanosecondi: in queste condizioni, sono sufficienti pochi accessi alla memoria per esaurire il tempo disponibile per il routing. Dato che l’RTLP è un problema chiave per lo sviluppo della rete Internet, esso è stato affrontato intervenendo su più fattori con lo scopo di velocizzare al massimo il processo di routing: si sono studiate strutture dati per memorizzare la tabella di routing in maniera compatta ed efficiente, si sono ideati algoritmi per velocizzare la consultazione della tabella stessa, si è proposto di utilizzare sistemi paralleli allo scopo di suddividere il carico di lavoro tra più processori e altro ancora. Tuttavia, tutto questo non è ancora sufficiente: negli ultimi anni l’overhead legato alla gestione del traffico di pacchetti (packet processing) è diventato così critico per le prestazioni che si è cominciato a sviluppare hardware dedicato a tale gestione. In questo contesto, i network processor sono un promettente tentativo di ottenere elevate prestazioni mantenendo almeno parte della flessibilità dei microprocessori tradizionali e con essa la capacità di adattarsi a mutamenti degli algoritmi e dei protocolli di rete.

L'RTLP si può ricondurre alla ricerca, nella tabella, del più lungo prefix corrispondente all'IP del destinatario (ricerca di prefisso di lunghezza mas sima). Per esempio, per i pacchetti indirizzati a 176.16.5.99, il router, tra 176.16.0.0/16 e 176.16.5.0/24, sceglierà quest'ultimo per l'inoltro , poiché ha la corrispondenza più lunga.

---
[[B, Gli algoritmi e i Protocolli di Routing]]