## **Regole di Codifica**

==Le regole di codifica **definiscono linee guida per scrivere codice** leggibile, mantenibile e privo di errori==.

### **Scopi principali**:

1. **Leggibilità**: ==Facilitare la comprensione del codice== a tutti i membri del team.
2. **Manutenibilità**: ==Rendere il codice più semplice da aggiornare o correggere==.
3. **Uniformità**: ==Evitare stili di codifica incoerenti tra i programmatori==.
4. **Prevenzione degli errori**: ==Riducono la probabilità di bug legati a cattive pratiche==.

Esempio:

- **Evita nomi generici** per variabili come `x`, `temp`, ecc.
- **Usa il camelCase** per variabili e metodi in Java.

---

## **Guide di Stile**

==Le guide di stile forniscono regole specifiche== per scrivere codice seguendo standard ben definiti.

### **Macro tipologie di regole**:

1. **Regole di Formattazione**:
    - Stabiliscono come indentare, posizionare le parentesi e spaziature.
    - Es.: "Usare 4 spazi per l'indentazione, non tabulazioni."
2. **Regole sui Nomi**:
    - Specificano convenzioni per i nomi di classi, metodi, variabili, ecc.
    - Es.: "Nomi delle classi in PascalCase, nomi dei metodi in camelCase."
3. **Documentazione**:
    - Indicano come scrivere commenti e documentare il codice con Javadoc.
    - Es.: "Ogni metodo pubblico deve avere un commento Javadoc che ne descriva lo scopo."

---

## **Google Java Style Guide**

Una guida di riferimento per scrivere codice Java standardizzato. Ecco i punti chiave dei capitoli richiesti:

### **Capitolo 2: Elementi Base di Codifica**

1. **Sorgenti UTF-8**:
    - Tutti i file sorgenti devono essere in codifica UTF-8.
2. **Caratteri visibili**:
    - Non usare caratteri invisibili (es. caratteri non stampabili) nel codice.
3. **Linee lunghe**:
    - Limita la lunghezza delle linee a **100 caratteri**.
4. **File di origine**:
    - Ogni file `.java` deve contenere **una sola classe pubblica**.
    - Il nome del file deve corrispondere al nome della classe pubblica.

---

### **Capitolo 4: Formattazione**

1. **Indentazione**:
    - Usa 2 spazi per l'indentazione (non tabulazioni).
2. **Linee vuote**:
    - Aggiungi una linea vuota per separare blocchi logici di codice.
3. **Parentesi**:
    - Posiziona le parentesi aperte `{` sulla stessa linea della dichiarazione:
        
        ```java
        if (condition) {
            // codice
        } else {
            // codice
        }
        ```
        
4. **Spaziature**:
    - Usa spazi attorno agli operatori binari:
        
        ```java
        int sum = a + b;
        ```
        
5. **Linee multiple**:
    - Spezza le linee lunghe in più righe rispettando un'indentazione coerente:
        
        ```java
        someMethod(argument1, argument2,
                   argument3, argument4);
        ```
        

---

### **Capitolo 5: Nomi**

1. **Classi**:
    - Usa **PascalCase** per i nomi delle classi:
        
        ```java
        public class MyClassName {}
        ```
        
2. **Variabili e Metodi**:
    - Usa **camelCase**:
        
        ```java
        int myVariable = 10;
        public void myMethod() {}
        ```
        
3. **Costanti**:
    - Usa **tutto maiuscolo con underscore**:
        
        ```java
        public static final int MAX_COUNT = 100;
        ```
        
4. **Nomi brevi ma significativi**:
    - Evita abbreviazioni poco comprensibili.

---

### **Capitolo 7: Javadoc**

1. **Regole generali**:
    - Usa commenti Javadoc per ogni classe, metodo o costruttore pubblico.
2. **Struttura**:
    - Ogni commento deve iniziare con `/**` e terminare con `*/`.
    - Usa tag specifici:
        - `@param` per descrivere i parametri.
        - `@return` per descrivere il valore restituito.
        - `@throws` per eccezioni.
3. **Esempio**:
    
    ```java
    /**
     * Calcola la somma di due numeri.
     *
     * @param a il primo numero
     * @param b il secondo numero
     * @return la somma di a e b
     */
    public int sum(int a, int b) {
        return a + b;
    }
    ```
    