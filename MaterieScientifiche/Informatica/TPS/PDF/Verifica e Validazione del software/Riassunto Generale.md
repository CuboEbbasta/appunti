### **Testing**

Il testing è il processo di verifica e validazione di un sistema o software per identificare eventuali difetti, garantire che funzioni come previsto e soddisfi i requisiti.

---

### **Caratteristiche di un buon test**

1. **Test accurati**:
    - Devono individuare efficacemente i difetti nel sistema.
    - Si concentrano su casi limite, condizioni non banali e scenari complessi.
2. **Casi di test ripetibili**:
    - Devono poter essere rieseguiti in modo identico per verificare che le correzioni funzionino senza introdurre nuovi difetti.
3. **Test che aiutano nella localizzazione dei guasti**:
    - Devono fornire informazioni utili per identificare la causa del difetto.

---

### **Verification & Validation**

1. **Verification**:
    - Si concentra sul fatto che il software è stato sviluppato correttamente.
    - Risponde alla domanda: _"Stiamo costruendo il prodotto correttamente?"_
    - Usa tecniche come review, ispezioni e verifiche statiche.
2. **Validation**:
    - Si concentra sul fatto che il software soddisfa i requisiti dell'utente finale.
    - Risponde alla domanda: _"Stiamo costruendo il prodotto giusto?"_
    - Usa tecniche come testing dinamico e test di accettazione.

---

### **Test di Usabilità**

- Verificano che il sistema sia intuitivo e facile da usare.
- Valutano parametri come:
    - Facilità di apprendimento.
    - Efficienza nell'uso.
    - Soddisfazione dell'utente.

---

### **Test e Casi di Test**

- **Test**: Esecuzione pratica del software per verificare il comportamento rispetto a specifici casi di test.
- **Caso di Test**: Una situazione o input specifico progettato per testare una funzionalità.
    - Include:
        - Condizioni iniziali.
        - Dati di input.
        - Risultati attesi.

---

### **Oracolo**

Un oracolo è un meccanismo o entità che determina il risultato atteso per un caso di test. Può essere:

- Una specifica formale.
- Una simulazione o prototipo.
- L'input di un esperto.

---

### **Debugging**

- Processo di identificazione e correzione dei difetti trovati durante il testing.
- Non è lo stesso del testing: il debugging si occupa della correzione, mentre il testing si occupa dell'individuazione dei problemi.

---

### **Tipi di Verifica**

1. **Verifica Statica**:
    - Eseguita senza eseguire il programma.
    - Include:
        - **Review** (es. desk check): Controllo manuale del codice, documenti o specifiche.
        - **Model Checking**: Tecnica automatizzata per verificare che un modello di sistema soddisfi le specifiche formali.
    - **Impossibile per programmi che generano codice a runtime**: Questi programmi costruiscono dinamicamente parti del codice durante l'esecuzione, rendendo impraticabile l'analisi statica completa.
2. **Verifica Dinamica**:
    - Richiede l'esecuzione del software.
    - Comprende il **testing dinamico**, che coinvolge input reali o simulati.

---

### **Testing Dinamico**

**Definizione**: Processo di esecuzione del software per verificare che soddisfi i requisiti. Si basa sull'osservazione dell'output rispetto agli input.

**Metodi disponibili**:

1. **Testing funzionale (Black Box)**:
    - Non considera l'implementazione interna.
    - Testa il comportamento del sistema in base ai requisiti.
2. **Testing strutturale (White Box)**:
    - Considera l'implementazione interna.
    - Include analisi di percorsi, copertura del codice e controllo dei flussi.
3. **Testing casuale**:
    - Usa input casuali per identificare difetti imprevisti.

---

### **Livelli di Test**

1. **Unit Testing**:
    - Testa singoli componenti o unità del codice.
    - Usa spesso stub o driver per simulare dipendenze.
2. **Test di integrazione**:
    - Testa l'interazione tra moduli o componenti.
    - Approcci:
        - **Top-down**: Testa i moduli di alto livello per primi.
        - **Bottom-up**: Testa i moduli di basso livello per primi.
        - **Sandwich**: Combinazione di entrambi.
3. **Test di sistema**:
    - Verifica il sistema completo.
    - Include:
        - **Test di stress**: Sistema sotto carichi pesanti.
        - **Test di sicurezza**: Controlla la protezione da accessi non autorizzati.
        - **Test di robustezza**: Verifica come il sistema gestisce input non validi.
        - **Test di configurazione**: Testa il sistema su diverse configurazioni hardware/software.
        - **Test di usabilità e compatibilità**: Verifica l'ergonomia e l'adattabilità con altri sistemi.

---

### **Test di Accettazione**

- Verifica se il sistema soddisfa i requisiti degli utenti.
- Eseguito dai clienti o dagli utenti finali.

---

### **Specifica di Test**

Un documento che descrive come eseguire i test. Contiene:

1. **Test Bed**: Ambiente di test (hardware, software, strumenti).
2. **Procedura di Test**: Istruzioni passo passo per l'esecuzione.
3. **Input dati** e **risultati attesi**.

---

### **Test di Regressione**

- Verifica che le modifiche al codice non introducano nuovi difetti.
- Eseguito frequentemente durante lo sviluppo per garantire la stabilità del sistema.
