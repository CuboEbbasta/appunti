Le **liste** sono strutture dati utilizzate per memorizzare sequenze di elementi in modo ordinato. Una **lista collegata** (o semplicemente **lista**) è una struttura dati in cui ogni elemento è un "nodo" che contiene due parti:

1. **Il dato** (o informazione) che l'elemento contiene.
2. **Il riferimento al nodo successivo** (in una lista semplicemente collegata), che è un "link" al prossimo nodo della lista. In una lista doppiamente collegata, ci sono anche riferimenti al nodo precedente.

### Struttura di un Nodo

Ogni nodo della lista contiene almeno due componenti:

- **dato**: il valore memorizzato nel nodo (ad esempio, un numero, una stringa, un oggetto, ecc.).
- **next**: un riferimento al prossimo nodo nella lista. Se il nodo è l'ultimo della lista, il riferimento sarà `null`.

Ecco un esempio di definizione di una classe `Nodo` in Java:

```java
class Nodo {
    int dato;      // Dato che il nodo memorizza
    Nodo next;     // Riferimento al prossimo nodo

    Nodo(int dato) {
        this.dato = dato;
        this.next = null;
    }
}
```

### La Lista Collegata

Una lista collegata è composta da una serie di nodi connessi tra loro. Per manipolare la lista, devi mantenere un riferimento al **primo nodo** della lista, chiamato **testa**.

Ecco una semplice implementazione della classe `Lista`:

```java
class Lista {
    Nodo testa;  // Riferimento al primo nodo della lista

    // Costruttore della lista
    public Lista() {
        testa = null;  // All'inizio la lista è vuota
    }

    // Metodo per aggiungere un nodo alla fine della lista
    public void aggiungi(int valore) {
        Nodo nuovoNodo = new Nodo(valore);  // Crea un nuovo nodo
        if (testa == null) {
            testa = nuovoNodo;  // Se la lista è vuota, il nuovo nodo diventa la testa
        } else {
            Nodo corrente = testa;
            while (corrente.next != null) {
                corrente = corrente.next;  // Scorri fino all'ultimo nodo
            }
            corrente.next = nuovoNodo;  // Collega il nuovo nodo all'ultimo nodo
        }
    }

    // Metodo per rimuovere il primo nodo con un dato valore
    public void rimuovi(int valore) {
        if (testa == null) return;  // La lista è vuota, quindi non si può rimuovere nulla
        if (testa.dato == valore) {
            testa = testa.next;  // Se il nodo da rimuovere è il primo, aggiorna la testa
            return;
        }
        Nodo corrente = testa;
        while (corrente.next != null && corrente.next.dato != valore) {
            corrente = corrente.next;  // Trova il nodo precedente a quello da rimuovere
        }
        if (corrente.next != null) {
            corrente.next = corrente.next.next;  // Rimuove il nodo
        }
    }

    // Metodo per visualizzare tutta la lista
    public void visualizza() {
        Nodo corrente = testa;
        while (corrente != null) {
            System.out.print(corrente.dato + " ");  // Stampa il dato del nodo corrente
            corrente = corrente.next;  // Passa al nodo successivo
        }
        System.out.println();
    }
}
```

### Aggiungere, Rimuovere e Visualizzare

1. **Aggiungere un elemento**: Per aggiungere un elemento alla lista, bisogna creare un nuovo nodo e collegarlo alla lista. Se la lista è vuota, il nuovo nodo diventa il primo nodo; altrimenti, viene aggiunto alla fine.
    
2. **Rimuovere un elemento**: Per rimuovere un nodo con un dato valore, si percorre la lista fino a trovare il nodo da rimuovere, poi si aggiorna il nodo precedente per "saltare" quello da rimuovere.
    
3. **Visualizzare la lista**: Per visualizzare tutti gli elementi, si percorre la lista partendo dalla testa e si stampa ogni dato contenuto in ogni nodo.
    

### Esempio di Utilizzo

Ecco come potrebbe apparire un semplice programma che usa la classe `Lista`:

```java
public class Main {
    public static void main(String[] args) {
        Lista lista = new Lista();

        // Aggiungi elementi
        lista.aggiungi(10);
        lista.aggiungi(20);
        lista.aggiungi(30);
        lista.aggiungi(40);

        // Visualizza la lista
        lista.visualizza();  // Output: 10 20 30 40

        // Rimuovi un elemento
        lista.rimuovi(20);
        lista.visualizza();  // Output: 10 30 40

        // Rimuovi un altro elemento
        lista.rimuovi(10);
        lista.visualizza();  // Output: 30 40
    }
}
```

### Considerazioni

- Le liste collegate sono utili quando bisogna aggiungere o rimuovere elementi frequentemente da posizioni diverse (in particolare dalla testa o dalla coda) senza dover ridimensionare o spostare gli altri elementi, come invece accade con gli array o gli `ArrayList`.
- Un'altra variante delle liste collegate è la **lista doppiamente collegata**, in cui ogni nodo contiene anche un riferimento al nodo precedente, permettendo un'operazione di scorrimento bidirezionale.

---
[[Metodi per List in java]]
[[Liste note 1]]