### **Controllo delle Versioni**

Il controllo delle versioni è il processo di gestione delle modifiche al codice sorgente o ad altri documenti digitali. È fondamentale per collaborare in team e mantenere uno storico delle modifiche.

**Scopi principali**:

1. **Tracciare le modifiche**: Ogni versione è documentata e può essere recuperata.
2. **Collaborazione**: Più persone possono lavorare contemporaneamente sullo stesso progetto.
3. **Prevenire errori irreversibili**: Permette di tornare indietro a versioni precedenti in caso di errori.

---

### **Numerazione delle Release/Versioni**

Il sistema di numerazione delle versioni segue il formato **MAJOR.MINOR.PATCH**, dove:

1. **MAJOR (Major Level)**:
    - Incrementato per cambiamenti importanti e incompatibili con le versioni precedenti.
    - Es.: Passare da `1.0.0` a `2.0.0`.
2. **MINOR (Minor Level)**:
    - Incrementato per l'aggiunta di nuove funzionalità compatibili con le versioni precedenti.
    - Es.: Passare da `1.0.0` a `1.1.0`.
3. **PATCH (Patch Level)**:
    - Incrementato per correzioni di bug o miglioramenti minori.
    - Es.: Passare da `1.0.0` a `1.0.1`.

---

### **Sistemi di Versionamento**

1. **Reversibilità**:
    - Permette di tornare a una versione precedente del codice.
2. **Concorrenza**:
    - Consente a più sviluppatori di lavorare sugli stessi file contemporaneamente.
3. **Annotazione**:
    - Ogni modifica è accompagnata da un messaggio che spiega cosa è stato cambiato e perché.

---

### **Branch e Fork**

1. **Branch**:
    - Un branch è una linea di sviluppo separata. Permette di lavorare su nuove funzionalità o correzioni senza interferire con il codice principale.
    - Esempio:
        - Branch `main`: Codice stabile.
        - Branch `feature-x`: Lavoro su una nuova funzionalità.
2. **Fork**:
    - Una copia di un repository che risiede sotto un diverso account o organizzazione. È utile per collaborazioni su progetti open source.

---

### **VCS Centralizzati e Distribuiti**

1. **Sistemi Centralizzati**:
    - Es.: Subversion (SVN).
    - Il repository è centralizzato su un unico server.
    - Pro:
        - Semplicità di configurazione.
    - Contro:
        - Il server centrale è un punto di fallimento.
        - Difficoltà nel lavorare offline.
2. **Sistemi Distribuiti**:
    - Es.: Git.
    - Ogni sviluppatore ha una copia completa del repository.
    - Pro:
        - Maggiore flessibilità e resilienza.
        - Supporto migliore per il lavoro offline.

---

### **SVN (Subversion)**

SVN è un sistema di controllo delle versioni centralizzato.

- **Caratteristiche principali**:
    - Tutti i file e le modifiche sono memorizzati su un server centrale.
    - Richiede accesso al server per la maggior parte delle operazioni.
- **Comandi principali**:
    - `svn checkout`: Scarica il repository sul computer locale.
    - `svn commit`: Invia le modifiche al server.
    - `svn update`: Sincronizza il repository locale con il server.

---

### **Git**

Git è un sistema di controllo delle versioni distribuito, popolare per il lavoro collaborativo.

#### **Comandi principali per lavorare in team con Git**

1. **Clonare un repository**:
    - `git clone <URL>`: Copia il repository sul proprio computer.
2. **Creare un branch**:
    - `git branch <nome-branch>`: Crea un nuovo branch.
    - `git checkout <nome-branch>`: Sposta il lavoro sul branch creato.
    - Oppure: `git switch -c <nome-branch>`.
3. **Aggiungere modifiche**:
    - `git add <file>`: Aggiunge un file all'area di staging.
    - `git add .`: Aggiunge tutti i file modificati.
4. **Committare modifiche**:
    - `git commit -m "Messaggio descrittivo"`: Salva le modifiche localmente con un messaggio.
5. **Sincronizzare con il repository remoto**:
    - `git pull`: Recupera le modifiche dal repository remoto.
    - `git push`: Invia le modifiche al repository remoto.
6. **Unire branch**:
    - `git merge <nome-branch>`: Unisce le modifiche di un branch nel branch corrente.
7. **Visualizzare lo stato**:
    - `git status`: Mostra lo stato attuale del repository.
8. **Gestire conflitti**:
    - Quando due modifiche confliggono, Git richiede di risolvere manualmente i conflitti nei file.

---

### **GitLab e GitHub**

Entrambe sono piattaforme basate su Git per la gestione di repository remoti.  
**Differenze principali**:

1. **GitHub**:
    - Maggiormente orientato ai progetti open source.
    - Offre una vasta comunità e integrazione con altre piattaforme.
2. **GitLab**:
    - Si concentra sull'integrazione continua (CI/CD).
    - Offre funzionalità più robuste per l'automazione dei workflow.

**Caratteristiche comuni**:

- Interfacce web per la gestione dei repository.
- Strumenti per le Pull Request (GitHub) o Merge Request (GitLab).
- Hosting di repository pubblici e privati.