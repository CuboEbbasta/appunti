I protocolli di routing di tipo EGP (Exterior Gateway Protocol) noti come protocolli extradom inio poiché vengono usati per regolare l’instradamento dei pacchetti tra host appartenenti ad Autonomous System diversi.

I principali EGP sono:
- EGP, Exterior Gateway Protocol, è stato il primo EGP a essere standardizzato, di sponibile su tutti i router, ormai è considerato un protocollo obsoleto;
- BGP, Border Gateway Protocol, definito in ambito IETF, è attualmente il protocol lo di tipo EGP usato su Internet, nella sua versione BGP-4;
- IDRP, Inter-Domain Routing Protocol, specificato da ISO, è della famiglia Path Vector come BGP.

---
[[Sistemi e reti(Internetworking).pdf#page=234&selection=56,4,56,47&color=yellow|II protocollo BGP (Border Gateway Protocol)]]

BGP (Border Gateway Protocol) è un protocollo di routing tra Autonomous System, attualmente utilizzato sul backbone di Internet ed è in pratica il succes sore del protocollo EGP.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=234&selection=70,0,71,64&color=yellow|BGP è un protocollo molto complesso, usato soprattutto su Internet dove diversi AS sono collegati attraverso gli Internet Service Provider (ISP)]]
> > BGP è un protocollo molto complesso, usato soprattutto su Internet dove diversi AS sono collegati attraverso gli Internet Service Provider (ISP)

II protocollo BGP costruisce un grafo di Autonomous System basato sulle informazioni che si scambiano i router in cui ciascun AS viene identificato con il suo AS Number (ASN). La connessione tra due AS si chiama path e una collezione di path forma a sua volta un path che viene utilizzato per raggiungere la destinazione

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=234&selection=82,0,88,17&color=yellow|BGP è un protocollo di tipo Path Vector, evoluzione del Distance Vector, dove nel vettore dei percorsi si elencano tutti gli AS da attraversare per raggiungere una destinazione.]]
> > BGP è un protocollo di tipo Path Vector, evoluzione del Distance Vector, dove nel vettore dei percorsi si elencano tutti gli AS da attraversare per raggiungere una destinazione.

Il Path Vector risolve il problema dei percorsi ciclici ed è più consono a definire le politiche di routing tra AS rispetto alla semplice distanza. I cicli vengono evitati poiché quando un router di frontiera di un AS riceve un Path Vector, controlla se il suo AS è già elencato al suo interno: • se lo è significa che esiste la possibilità di un loop e quel Path Vector non viene considerato; • altrimenti il Path Vector viene aggiornato con l’indicazione dell’AS di appartenen za e comunicato ai vicini, in quanto considerato corretto ([[Sistemi e reti(Internetworking).pdf#page=235&selection=179,1,183,0&color=yellow|figura 9]])

---
A ciascun Path Vector sono associati degli attributi che ne specificano la natura. Un determinato attributo può avere le seguenti caratteristiche: 
- well-known: riconoscibile da tutte le implementazioni BGP, deve essere inoltrato assieme al Path Vector (dopo un eventuale aggiornamento);
- mandatory: deve essere presente nel Path Vector;
- discretionary: può anche non essere indicato;
- optional: può non essere riconosciuto da alcuni router;
- transitive: deve essere inoltrato anche se non riconosciuto;
- non-transitive: deve essere ignorato se non riconosciuto; 
- partial: si tratta di un attributo optional-transitive che è stato ritrasmesso senza modifiche da un router perché non lo ha riconosciuto (indica se un determinato Path Vector è stato riconosciuto o meno da tutti i router attraversati)

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=236&selection=47,0,52,46&color=yellow|Quando un router annuncia un indirizzo di rete attraverso una sessione BGP, include anche alcuni attributi: in BGP si chiama route l'indirizzo di rete insieme ai suoi attributi.]]
> > Quando un router annuncia un indirizzo di rete attraverso una sessione BGP, include anche alcuni attributi: in BGP si chiama route l'indirizzo di rete insieme ai suoi attributi.

Gli attributi più significativi sono i seguenti:

- origin (Code = 1) è well-known mandatory e può valere:
	- 0 = IGP: l’informazione è stata ottenuta direttamente dal protocollo di routing ope rante all’interno dell’AS in cui si trova la destinazione e per cui la si ritiene veritiera;
	- 1 = EGP: l’informazione è stata appresa dal protocollo EGP, che non funziona se vi sono cicli (un percorso caratterizzato da questo valore è peggiore di uno di tipo IGP);
	- 2 = incomplete: serve a indicare che il percorso è stato determinato in altro mo do (per esempio statico) oppure è utilizzato per marcare un percorso di AS che è stato troncato perché la destinazione è al momento non raggiungibile;

- AS path (Code = 2) è well-known mandatory e consiste nell’elenco degli AS da at traversare lungo il percorso verso la destinazione;

- • next hop (Code = 3) è well-known mandatory e indica l’indirizzo IP del router di bordo dell’AS che deve essere usato come next hop verso la destinazione specificata.

La precedente Figura 9 mostra un esempio di Path Vector con attributi AS path e next hop. L'header dei messaggi BGP è lungo 19 ottetti: i primi 16 non sono usati e devono es sere messi tutti a 1; i successivi 2 ottetti indicano la lunghezza totale del messaggio e l'ultimo ottetto contiene il codice relativo al tipo di messaggio. 

I messaggi possono essere di 4 tipi:

- Open è il primo messaggio trasmesso quando viene attivata una connessione TCP verso un router BGP vicino, contiene:
	- informazioni di identificazione dell’AS di chi trasmette;
	- durata del timeout per considerare un vicino non più attivo;
	- dati di autenticazione;

- UpDate contiene il Path Vector e i relativi attributi;

- Notification è un messaggio di notifica di errori e/o di chiusura della connessione;

- KeepAlive è usato per comunicare a un router BGP vicino, in assenza di nuove informazioni di routing, che il trasmettitore è comunque attivo, anche se silente.

---
[[A, LE PORTE, LE SOCKET E I SERVIZI]]