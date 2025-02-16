Lo scopo di un protocollo di routing è quello di aggiornare dinam icam ente le routing table. Per fare ciò, i router devono quindi condividere le informazioni sui percorsi (route) che ciascuno conosce. Questo scambio di dati è compiuto mediante pacchetti speciali chiamati **routing update**. Prima di entrare nel dettaglio vediamo quali sono gli scopi che un routing protocol si deve prefiggere:
- **Ottimalità**: deve essere in grado di fornire il percorso migliore o più veloce lungo l’Internetwork individuando percorsi alternativi, ciascuno con una velocità o livel lo di traffico diverso. Per esempio, un protocollo userà la banda e il conteggio dei salti (hop count), mentre un altro darà un peso maggiore alla banda;
- **Imparzialità**: deve utilizzare tutte le linee disponibili per distribuire il traffico evitando le congestioni (occorre mediare tra ottimalità e imparzialità, spesso in conflitto);
- **Flessibilità**: deve garantire capacità di adattarsi ai cambiamenti della topologia di rete;
- **Convergenza veloce**: deve far sì che i cambiamenti all’interno dell’Internetwork si propaghino verso tutti i router nel minor tempo possibile;
- **Robustezza**: deve essere in grado di funzionare anche nel caso di configurazioni non corrette e guasti di componenti;
- **Semplicità**: deve essere semplice ed efficiente.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=213&selection=83,0,90,73&color=yellow|Sistemi e reti(Internetworking), p.213]]
> > La gran parte dei protocolli che regolano il routing moderno utilizzano uno dei due seguenti algoritmi: Distance Vector Routing 
> > Link State Routing
> > Gli algoritmi di routing calcolano il percorso migliore o a costo minimo.
> > 
> 

---
[[Sistemi e reti(Internetworking).pdf#page=213&selection=92,4,92,42&color=yellow|L'algoritmo di routing Distance Vector]]

L’algoritmo Distance Vector si basa sull’algoritmo **Bellman-Ford** per calcolare il per corso migliore. Crea una tabella di routing costituita essenzialmente da due colonne: una contenente la **distanza** (il costo) stimata per raggiungere ogni nodo della rete e una che specifica l’**interfaccia** (la linea) da utilizzare. La distanza può essere calcolata secondo metriche diverse in base al protocollo in uso. Le righe della tabella saranno invece tante quanti sono i nodi della rete. Essendo un algoritmo dinamico, le tabelle vengono aggiornate a intervalli di tempo prestabiliti. Inizialmente ogni router invia ai router vicini (**neighbour**) un pacchetto di **ECHO** per calcolare la distanza che lo separa da ciascuno di essi e inserisce il valore nella tabella. Subito dopo i router vicini si scambiano un **vettore delle distanze**, cioè un array contenente le informazioni che ciascun router ha a disposizione riguardo i costi per raggiungere le varie destinazioni. A quel punto, ricevuti i vettori dai vicini, ciascun router aggiorna la propria tabella mediante un confronto tra i costi risultanti dalla
propria tabella e quelli ricevuti, modificando i valori laddove risultino inferiori e ag giornando le relative interfacce (linee d'uscita).
- [[Sistemi e reti(Internetworking).pdf#page=214&selection=9,0,9,9&color=yellow|esercizio 1]]
- [[Sistemi e reti(Internetworking).pdf#page=215&selection=89,0,89,9&color=yellow|esercizio 2]]
---
[[Sistemi e reti(Internetworking).pdf#page=216&selection=273,0,281,6&color=yellow|I PRINCIPALI PROBLEMI DEL DISTANCE VECTOR]]

I due principali problemi che possono presentarsi con il Distance Vector sono:
- **Routing loop**: si verifica quando un pacchetto è inoltrato su un percorso circola re senza mai giungere a destinazione; in questi casi il problema si risolve grazie al contatore T T L (Time To Live) il cui valore si riduce a ogni hop e quando arriva a 0 il pacchetto viene scartato;
- **Count to infinity**: si verifica quando il costo per il raggiungimento di una desti nazione viene progressivamente incrementato (normalmente avviene quando una destinazione non è più raggiungibile per via di un guasto di cui il mittente non è a conoscenza); in questi casi è il percorso che finisce con l’essere scartato visti i co sti sempre crescenti.

Entrambi i problemi sono legati al fatto che il Distance Vector **non conosce la topologia della rete** e che la convergenza della rete (cioè la propagazione delle informa zioni) può richiedere molto tempo.

