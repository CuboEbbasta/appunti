Java è un linguaggio di programmazione (con sintassi ispirata da C) staticamente tipizzato (conosci il tipo in anticipo delle variabile) orientato agli oggetti creato nel 1995 dalla Sun Microsystem. Java inizialmente progettato per dispositivi elettronici come televisori poi diventato a uso generico.

  

Ps. primo linguaggio ad oggetti è stato “simula”.

  

---

  

Nel linguaggio orientato agli oggetti i problemi si modellano tramite l’interazione tra entità chiamate oggetti a differenza che di C dove si utilizza una sequenza finita di istruzioni.

Le classi sono l’insieme di dati statici(attributi) e comportamenti(metodi) che interagiscono con gli attributi. La classe non occupa ram a runtime poiché è solo l’idea di un oggetto.

  

Un oggetto è un'istanza di classe.

L’oggetto è composto da attributi e metodi.

Un oggetto visto che è un'entità concreta, occupa ram allocata sulla heap(parte della ram disordinata dove dati non necessariamente vicini).

  

Es.

Triangolo è un'idea di classe mentre un triangolo con determinati lati ed angoli è un oggetto

  

L’UML(Unified Modeling Language) è un tipo di modellazione standard per rappresentare le relazioni tra classi.(Utile per il lavoro in team)

  

---

  

I vantaggi principali di un linguaggio orientato agli oggetti sono:

-Facilità nella manutenzione del software

-Riutilizzabilità

-Espandibilità

  

---

  

I principi fondamentali della programmazione orientata agli oggetti sono:

  

Incapsulamento: Tecnica dove nascondiamo gli attributi di un oggetto.

Information Hiding: Principio dove definiamo i dettagli di implementazione(attributo fine alla classe)

Es. Nella media, la variabile “somma” è un dettaglio di implementazione.

Private, Public e Protected sono dei Qualificatori

  

Ereditarietà: Permette ad una classe(sottoclasse) di ereditare attributi o metodi da un’altra classe(superclasse)

  

Polimorfismo: Dove una classe(che può essere astratta ovvero composta da uno o più metodi astratti) consente a una stessa funzione di comportarsi in modo diverso in base all’implementazione della sotto classe.

Statico:metodo astratto(Overloading) Dinamico:Override

  

---

  

Associazioni tra classi:

  

Associazione statica(early binding): Una classe è contenuta in un altra classe (in tempo di compilazione)

Associazione dinamica(late binding): Scambio di messaggi che veicolano con i loro parametri la relazione tra classi (in tempo di esecuzione)

  

Dipendenza: Una classe A dipende da un’altra classe B se in una delle sue operazioni(classe A) ha dei parametri di una classe B

  

Generalizzazione: Altro termine per definire l’ereditarietà dove una classe più specifica eredità da una classe più generica

  

Composizione: Relazione Has-A(parte-tutto) dove un oggetto “parte” dipende dall’oggetto “tutto”. Se l’oggetto “tutto” viene distrutto anche l’oggetto ”parte” viene distrutto.

(relazione più forte rispetto ad Aggregazione)

  

Aggregazione: Relazione Is-A (simile alla Composizione) dove l’oggetto “parte” può esistere indipendente dall'oggetto “tutto”

  

---

Compilazione ed Esecuzione in Java:

  

Il codice sorgente(.Java) viene compilato(JavaC) in Bytecode(.Class).

  

Lexer(analizzatore lessicale): legge il codice e lo suddivide in unità minime chiamate token(parola chiave, identificatore, operatore, simbolo di punteggiatura)

es: int x = 10; (ogni cosa scritta è un identificatore)

  

Parser(analizzatore sintattico): prende i token fatti dal lexer e li organizza in una struttura gerarchica secondo le regole grammaticali del linguaggio, verifica che il codice sorgente sia sintatticamente corretto ed organizza il codice per le fasi successive.

es: int x = 10; controlla che int sia un dato valido, che x sia una variabile valida e che la sintassi sia scritta correttamente(output del lexer)

  

Abstract Syntax Tree (AST): rappresentazione ad albero della struttura del programma, serve per trasformazioni ed ottimizzazioni durante la compilazione(output dell’ parser)

L’AST viene tradotto in istruzioni comprensibili dalla JVM

  

Bytecode: fase finale della compilazione(output dell’ast)

  
  

Il Bytecode viene poi interpretato dalla JVM(Java Virtual Machine).

(La JVM sfrutta la tecnica  “Just In Time Compilation, JIT compilation” per eseguire il ByteCode)

(Il “JIT compiler” prende un pezzo di codice(una routine) e lo traduce nell’ “Instruction Set” ovvero le istruzioni della CPU)

La JVM rende java portabile tra piattaforme diverse implementando il concetto: Write once, Run everywhere 

  

Es. Non traduce Parola per Parola ma Frase per Frase e riutilizza la Frase nel caso ricapiti

  

---

  

JDK(Java Development Kit): Ambiente di sviluppo completo che include strumenti(JavaC, JavaDoc ovvero un generatore di documentazione, Jar è un file archiviato(.jar) che contiene il bytecode) e la JRE

  

JRE(Java Runtime Environment): Ambiente necessario per eseguire applicazioni Java già compilate e include la JVM

  

JVM(Java Virtual Machine):Componente che esegue il Bytecode(.class)

---

Static: Attributo comune a tutti gli oggetti di una classe

Static su un metodo: Metodo di una funzione quando una classe non è mai stata istanziata

  

Final:Attributo costante, che non cambia mai

Final su un metodo: Non può essere sovrascritto da altre classi

  

---

  

Costruttore di Copia: Quando un costruttore chiede in input un oggetto già esistente e ne copia lo stato.

  

---

  

ADT(Abstract Data Type): è un concetto ampio e teorico dove non importa come vengono svolte le operazione ma il risultato.

Es. Grande macchina a cui noi diamo input e riceviamo un output senza sapere come la svolge, Input 2 e 2, somma 4 ma non sai come viene fatta l’operazione

  

---

  

JAVABEAN: Una classe con delle convenzioni, con costruttore senza argomenti(default constructor) e attributi privati accessibili con Get e Set

  

---