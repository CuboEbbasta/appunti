Nei primi anni Ottanta, Internet era considerata come una single network cioè un’unica rete in cui tutti i router dovevano predisporre una routing table contenente una voce per ogni rete raggiungibile e l’indirizzo del router attraverso cui raggiungere la (neighbour router). ==L’introduzione di algoritmi e protocolli che permettessero ai router di adattarsi dinamicamente al mutare della topologia non risolveva il problema della crescita delle tabelle di routing==.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=219&selection=38,0,47,35&color=yellow|Internet è stata suddivisa in un certo numero di aree denominate Autonomous System (AS), ognuna gestita da un network provider (o da un gruppo di amministratori). Un AS è costituito da un insieme di router e LAN raggruppati secondo criteri topologici e organizzativi, che assicurano che i router all’interno di ogni AS siano reciprocamente raggiungibili.]]
> > Internet è stata suddivisa in un certo numero di aree denominate **==Autonomous System==** (**==AS==**), ognuna gestita da un network provider (o da un gruppo di amministratori). ==**Un AS è costituito da un insieme di router e LAN** raggruppati secondo criteri topologici e organizzativi==, ==che assicurano che i router all’interno di ogni AS siano reciprocamente raggiungibili==.

La [[Sistemi e reti(Internetworking).pdf#page=219&selection=49,0,50,1&color=yellow|FIGURA 2]] mostra la comunicazione all’interno di un AS e tra AS diversi:

- le informazioni di raggiungibilità all’interno di un AS sono scambiate mediante uno o più protocolli adattivi detti **Interior Protocol**; 
- gli AS si scambiano informazioni sulla rispettiva raggiungibilità utilizzando un protocollo opportuno genericamente designato come **Exterior Protocol**.

Se un router deve instradare un messaggio a un altro router appartenente allo stesso AS (in questo caso si parla di comunicazione tra **Interior Router, IR**), avrà nella propria tabella di routing l’informazione di raggiungibilità idonea. Se al contrario è necessario raggiungere un router che appartiene a un differente AS, il messaggio viene inviato attraverso una coppia di router particolari detti **Exterior Router** (**ER**), almeno uno per ogni AS. Ciascun ER conosce le reti raggiungibili utilizzando i link che lo collegano agli altri ER, ma non conosce il modo in cui queste reti sono di fatto connesse all’interno dei rispettivi AS.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=219&selection=97,0,100,8&color=yellow|Gli Exterior Router di un AS hanno vi sibilità su tutte le destinazioni all’inter no dell’AS e sugli Exterior Router degli altri AS]]
> > Gli Exterior Router di un AS hanno visibilità su tutte le destinazioni all’inter no dell’AS e sugli Exterior Router degli altri AS.

Ciascun AS è gestito indipendentemente dagli altri, in particolare per quanto riguar da l’instradamento dei pacchetti IP al suo interno. Gli accordi, amministrativi e tecnici, ==tra i gestori di AS differenti per stabilire le politiche di transito e raggiungibilità==, ==sono detti accordi di **peering**==.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=220&selection=14,0,15,31&color=yellow|Una relazione di peering si stabilisce tutte le volte che un Exterior Protocol viene attivato tra due AS differenti.]]
> > Una relazione di peering si stabilisce tutte le volte che un Exterior Protocol viene attivato tra due AS differenti.


