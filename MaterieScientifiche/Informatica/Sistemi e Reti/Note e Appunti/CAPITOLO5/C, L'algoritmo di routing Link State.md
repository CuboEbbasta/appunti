L’algoritmo Link State supera la principale limitazione del Distance Vector cioè la mancata conoscenza della topologia della rete.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=217&selection=77,0,83,26&color=yellow|Ogni router ha una descrizione completa e diretta della topologia della rete poiché scambia le informazioni sulle distanze direttamente con tutti i router della rete e non solo coi vicini]]
> > Ogni router ha una descrizione completa e diretta della topologia della rete poiché scambia le informazioni sulle distanze direttamente con tutti i router della rete e non solo coi vicini

Questo avviene tramite l’invio di pacchetti, detti **LSP** (Link State Packet), da parte di ogni router a **tutti** gli altri router della rete. La trasmissione avviene in ==**flooding**, cioè un pacchetto viene inoltrato verso tutte le linee, tranne quella da cui è arrivato==. Il pacchetto LSP è solitamente inviato solo **quando avviene un cambiamento** nella rete (come guasti o aggiunta di nuovi nodi), anche se alcuni gestori ne prevedono l’invio periodicamente. Il pacchetto LSP contiene, per ogni mittente, l’elenco e la distanza da ogni vicino. Ogni router esamina ==il numero di sequenza del pacchetto in arrivo== e se risulta minore o uguale a quello memorizzato nel database, lo scarta. Se invece è maggiore lo memorizza e lo ritrasmette in flooding.

Tramite questi pacchetti, ogni router si costruisce un suo database con le informazioni sull’intera rete e, dopo aver ricevuto i pacchetti da tutti i router, è in grado di costruire un **==grafo pesato==** che rappresenta la rete stessa. A questo punto è possibile applicare un algoritmo per la ricerca dei cammini a costo minimo (il più noto è quel lo di **==Dijkstra==**).

Le caratteristiche del Link State si possono riassumere così:

- Dispone della mappa della rete;

- Ha una ==convergenza rapida== *(Tutti i router conoscono tutto)* poiché le informazioni si propagano velocemente sen za alcuna elaborazione intermedia (comunicazione diretta tra tutti i nodi e non attraverso informazioni di “seconda mano”);

- ==Difficilmente genera loop== e comunque è in grado di identificarli e interromperli facilmente;

- ==Tutti i nodi hanno basi di dati identiche==;

- ==È facilmente scalabile==, *può crescere* (all’aumentare del numero di router).

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=218&selection=49,0,51,71&color=yellow|Il principale svantaggio di un algoritmo Link State è la complessità di realizzazione, anche dovuta alla notevole capacità di memoria (il database di tutta la rete) e velocità di elaborazione (ricerca dei cammini a costo minimo) richiesti]]
> > Il principale ==svantaggio== di un algoritmo Link State è la complessità di realizzazione, anche dovuta alla notevole capacità di memoria (==il database di tutta la rete==) ==e velocità di elaborazione== (==ricerca dei cammini a costo minimo==) ==richiesti==.

[[Sistemi e reti(Internetworking).pdf#page=218&selection=57,0,58,1&color=yellow|TABELLA 2]]

