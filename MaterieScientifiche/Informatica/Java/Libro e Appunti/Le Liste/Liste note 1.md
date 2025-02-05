### Implementazione della Classe `Lista`

```java
public class Lista {
    // Classe interna Nodo
    private class Nodo {
        private String valore;
        private Nodo next;

        public Nodo(String valore) {
            this.valore = valore;
            this.next = null;
        }

        public String getValore() {
            return valore;
        }

        public void setValore(String valore) {
            this.valore = valore;
        }

        public Nodo getNext() {
            return next;
        }

        public void setNext(Nodo next) {
            this.next = next;
        }
    }

    private Nodo head; // Primo elemento della lista

    public Lista() {
        this.head = null;
    }

    // Aggiungi un elemento in coda
    public void aggiungi(String valore) {
        Nodo nuovoNodo = new Nodo(valore);
        if (head == null) {
            head = nuovoNodo;
        } else {
            Nodo corrente = head;
            while (corrente.getNext() != null) {
                corrente = corrente.getNext();
            }
            corrente.setNext(nuovoNodo);
        }
    }

    // Rimuovi il primo elemento
    public String rimuoviPrimo() {
        if (head == null) {
            throw new IllegalStateException("Lista vuota.");
        }
        String valore = head.getValore();
        head = head.getNext();
        return valore;
    }

    // Ottieni un iteratore per scorrere la lista
    public Iteratore getIteratore() {
        return new Iteratore(head);
    }

    // Classe interna Iteratore
    public class Iteratore {
        private Nodo corrente;

        protected Iteratore(Nodo inizio) {
            this.corrente = inizio;
        }

        public boolean hasNext() {
            return corrente != null;
        }

        public String next() {
            if (!hasNext()) {
                throw new IllegalStateException("Nessun elemento successivo.");
            }
            String valore = corrente.getValore();
            corrente = corrente.getNext();
            return valore;
        }
    }
}
```

---

### **Esempio di Verifica nel `main`**

```java
public class Main {
    public static void main(String[] args) {
        Lista lista = new Lista();

        // Aggiunta di elementi alla lista
        lista.aggiungi("A");
        lista.aggiungi("B");
        lista.aggiungi("C");

        // Uso dell'iteratore per scorrere la lista
        Lista.Iteratore iteratore = lista.getIteratore();
        System.out.println("Elementi della lista:");
        while (iteratore.hasNext()) {
            System.out.println(iteratore.next());
        }

        // Rimuovi il primo elemento
        System.out.println("Rimosso: " + lista.rimuoviPrimo());

        // Verifica dopo la rimozione
        iteratore = lista.getIteratore();
        System.out.println("Elementi della lista dopo rimozione:");
        while (iteratore.hasNext()) {
            System.out.println(iteratore.next());
        }
    }
}
```

---

### **Output Esempio**

```
Elementi della lista:
A
B
C
Rimosso: A
Elementi della lista dopo rimozione:
B
C
```

### **Dettagli Importanti**

1. **Classe `Nodo`:** Contiene i metodi `set` e `get` per accedere ai dati e al riferimento al nodo successivo.
2. **Classe `Iteratore`:** Ha un costruttore `protected` che accetta il nodo iniziale, oltre ai metodi `hasNext` e `next`.
3. **Struttura Modularizzata:** Tutto è incluso nella classe `Lista`, e l'iteratore è progettato appositamente per funzionare con essa.

Puoi usare questa implementazione per gestire facilmente una lista di stringhe e iterare attraverso i suoi elementi.