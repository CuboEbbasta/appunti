## **Alberi Binari: Struttura, Proprietà e Implementazione in Java**

Un **albero binario** è una struttura dati gerarchica in cui ogni nodo ha al massimo **due figli** (chiamati **figlio sinistro** e **figlio destro**).

---

## **1. Concetti di Base**

Un **albero** è una struttura composta da nodi collegati tra loro, con un nodo speciale chiamato **radice** (_root_). Ogni nodo può avere:

- **Figlio sinistro** (_left child_)
- **Figlio destro** (_right child_)

Un **albero binario** segue queste regole:

- Ogni nodo può avere **al massimo due figli**.
- Ogni sottoalbero è a sua volta un albero binario.

### **Terminologia**

- **Radice (Root):** Il nodo principale dell’albero.
- **Foglie (Leaves):** Nodi senza figli.
- **Padre (Parent):** Nodo che ha uno o più figli.
- **Altezza:** Il numero massimo di livelli in un albero.
- **Sottoalbero (Subtree):** Ogni nodo, con i suoi figli, può essere visto come un albero a sé stante.

---

## **2. Tipologie di Alberi Binari**

### **Albero Binario Pieno (Full Binary Tree)**

Un albero binario è **pieno** se ogni nodo ha **0 o 2 figli**.

### **Albero Binario Completo (Complete Binary Tree)**

Un albero binario è **completo** se tutti i livelli sono riempiti **tranne forse l'ultimo**, che è riempito da sinistra a destra.

### **Albero Binario Perfetto (Perfect Binary Tree)**

Un albero binario è **perfetto** se tutti i nodi interni hanno **due figli** e tutte le foglie sono allo stesso livello.

### **Albero Binario di Ricerca (Binary Search Tree - BST)**

È un tipo speciale di albero binario in cui:

- Il **sottoalbero sinistro** contiene valori minori del nodo.
- Il **sottoalbero destro** contiene valori maggiori del nodo.
- Non ci sono duplicati.

---

## **3. Implementazione di un Albero Binario in Java**

Per implementare un albero binario, definiamo prima la **classe NodoAlberoBinario**, che rappresenta un nodo con tre elementi:

1. Il valore del nodo.
2. Il riferimento al figlio sinistro.
3. Il riferimento al figlio destro.

### **Classe `NodoAlberoBinario`**

```java
class NodoAlberoBinario {
    int valore;
    NodoAlberoBinario sinistro, destro;

    public NodoAlberoBinario(int valore) {
        this.valore = valore;
        this.sinistro = null;
        this.destro = null;
    }
}
```

Questa classe definisce un **nodo** con un valore e due puntatori ai figli.

---

## **4. Classe `AlberoBinario` con operazioni principali**

Ora implementiamo la classe **AlberoBinario**, con le operazioni di base:

4. **Inserimento di un nodo**
5. **Visita anticipata (preorder)**
6. **Visita differita (postorder)**
7. **Ricerca di un valore**
8. **Stampa dell’albero**

### **Implementazione**

```java
class AlberoBinario {
    NodoAlberoBinario radice;

    public AlberoBinario() {
        this.radice = null;
    }

    // Metodo per inserire un nodo nell'albero
    public void inserisci(int valore) {
        radice = inserisciRicorsivo(radice, valore);
    }

    private NodoAlberoBinario inserisciRicorsivo(NodoAlberoBinario nodo, int valore) {
        if (nodo == null) {
            return new NodoAlberoBinario(valore);
        }
        if (valore < nodo.valore) {
            nodo.sinistro = inserisciRicorsivo(nodo.sinistro, valore);
        } else {
            nodo.destro = inserisciRicorsivo(nodo.destro, valore);
        }
        return nodo;
    }

    // Visita anticipata (Preorder: Radice → Sinistra → Destra)
    public void visitaAnticipata(NodoAlberoBinario nodo) {
        if (nodo != null) {
            System.out.print(nodo.valore + " ");
            visitaAnticipata(nodo.sinistro);
            visitaAnticipata(nodo.destro);
        }
    }

    // Visita differita (Postorder: Sinistra → Destra → Radice)
    public void visitaDifferita(NodoAlberoBinario nodo) {
        if (nodo != null) {
            visitaDifferita(nodo.sinistro);
            visitaDifferita(nodo.destro);
            System.out.print(nodo.valore + " ");
        }
    }

    // Metodo per cercare un valore nell'albero
    public boolean cerca(int valore) {
        return cercaRicorsivo(radice, valore);
    }

    private boolean cercaRicorsivo(NodoAlberoBinario nodo, int valore) {
        if (nodo == null) {
            return false;
        }
        if (nodo.valore == valore) {
            return true;
        }
        return valore < nodo.valore ? cercaRicorsivo(nodo.sinistro, valore) : cercaRicorsivo(nodo.destro, valore);
    }
}
```

---

## **5. Test dell'Albero Binario**

Nel `main`, possiamo creare un albero e testare le operazioni:

```java
public class Main {
    public static void main(String[] args) {
        AlberoBinario albero = new AlberoBinario();

        // Inserimento di alcuni nodi
        albero.inserisci(50);
        albero.inserisci(30);
        albero.inserisci(70);
        albero.inserisci(20);
        albero.inserisci(40);
        albero.inserisci(60);
        albero.inserisci(80);

        // Stampa dell'albero in Preorder e Postorder
        System.out.print("Visita anticipata (Preorder): ");
        albero.visitaAnticipata(albero.radice);
        System.out.println();

        System.out.print("Visita differita (Postorder): ");
        albero.visitaDifferita(albero.radice);
        System.out.println();

        // Ricerca di un valore
        System.out.println("Il valore 40 è presente? " + albero.cerca(40)); // true
        System.out.println("Il valore 100 è presente? " + albero.cerca(100)); // false
    }
}
```

---

## **6. Complessità Temporale delle Operazioni**

|Operazione|Complessità Tempo (caso medio)|Complessità Tempo (caso peggiore, albero sbilanciato)|
|---|---|---|
|Inserimento|**O(log n)**|**O(n)** (se è una lista)|
|Ricerca|**O(log n)**|**O(n)**|
|Visita|**O(n)**|**O(n)**|

Per evitare il caso peggiore, si possono usare **Alberi Bilanciati** come:

- **AVL Tree** (autobilanciato)
- **Red-Black Tree** (usato nelle Java Collections come `TreeSet` e `TreeMap`)

---

## **Conclusione**

Abbiamo visto:

- La definizione di **albero binario** e le sue varianti.
- L'implementazione di un **Albero Binario di Ricerca** con inserimento, ricerca e visite.
- Il confronto delle complessità temporali.
