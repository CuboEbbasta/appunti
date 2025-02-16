
## **1. Classi anonime**

Le **classi anonime** sono classi che non hanno un nome e vengono dichiarate ed istanziate contemporaneamente. Vengono utilizzate soprattutto quando è necessario estendere una classe o implementare un’interfaccia senza dover creare una nuova classe separata.

### **Sintassi di base**

```java
// Esempio con interfaccia
interface Saluto {
    void saluta();
}

public class Main {
    public static void main(String[] args) {
        // Dichiarazione e implementazione di una classe anonima
        Saluto s = new Saluto() {
            @Override
            public void saluta() {
                System.out.println("Ciao, sono una classe anonima!");
            }
        };

        s.saluta();
    }
}
```

### **Quando usare le classi anonime?**

- Quando si deve creare un'istanza di una classe con un comportamento specifico solo in un punto del codice.
- Per implementare rapidamente un'interfaccia o estendere una classe senza dichiarare una classe separata.

---

## **2. Inner Class (Classi interne)**

Le **inner class** sono classi dichiarate all'interno di un'altra classe. Possono accedere ai membri della classe esterna e vengono usate per modellare una stretta relazione tra due classi.

### **Tipologie di classi interne**

1. **Classe interna non statica**
    
    - Ha accesso ai membri della classe esterna (anche privati).
    - Deve essere istanziata attraverso un'istanza della classe esterna.
    
    ```java
    class Esterna {
        private String messaggio = "Ciao dal mondo esterno!";
        
        class Interna {
            void stampa() {
                System.out.println(messaggio);
            }
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Esterna e = new Esterna();
            Esterna.Interna i = e.new Interna();
            i.stampa();
        }
    }
    ```
    
2. **Classe interna statica**
    
    - Non ha accesso ai membri non statici della classe esterna.
    - Può essere istanziata senza un'istanza della classe esterna.
    
    ```java
    class Esterna {
        static class Interna {
            void stampa() {
                System.out.println("Sono una classe interna statica!");
            }
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Esterna.Interna i = new Esterna.Interna();
            i.stampa();
        }
    }
    ```
    

---

## **3. Diagrammi di sequenza (UML)**

I **diagrammi di sequenza** fanno parte della modellazione UML e servono a rappresentare la comunicazione tra gli oggetti nel tempo. Sono composti da:

- **Oggetti** (rappresentati con rettangoli).
- **Linea della vita** (una linea tratteggiata che scende verticalmente).
- **Messaggi** (frecce che rappresentano la comunicazione tra oggetti).

### **Esempio di flusso in un diagramma di sequenza**

Immaginiamo un sistema bancario con un **Cliente**, un **Bancomat**, e una **Banca**:

```
Cliente → Bancomat : inserisce carta
Bancomat → Banca : verifica PIN
Banca → Bancomat : PIN corretto
Bancomat → Cliente : mostra opzioni
```

I diagrammi di sequenza aiutano a visualizzare **come** gli oggetti interagiscono tra loro in un processo.

---

## **4. Generics (con implementazione di una coda)**

I **Generics** in Java permettono di scrivere codice generico, che può funzionare con diversi tipi di dati senza ripetere l’implementazione.

### **Esempio: Implementazione di una coda generica**

```java
class Coda<T> {
    private LinkedList<T> elementi = new LinkedList<>();

    public void enqueue(T elemento) {
        elementi.addLast(elemento);
    }

    public T dequeue() {
        if (elementi.isEmpty()) {
            throw new RuntimeException("Coda vuota!");
        }
        return elementi.removeFirst();
    }

    public boolean isEmpty() {
        return elementi.isEmpty();
    }
}

public class Main {
    public static void main(String[] args) {
        Coda<Integer> coda = new Coda<>();
        coda.enqueue(10);
        coda.enqueue(20);
        System.out.println(coda.dequeue()); // 10
    }
}
```

---

## **5. Utilizzo di `Random` per la generazione di valori pseudocasuali**

La classe `Random` in Java viene utilizzata per generare numeri casuali.

### **Generare un numero casuale in un intervallo [min, max]**

```java
import java.util.Random;

public class Main {
    public static void main(String[] args) {
        Random rand = new Random();
        int min = 5, max = 15;
        int numeroCasuale = rand.nextInt(max - min + 1) + min; // Tra 5 e 15 inclusi
        System.out.println("Numero casuale: " + numeroCasuale);
    }
}
```

---

## **6. Coda Circolare**

Una **coda circolare** è una variante della coda in cui l’ultimo elemento è collegato al primo, evitando lo spreco di spazio.

### **Esempio di implementazione**

```java
class CodaCircolare {
    private int[] coda;
    private int front, rear, size, capacità;

    public CodaCircolare(int capacità) {
        this.capacità = capacità;
        this.coda = new int[capacità];
        this.front = 0;
        this.rear = -1;
        this.size = 0;
    }

    public void enqueue(int valore) {
        if (size == capacità) {
            System.out.println("Coda piena!");
            return;
        }
        rear = (rear + 1) % capacità;
        coda[rear] = valore;
        size++;
    }

    public int dequeue() {
        if (size == 0) {
            throw new RuntimeException("Coda vuota!");
        }
        int valore = coda[front];
        front = (front + 1) % capacità;
        size--;
        return valore;
    }
}
```

Questo evita sprechi di spazio tipici delle code tradizionali.

---

## **7. Debug**

Il **debugging** è il processo di individuazione e correzione di errori nel codice.

### **Strumenti principali di debug in Java**

1. **Stampa con `System.out.println()`**
    
    ```java
    System.out.println("Valore di x: " + x);
    ```
    
2. **Uso del Debugger dell'IDE (es. IntelliJ, Eclipse, VS Code)**
    - Permette di **impostare breakpoint** e controllare lo stato del programma passo per passo.
3. **Gestione delle eccezioni con `try-catch`**
    
    ```java
    try {
        int risultato = 10 / 0; // Errore
    } catch (ArithmeticException e) {
        System.out.println("Errore: divisione per zero");
    }
    ```
    
4. **Uso di `assert` per verificare condizioni durante l'esecuzione**
    
    ```java
    assert x > 0 : "Errore: x deve essere positivo!";
    ```
    

---
