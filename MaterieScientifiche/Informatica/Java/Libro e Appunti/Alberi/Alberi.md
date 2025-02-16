Un **albero** è una struttura dati gerarchica utilizzata per rappresentare una collezione di elementi (nodi), organizzati in modo che ogni elemento (tranne uno) abbia un solo genitore e possa avere zero o più figli. È una struttura molto usata in informatica per rappresentare dati con relazioni gerarchiche, come i file system, le espressioni matematiche o le classificazioni.

---

### **Definizioni principali**

1. **Nodo:** Ogni elemento dell'albero che può contenere un dato e riferimenti ad altri nodi (figli).
2. **Arco:** Una connessione diretta tra due nodi.
3. **Connesso:** Un albero è connesso se c'è un percorso tra ogni coppia di nodi.
4. **Aciclico:** Un albero non contiene cicli, ovvero non è possibile tornare allo stesso nodo percorrendo gli archi.
5. **Albero con radice:** Un albero con un nodo speciale chiamato **radice**, da cui si diramano tutti gli altri nodi.
6. **Padre e Figlio:** Il nodo A è il **padre** di un nodo B se esiste un arco da A a B. Di conseguenza, B è il **figlio** di A.
7. **Foglia:** Un nodo senza figli.
8. **Fratelli:** Nodi che hanno lo stesso padre.
9. **Sottoalbero:** Una porzione dell'albero che parte da un nodo e include tutti i suoi discendenti.
10. **Profondità:** La distanza (numero di archi) dalla radice a un nodo.
11. **Livelli:** Insieme di tutti i nodi che hanno la stessa profondità.
12. **PTR (Pointer Tree Root):** Un puntatore che indica il nodo radice dell'albero.
13. **PFC (Pointer First Child):** Un puntatore che indica il primo figlio di un nodo.

---

### **Tipologie di Alberi**

14. **Alberi Generici:** Ogni nodo può avere un numero arbitrario di figli.
15. **Alberi Binari:** Ogni nodo può avere al massimo due figli (sinistro e destro).
16. **Alberi N-ari:** Ogni nodo può avere al massimo N figli.

---

### **Esempi Visivi**

#### Esempio 1: Albero Generico

```
           A (Radice)
         /   |    \
        B    C     D
       / \       / | \
      E   F     G  H  I
```

- **Radice:** `A`
- **Padre di B:** `A`
- **Figli di A:** `B, C, D`
- **Foglie:** `E, F, G, H, I`
- **Fratelli di B:** `C, D`
- **Sottoalbero radicato in D:**

```
        D
      / | \
     G  H  I
```

---

#### Esempio 2: Albero Binario

```
           10
         /    \
        5      15
       / \    /  \
      2   7  12   20
```

- **Radice:** `10`
- **Figli di 10:** `5, 15`
- **Padre di 7:** `5`
- **Foglie:** `2, 7, 12, 20`
- **Profondità di 12:** `2`
- **Livelli:**
    - Livello 0: `10`
    - Livello 1: `5, 15`
    - Livello 2: `2, 7, 12, 20`

---

### **Codice Java: Albero Generico**

#### Classe Nodo e Albero Generico

```java
import java.util.ArrayList;
import java.util.List;

class Nodo {
    String valore;
    List<Nodo> figli;

    public Nodo(String valore) {
        this.valore = valore;
        this.figli = new ArrayList<>();
    }

    public void aggiungiFiglio(Nodo figlio) {
        figli.add(figlio);
    }

    public List<Nodo> getFigli() {
        return figli;
    }

    public String getValore() {
        return valore;
    }
}

class Albero {
    private Nodo radice;

    public Albero(String valoreRadice) {
        this.radice = new Nodo(valoreRadice);
    }

    public Nodo getRadice() {
        return radice;
    }

    public void stampa(Nodo nodo, String prefisso) {
        if (nodo == null) return;
        System.out.println(prefisso + nodo.getValore());
        for (Nodo figlio : nodo.getFigli()) {
            stampa(figlio, prefisso + "--");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Albero albero = new Albero("A");
        Nodo radice = albero.getRadice();

        Nodo b = new Nodo("B");
        Nodo c = new Nodo("C");
        Nodo d = new Nodo("D");

        radice.aggiungiFiglio(b);
        radice.aggiungiFiglio(c);
        radice.aggiungiFiglio(d);

        b.aggiungiFiglio(new Nodo("E"));
        b.aggiungiFiglio(new Nodo("F"));
        d.aggiungiFiglio(new Nodo("G"));
        d.aggiungiFiglio(new Nodo("H"));
        d.aggiungiFiglio(new Nodo("I"));

        System.out.println("Struttura dell'albero:");
        albero.stampa(radice, "");
    }
}
```

---

### **Codice Java: Albero Binario**

#### Classe Nodo e Albero Binario

```java
class NodoBinario {
    int valore;
    NodoBinario sinistro, destro;

    public NodoBinario(int valore) {
        this.valore = valore;
        this.sinistro = null;
        this.destro = null;
    }
}

class AlberoBinario {
    private NodoBinario radice;

    public AlberoBinario(int valoreRadice) {
        this.radice = new NodoBinario(valoreRadice);
    }

    public NodoBinario getRadice() {
        return radice;
    }

    public void aggiungi(NodoBinario nodo, int valore, boolean sinistro) {
        if (sinistro) {
            nodo.sinistro = new NodoBinario(valore);
        } else {
            nodo.destro = new NodoBinario(valore);
        }
    }

    public void stampa(NodoBinario nodo) {
        if (nodo == null) return;
        stampa(nodo.sinistro);
        System.out.print(nodo.valore + " ");
        stampa(nodo.destro);
    }
}

public class Main {
    public static void main(String[] args) {
        AlberoBinario albero = new AlberoBinario(10);
        NodoBinario radice = albero.getRadice();

        albero.aggiungi(radice, 5, true);  // Figlio sinistro
        albero.aggiungi(radice, 15, false); // Figlio destro
        albero.aggiungi(radice.sinistro, 2, true);
        albero.aggiungi(radice.sinistro, 7, false);
        albero.aggiungi(radice.destro, 12, true);
        albero.aggiungi(radice.destro, 20, false);

        System.out.println("Albero Binario (in-order):");
        albero.stampa(radice);
    }
}
```

---
[[Alberi Binari]]