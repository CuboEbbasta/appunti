Nelle precedenti Unità sono stati descritti i livelli inferiori dello stack TCP/IP, che si occupano della comunicazione host-nodo e nodo-nodo. Grazie all’organizzazione a livelli, i protocolli del livello di trasporto (Transport Layer) non necessitano di conoscere i dettagli della rete che utilizzano.
In particolare, si è visto l’importante ruolo del protocollo IP nel trasferire i datagram attraverso Internet. Una volta arrivato a destinazione, però, l’header del datagram IP non contiene alcuna informazione utile all’host ricevente per individuare l’applicazione destinataria del messaggio.

Infatti i protocolli del livello Network svolgono la funzione di far attraversare la re te al pacchetto per poi consegnarlo al sistema di destinazione; a questo punto il loro compito è finito. Poiché su un host ci possono essere più applicazioni aperte contemporaneamente che generano un **processo** di richiesta o anche più di uno, si pone il problema per l’host destinatario di sapere a quale processo attivo (di sistema o utente) consegnare il pacchetto ricevuto.

PROCESSO: Un processo è una sequenza di attività (task) generata da un programma applicativo utente o di sistema, eseguito su un processore sotto la gestione del rispettivo Sistema Operativo.

Il problema di consegnare il messaggio all’applicazione finale potrebbe essere risolto semplicemente individuando il processo relativo a quella applicazione, ma la questione è tutt’altro che semplice. Infatti i processi vengono creati ed eliminati dinamicamente, non possono quindi essere noti ai potenziali mittenti che si trovano in Internet. Per esempio, un host mittente deve poter richiedere una pagina web che risiede su un computer server di cui conosce l'indirizzo, senza dover sapere qual è il processo che implementa la funzione di web server. Non solo, uno stesso processo potrebbe gestire più funzionalità, ma una sola è quella destinataria del messaggio.

---
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=275&selection=105,0,130,65&color=yellow|Le applicazioni finali devono allora poter essere individuate non in base al processo che le esegue, bensì alle funzioni che richiedono (client) o che svolgono (server). Occorre quindi trovare un sistema che consenta di individuare in modo univoco ogni comunicazione in rete in base alla sua funzione (web server, mail server, co municazione tra App, accesso a social network,...). Sulla base di questo approccio, il primo passo è stato stabilire che in ogni host siano definiti dei punti di acces so, chiamati porte (ports), che vengono associati al processo che sta svolgendo in quel momento la funzione richiesta e al protocollo utilizzato. Solo alla porta pre disposta verranno consegnati i pacchetti che arrivano dalla rete.]]
> > Le applicazioni finali devono allora poter essere individuate non in base al processo che le esegue, bensì alle funzioni che richiedono (client) o che svolgono (server). Occorre quindi trovare un sistema che consenta di individuare in modo univoco ogni comunicazione in rete in base alla sua funzione (web server, mail server, comunicazione tra App, accesso a social network,...). Sulla base di questo approccio, il primo passo è stato stabilire che in ogni host siano definiti dei **punti di accesso**, **chiamati porte** (ports), che vengono **associati al processo** che sta svolgendo in quel momento la funzione richiesta e al protocollo utilizzato. Solo alla porta pre disposta verranno consegnati i pacchetti che arrivano dalla rete.

Ogni porta viene identificata da un numero intero positivo codificato in 16 bit (range: 0 - 65.535).

I **numeri di porta** sono assegnati a livello internazionale da IANA e suddivisi in tre gruppi:
- Well Known Ports (da 0 a 1.023);
- Registered Ports (da 1.024 a 49.151); 
- Dynamic and/or Private Ports (da 49.152 a 65.535).

---
> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=276&selection=42,0,45,34&color=yellow|L’host client e Thost server, oltre al reciproco indirizzo IP, devono conoscere i rispettivi numeri di porta utilizzati dall’applicazione che ha generato il processo re lativo a una determinata funzione.]]
> > L’host client e l'host server, oltre al reciproco indirizzo IP, devono conoscere i rispettivi numeri di porta utilizzati dall’applicazione che ha generato il processo relativo a una determinata funzione.

Tali porte sono dette: 
- **source port**: numero della porta presente sull’host client, sulla quale il processo client è in attesa di risposta dal server (è un’informazione utilizzata dal server);
- **destination port**: numero della porta su cui il processo server è in ascolto o su cui fornisce il servizio (è un’informazione utilizzata dal client).

Nella [[Sistemi e reti(Internetworking).pdf#page=276&selection=78,0,80,1&color=yellow|FIGURA 1]] si mostra un esempio di utilizzo delle porte nel caso di un’applicazione di trasferimento file con FTP (File Transfert Protocol), protocollo del livello applica zione che affronteremo nell’Unità 8.

---
[[Sistemi e reti(Internetworking).pdf#page=277&selection=42,0,42,9&color=yellow|LE SOCKET]]

Come abbiamo detto le porte sono il primo passo per stabilire un canale bidirezionale univocamente individuabile tra processo client e processo server relativamente a una funzione.
Un client che si rivolge a un server, in ascolto su una propria porta, dovrà innanzitutto fare una richiesta di connessione al servizio comunicando il proprio indirizzo IP e la porta su cui vuole ricevere la risposta. Il server, dopo un’eventuale fase di impostazione utile al trasferimento successivo delle informazioni, stabilirà la connessione comunicando a sua volta il proprio indirizzo IP e la porta su cui avverrà la comunicazione, diversa da quella su cui era in ascolto ([[Sistemi e reti(Internetworking).pdf#page=277&selection=12,0,14,0&color=yellow|FIGURA 2]]).

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=277&selection=64,0,100,89&color=yellow|Un pacchetto che viaggia nella rete deve quindi contenere 4 informazioni fondamentali: (Client IP address, Server IP address, Client Port number, Server Port number) Specificando anche il protocollo per la comunicazione si riesce a descrivere univo camente la connessione con una quintupla detta Association: (protocollo, ind. logico locale, porta locale, ind. logico remoto, porta remota) esempio: (TCP, 200.18.6.12, 3000, 58.163.138.10, 4000) La quintupla viene in realtà costituita a partire da due elementi simmetrici, un’as sociazione locale e una remota: • protocollo, ind. logico locale, porta locale (TCP, 200.18.6.12,3000); • protocollo, ind. logico remoto, porta remota (TCP, 58.163.138.10,4000). Ciascuna di queste parti è una socket su un host diverso. A ogni processo che richiede o risponde a una comunicazione in rete viene assegnata una socket che ha il compito di interfacciare l’applicazione client che ha generato il processo (di richiesta) con l’applicazione server che fornisce il servizio (in risposta).]]
> > Un pacchetto che viaggia nella rete deve quindi contenere 4 informazioni fondamentali: (**Client IP address**, **Server IP address**, **Client Port number**, **Server Port number**) Specificando anche il protocollo per la comunicazione si riesce a descrivere univocamente la connessione con una **quintupla** detta **Association**: (**protocollo**, **ind. logico locale**, **porta locale**, **ind. logico remoto**, **porta remota**) esempio: (TCP, 200.18.6.12, 3000, 58.163.138.10, 4000) La quintupla viene in realtà costituita a partire da due elementi simmetrici, un’as sociazione locale e una remota: 
> > 	- protocollo, ind. logico locale, porta locale (TCP, 200.18.6.12,3000); (client)
> > 	- protocollo, ind. logico remoto, porta remota (TCP, 58.163.138.10,4000).
> > Ciascuna di queste parti è una socket su un host diverso. A ogni processo che richiede o risponde a una comunicazione in rete viene assegnata una socket che ha il compito di interfacciare l’applicazione client che ha generato il processo (di richiesta) con l’applicazione server che fornisce il servizio (in risposta).

---
Agli inizi degli anni Ottanta, l' ARPA con l’Università di Berkeley creò un’interfac cia per far comunicare applicazioni che girano su macchine UNIX connesse in rete. Fu deciso anche di adoperare il sistema di **chiamate a funzioni** esistente in UNIX e di aggiungere un nuovo sistema di chiamate con apposite **primitive** per supportare le funzioni TCP/IP ([[Sistemi e reti(Internetworking).pdf#page=278&selection=89,0,89,9&color=yellow|TABELLA 1]]). Il risultato fu una interfaccia socket BSD (Berkeley Software Distribution) UNIX.

PRIMITIVA: Con primitiva si intende una **chiamata di sistema a una routine del kernel**.

---
Nel 1991 Microsoft decise di definire una **API** (Application Program Interface) standard per applicazioni TCP/IP in ambiente Windows ([[Sistemi e reti(Internetworking).pdf#page=278&selection=177,0,177,7&color=yellow|FIGURA 3]]) che permette di semplificare il dialogo tra applicazioni residenti su host diversi.

API: Con API si indica un **insieme di procedure** (in genere raggruppate per strumenti specifici) **predisposte all'espletamento di un dato compito**; **spesso tale termine designa le librerie software di un linguaggio di programmazione**. Le API sono quindi un'interfaccia per programmatori.

Ogni linguaggio di programmazione, che sia di alto o basso livello, deve fornire delle API che permettano di lavorare con le Socket. In pratica le API permettono agli sviluppatori software di accedere a determinate funzioni, altrimenti inaccessibili, di un programma o servizio web in modo da creare un nuovo utilizzo. Tantissimi servizi Internet hanno ormai le loro librerie API e le forniscono in maniera open. Per esempio Facebook, Google Maps o Twitter hanno le loro e sono utilizzate per tantissimi altri servizi o da innumerevoli altri siti.

---
[[Sistemi e reti(Internetworking).pdf#page=279&selection=69,4,69,13&color=yellow|I SERVIZI]]

I protocolli implementati a livello Transport svolgono funzioni simili a quelli del livello Data Link, per esempio si occupano del controllo degli errori, della sequenza corretta dei dati, del controllo di flusso, ecc. La differenza fondamentale tra i due tipi di protocollo è lo scenario di rete in cui operano: a livello Data Link la connessione tra il router che invia il pacchetto a un altro router è diretta, infatti i due router comunicano attraverso un canale fisico di trasmissione; a livello Transport invece la connessione avviene attraverso l'intera rete, si tratta di un canale logico di trasmissione che unisce il computer host mittente con il computer host destinatario.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=279&selection=90,0,97,54&color=yellow|Per questo motivo si dice che il livello Transport si occupa della comunicazione end-to-end, dove i due estremi della connessione sono gli host che vogliono co municare o più precisamente le Socket predisposte sui due host.]]
> > Per questo motivo si dice che il livello Transport si occupa della comunicazione end-to-end, dove i due estremi della connessione sono gli host che vogliono comunicare o più precisamente le Socket predisposte sui due host. ([[Sistemi e reti(Internetworking).pdf#page=279&selection=99,0,100,30&color=yellow|FIGURA 4]])

Il livello Transport svolge quindi una funzione “cuscinetto” tra il livello Application e i livelli inferiori, che si occupano della trasmissione in rete dei dati. In questo modo le applicazioni non necessitano di conoscere i dettagli operativi e organizzativi della rete che utilizzano, non interessa loro sapere il tipo di computer di destinazione, il percorso che faranno i dati, quanto è grande la rete che utilizzano o quale mezzo trasmissivo verrà usato. Analogamente, anche i livelli inferiori non sono a conoscenza che esistono molte applicazioni che inviano dati in rete, loro hanno solo il compito di consegnare i messaggi a destinazione. Nella [[Sistemi e reti(Internetworking).pdf#page=280&selection=31,0,31,8&color=yellow|FIGURA 5]] viene evidenziato il ruolo del livello Transport nella comunicazione tra applicazioni differenti, installate su diverse tipologie di dispositivi (device)

---
Esistono vari protocolli di trasporto che sono stati standardizzati per soddisfare le differenti esigenze delle diverse applicazioni. Nel seguito si esamineranno i due pro tocolli di trasporto più diffusi: **UDP** e **TCP**.
UDP e TCP sono anche stati tra i primi a essere standardizzati. In generale il livel lo Transport non offre servizi di tipo reai time (come lo streaming audio-video) né una banda garantita. Vi sono però dei protocolli sviluppati dalla IETF che svolgono le funzioni del livello di trasporto (come TCP o UDP) appoggiandosi a un servizio di rete a pacchetto come IP. Tra i più recenti c’è per esempio **SCTP** (**Stream Control Transmission Protocol**) sviluppato nel 2000 per supportare la telefonia su reti IP e il cui uso si è poi allargato alle applicazioni **multistreaming** e **multihoming**. SCTP combina diverse caratteristiche dei protocolli TCP e UDP, anch’essi utilizza ti per il trasferimento dati, e include meccanismi per il controllo di congestione e il miglioramento della tolleranza ai guasti durante l’invio di pacchetti. Grazie alla sua elevata flessibilità, l’SCTP è utilizzato anche in altri modi (per esempio nella gestio ne e nell’amministrazione di pool di server). Nei documenti RFC di IETF, che descrivono i protocolli UDP e TCP, la Transport Protocol Data Unit (TPDU) è indicata con nomi differenti: datagram in UDP e segment in TCP.ù

MULTISTREAMING: Flussi indipendenti all'interno della stessa association. (A livello Application si hanno più indirizzi IP)

MULTIHOMING: Con multihoming si intende la **possibilità di avere più indirizzi di rete in un computer**, di solito per interfacciare reti diverse. 

---
I protocolli del livello Transport mettono in comunicazione le applicazioni, o meglio i processi, presenti su due host remoti offrendo un servizio denominato **multiplexing**/**demultiplexing** (descritto nella Lezione 4), insieme al controllo dell’integrità dei dati. Inoltre, un protocollo come TCP fornisce anche la garanzia di consegna dei dati, ef fettuando il controllo della congestione (descritta nella Lezione 5) e il controllo di flusso (sliding Windows).
La [[Sistemi e reti(Internetworking).pdf#page=281&selection=25,0,28,0&color=yellow|FIGURA 6]] mostra i servizi offerti dal livello Transport alle applicazioni.

---
[[B, LE FUNZIONALITÀ DI MULTIPLEXING E DEMULTIPLEXING]]
