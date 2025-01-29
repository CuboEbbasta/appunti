In Java, una **lista** è una struttura dati utilizzata per memorizzare una collezione di elementi in cui l'ordine di inserimento viene mantenuto. Può contenere elementi duplicati e fornisce metodi per manipolare questi elementi.

La lista più comune in Java è l'interfaccia `List`, che fa parte del package `java.util`. Le implementazioni principali di questa interfaccia sono:

- **`ArrayList`**: Una lista basata su array dinamico.
- **`LinkedList`**: Una lista basata su una struttura a nodi collegati (lista collegata).

Entrambe implementano l'interfaccia `List` e forniscono metodi simili, ma con differenze di performance a seconda dell'operazione.

---

## **Metodi principali della classe `List`**

La maggior parte di questi metodi è disponibile per `ArrayList`, `LinkedList`, e altre implementazioni di `List`.

### **Aggiunta di elementi**

1. **`add(E e)`**  
    Aggiunge un elemento alla fine della lista.
    
    ```java
    List<String> lista = new ArrayList<>();
    lista.add("A");
    lista.add("B");
    System.out.println(lista); // Output: [A, B]
    ```
    
2. **`add(int index, E e)`**  
    Aggiunge un elemento in una posizione specifica della lista. Gli elementi successivi vengono spostati.
    
    ```java
    lista.add(1, "C");
    System.out.println(lista); // Output: [A, C, B]
    ```
    

---

### **Accesso agli elementi**

1. **`get(int index)`**  
    Restituisce l'elemento alla posizione specificata.
    
    ```java
    String elemento = lista.get(1); // C
    ```
    

---

### **Modifica degli elementi**

1. **`set(int index, E e)`**  
    Sostituisce l'elemento in una posizione specifica con un nuovo valore.
    
    ```java
    lista.set(1, "D");
    System.out.println(lista); // Output: [A, D, B]
    ```
    

---

### **Rimozione di elementi**

1. **`remove(int index)`**  
    Rimuove l'elemento alla posizione specificata.
    
    ```java
    lista.remove(1);
    System.out.println(lista); // Output: [A, B]
    ```
    
2. **`remove(Object o)`**  
    Rimuove la prima occorrenza dell'oggetto specificato.
    
    ```java
    lista.remove("B");
    System.out.println(lista); // Output: [A]
    ```
    

---

### **Ricerca di elementi**

1. **`indexOf(Object o)`**  
    Restituisce l'indice della prima occorrenza dell'elemento, o `-1` se non è presente.
    
    ```java
    int index = lista.indexOf("A"); // 0
    ```
    
2. **`lastIndexOf(Object o)`**  
    Restituisce l'indice dell'ultima occorrenza dell'elemento.
    
3. **`contains(Object o)`**  
    Verifica se l'elemento è presente nella lista.
    
    ```java
    boolean esiste = lista.contains("A"); // true
    ```
    

---

### **Dimensione e controllo**

1. **`size()`**  
    Restituisce il numero di elementi nella lista.
    
    ```java
    int size = lista.size(); // 1
    ```
    
2. **`isEmpty()`**  
    Controlla se la lista è vuota.
    
    ```java
    boolean vuota = lista.isEmpty(); // false
    ```
    

---

### **Iterazione**

1. **`for` normale**
    
    ```java
    for (int i = 0; i < lista.size(); i++) {
        System.out.println(lista.get(i));
    }
    ```
    
2. **`for-each`**
    
    ```java
    for (String elemento : lista) {
        System.out.println(elemento);
    }
    ```
    
3. **`Iterator`**
    
    ```java
    Iterator<String> iteratore = lista.iterator();
    while (iteratore.hasNext()) {
        System.out.println(iteratore.next());
    }
    ```
    

---

### **Altri metodi utili**

1. **`clear()`**  
    Rimuove tutti gli elementi dalla lista.
    
    ```java
    lista.clear();
    System.out.println(lista); // Output: []
    ```
    
2. **`subList(int fromIndex, int toIndex)`**  
    Restituisce una vista (non una copia) di una porzione della lista.
    
    ```java
    List<String> sottoLista = lista.subList(0, 2);
    ```
    
3. **`toArray()`**  
    Converte la lista in un array.
    
    ```java
    String[] array = lista.toArray(new String[0]);
    ```
    

---

## **ArrayList vs LinkedList**

1. **`ArrayList`**
    
    - Basata su un array dinamico.
    - Velocissima per l'accesso agli elementi (`get` e `set`).
    - Lenta per aggiunte/rimozioni al centro (poiché richiede lo spostamento degli elementi).
2. **`LinkedList`**
    
    - Basata su nodi collegati.
    - Più veloce per aggiunte/rimozioni a inizio o fine.
    - Più lenta per l'accesso casuale, poiché richiede l'iterazione.

---

## **Esempio completo**

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> lista = new ArrayList<>();

        // Aggiungi elementi
        lista.add("A");
        lista.add("B");
        lista.add(1, "C");

        // Stampa lista
        System.out.println("Lista: " + lista); // Output: [A, C, B]

        // Accesso e modifica
        String elemento = lista.get(1); // C
        lista.set(1, "D");

        // Controlla dimensione
        System.out.println("Dimensione: " + lista.size()); // 3

        // Rimuovi elemento
        lista.remove(0);

        // Iterazione
        for (String el : lista) {
            System.out.println(el);
        }
    }
}
```
