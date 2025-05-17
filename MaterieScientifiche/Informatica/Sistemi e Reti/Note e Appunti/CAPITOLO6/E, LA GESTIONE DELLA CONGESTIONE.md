
[[Sistemi e reti(Internetworking).pdf#page=293&selection=33,0,39,11&color=yellow|SLOW START E CONGESTION AVOIDANCE]]

Come detto in precedenza l’architettura di rete TCP/IP adotta il modello di comportamento Best Effort: la rete fa del suo meglio per consegnare i pacchetti e non rifiuta mai nuovi utenti (come avviene invece nella tradizionale rete telefonica). La conseguenza di questo comportamento è che possono verificarsi delle congestioni in rete: se la coda di ricezione del router è piena e non è più in grado di accettare nuovi pacchetti, questi verranno scartati.
Prima di gestire la congestione è necessario ==rilevarla== e a questo scopo TCP utilizza dei **timer** per misurare il tempo intercorso tra l’invio di un segmento e la ricezione del relativo ACK. Se quest’ultimo non arriva entro un dato tempo, si genera un timeout.

I problemi che possono aver causato la perdita dei dati (o dell’ACK) potrebbero avere varie origini, per esempio una tratta radio con elevato tasso di errore, ma TCP è nato per essere usato su reti fisse, ipotizza che la causa della perdita sia la congestione e agisce di conseguenza. Questa ipotesi, più che plausibile dal momento che le moderne reti hanno una bassissima probabilità di errori di trasmissione, è comune a molte versioni di TCP. Negli ultimi anni sono nate nuove versioni di TCP, che tengono conto anche della possibilità che la perdita dei dati possa essere causata da errori di trasmissione, quindi non intervengono diminuendo la quantità di dati inviati, ma cercano di mantenere alte le prestazioni.

La funzione TCP di gestione della congestione è particolarmente critica proprio perché si basa su deduzioni che avvengono agli end System (==si ricordi che TCP è un **protocollo end-to-end**==) ==e non su dati precisi prelevati in rete==. Non ci sono quindi garanzie che queste deduzioni siano sempre esatte. 
Negli anni sono stati proposti diversi algoritmi che si adattano alle varie situazioni ed effettuano deduzioni a partire da varie informazioni. Per esempio c’è chi deduce la perdita di un segmento dallo scadere di un timer, altri al timeout aggiungono an che la ricezione di ACK duplicati e così via.
TCP lavora applicando congiuntamente diversi algoritmi e configurandone i parame tri da usare. Esistono perciò diverse implementazioni del protocollo, che differiscono in base alle opzioni scelte.
L’RFC 5681 specifica 4 algoritmi che cooperano tra loro per realizzare il controllo della congestione.

==Tutti questi algoritmi fanno uso di una nuova variabile: la **finestra di congestione** che viene utilizzata dal mittente per ogni connessione attiva e serve per avere un’indicazione sul massimo numero di byte non riscontrati che si possono trovare ancora nella rete.==
In particolare vale quanto segue: 

*maxWindow = **min**(FinestraDiCongestione, FinestraDiRicezione)*

dove:
- **FinestraDiCongestione** (**congestion window**): è il massimo numero di byte che la rete è in grado di trasmettere senza che si verifichino dei timeout che segnala no la perdita di dati; *(variano durante la connessione)*
- **FinestraDiRicezione** (**advertised window**): indica quanti byte il destinatario è in grado di ricevere; *(variano durante la connessione)*
- **maxWindow**: quando un host deve inviare dei dati prenderà come numero mas simo di byte che può trasmettere il minimo tra i due valori delle finestre

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=294&selection=19,0,28,44&color=yellow|L’idea alla base di questi algoritmi è diminuire la finestra di congestione quando un pacchetto è scartato dalla rete e aumentarla quando un pacchetto è riscontra to. Infatti se si sono persi pacchetti a causa della congestione, essi dovranno essere ritrasmessi, aumentando così il traffico in una rete che ne ha già troppo. Quindi perché la rete non collassi è importante che il mittente sia drastico nel ridurre il traffico che genera e cauto nell’aumentarlo.]]
> > L’idea alla base di questi algoritmi è ==diminuire la finestra di congestione quando un pacchetto è scartato dalla rete e aumentarla quando un pacchetto è riscontrato== *(ACK di conferma)*. Infatti se si sono persi pacchetti a causa della congestione, essi dovranno essere ritrasmessi, aumentando così il traffico in una rete che ne ha già troppo. ==Quindi perché la rete non collassi è importante che il mittente sia drastico nel ridurre il traffico che genera e cauto nell’aumentarlo==.

Dei 4 algoritmi descritti nelle specifiche, nel seguito si prendono in esame ==**slow start**== e **==congestion avoidance==**, che vengono usati solitamente insieme in molte implementazioni di TCP, prima fra tutte quella di Berkeley da cui deriva il nome TCP Berkeley dato alle versioni che implementano i due algoritmi. Si inzia a trasmettere lentamente, esplorando la rete, per poi accelerare, prima in modo esponenziale, poi lineare, finché non c’è una perdita di dati che comporta un rallentamento nell’invio di nuovi byte.

I punti seguenti spiegano come lavorano i due algoritmi, iniziando con **slow start**:
- al momento della creazione della connessione TCP tra due host, il mittente imposta la finestra di congestione alla massima quantità di byte che la rete può spedire;
- ogni volta che viene inviato un segmento TCP, e ricevuto PACK di conferma ricezione da parte del destinatario, il valore della finestra di congestione viene raddoppiato. Avviene in questo modo una crescita esponenziale del numero di byte che possono essere inviati in rete, fino al raggiungimento di una certa soglia (**threshold**) che viene consigliato di impostare inizialmente a 64 KB; 
- da questo punto in poi la dimensione della finestra di congestione è regolata dall’algoritmo **congestion avoidance** che effettua incrementi di tipo lineare, infatti viene di volta in volta sommato il valore assegnato inizialmente alla fine stra di congestione;
- quando si genera un timeout (che per questa versione di TCP significa congestione), si effettuano le seguenti operazioni:
	- la soglia viene impostata alla metà del valore della finestra di congestione che ha generato il timeout;
	- la finestra di congestione viene riportata al suo valore iniziale.

Nella [[Sistemi e reti(Internetworking).pdf#page=295&selection=25,2,27,3&color=yellow|FIGURA 15]] è mostrato il grafico dell'andamento della dimensione della finestra di congestione. 

---
[[F, L'HANDSHAKING TCP]]