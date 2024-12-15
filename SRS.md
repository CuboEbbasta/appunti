**Software Requirements Specification (SRS)**

  

**Autore:** [Nome Autore]  

**Data:** [Data di redazione]  

  

---

  

## **Sommario**

  

1. Introduzione  

   1.1 Scopo del documento  

   1.2 Scopo del prodotto  

   1.3 Definizioni, acronimi ed abbreviazioni  

   1.4 Documenti di riferimento  

  

2. Descrizione del sistema  

   2.1 Sistema e hardware richiesto  

   2.2 Identificazione e scopo del software  

   2.3 Descrizione generale  

  

3. Interfacce  

   3.1 Interfacce utente  

   3.2 Interfacce hardware  

   3.3 Interfacce software  

  

4. Use Case Diagram e scenari operativi  

  

5. Requisiti  

   5.1 Tabella requisiti funzionali  

   5.2 Tabella requisiti non funzionali, di dominio e vincolo  

  

6. Piani di test  

   6.1 Descrizione dei test  

   6.2 Report dei test  

  

7. Tracciabilità  

  

---

  

## **1. Introduzione**

  

### **1.1 Scopo del documento**

**Spiegazione:** Lo scopo di questa sezione è descrivere l'obiettivo del documento SRS. Include informazioni su cosa descriverà il documento e chi sono i destinatari principali.

  

**Esempio:** Questo documento definisce i requisiti per lo sviluppo del sistema "TaskManager", progettato per consentire la gestione di attività personali e professionali.

  

### **1.2 Scopo del prodotto**

**Spiegazione:** Questa sezione descrive l'obiettivo principale del software. Serve a chiarire perché il prodotto è stato creato e quali problemi intende risolvere.

  

**Esempio:** Il prodotto consente agli utenti di creare, modificare, eliminare e organizzare attività personali o lavorative, assegnando priorità e scadenze. Il sistema mira a migliorare la produttività individuale.

  

### **1.3 Definizioni, acronimi ed abbreviazioni**

**Spiegazione:** In questa sezione si riportano i termini tecnici, gli acronimi e le abbreviazioni utilizzate nel documento per assicurare chiarezza e comprensione.

  

**Esempio:**

- **Task:** Un'attività da completare.

- **Deadline:** La scadenza assegnata a un task.

- **UI:** Interfaccia utente (User Interface).

  

### **1.4 Documenti di riferimento**

**Spiegazione:** Elenca i documenti e le risorse utilizzati come riferimento per la stesura dell'SRS.

  

**Esempio:**

- IEEE Std 830-1998 - Recommended Practice for Software Requirements Specifications.  

- Manuale di progettazione "TaskManager".

  

---

  

## **2. Descrizione del sistema**

  

### **2.1 Sistema e hardware richiesto**

**Spiegazione:** Descrive i requisiti hardware e software necessari per installare ed eseguire il prodotto.

  

**Esempio:**

- **Piattaforma:** Windows 10+, macOS 11+, Android 10+, iOS 14+.

- **Hardware:** Minimo 4 GB di RAM, 100 MB di spazio libero.

  

### **2.2 Identificazione e scopo del software**

**Spiegazione:** Fornisce l'identità del software e il suo scopo generale.

  

**Esempio:** Il software è identificato come "TaskManager", un'app multipiattaforma per gestire attività con priorità e scadenze.

  

### **2.3 Descrizione generale**

**Spiegazione:** Fornisce una panoramica delle principali funzionalità e degli utenti target.

  

**Esempio:**

Il software offre funzionalità per:

- Creare e gestire task.

- Ricevere notifiche sui task.

- Visualizzare un riepilogo delle attività giornaliere.

Gli utenti target includono professionisti e studenti.

  

---

  

## **3. Interfacce**

  

### **3.1 Interfacce utente**

**Spiegazione:** Descrive le componenti dell'interfaccia utente e come interagiscono con gli utenti finali.

  

**Esempio:**

- **Home:** Visualizza l'elenco delle attività.

- **Editor:** Permette di creare/modificare task.

  

### **3.2 Interfacce hardware**

**Spiegazione:** Specifica le interfacce hardware richieste per il funzionamento del software.

  

**Esempio:** Dispositivo con schermo touchscreen o desktop con mouse e tastiera.

  

### **3.3 Interfacce software**

**Spiegazione:** Elenca i componenti software con cui il sistema interagisce.

  

**Esempio:**

- API di sincronizzazione con Google Calendar.

- Database SQLite per la gestione locale dei task.

  

---

  

## **4. Use Case Diagram e scenari operativi**

  

### **Use Case Diagram**

**Spiegazione:** Un diagramma UML che rappresenta gli attori e i casi d'uso principali.

  

**Esempio:** (Disegno di un diagramma UML Use Case che rappresenta attori come "Utente" e casi d'uso come "Crea Task", "Modifica Task", "Ricevi Notifica".)

  

### **Scenari operativi**

**Spiegazione:** Descrive i principali flussi di interazione tra gli utenti e il sistema.

  

**Esempio:**

1. **Scenario 1:** Creazione di un nuovo task:

   - L'utente accede all'app, inserisce titolo, scadenza e priorità, e salva il task.

  

2. **Scenario 2:** Notifica di promemoria:

   - Il sistema invia una notifica quando un task sta per scadere.

  

---

  

## **5. Requisiti**

  

### **5.1 Tabella requisiti funzionali**

**Spiegazione:** Elenca i requisiti funzionali del sistema in forma tabellare.

  

**Esempio:**

| ID | Descrizione                               | Priorità | Test case correlati |

|----|-----------------------------------------------|-----------|---------------------|

| RF1| Creare una nuova attività               | Alta  | TC1             |

| RF2| Modificare una attività esistente       | Media | TC2             |

| RF3| Notificare la scadenza di un'attività   | Alta  | TC3             |

  

### **5.2 Tabella requisiti non funzionali, di dominio e vincolo**

**Spiegazione:** Elenca i requisiti che non riguardano direttamente le funzionalità, come prestazioni, sicurezza o vincoli tecnici.

  

**Esempio:**

| ID | Descrizione                               | Categoria | Priorità |

|----|-----------------------------------------------|-----------|-----------|

| RNF1| Tempo di caricamento massimo di 2 secondi   | Prestazioni | Alta  |

| RNF2| Crittografia dei dati personali         | Sicurezza  | Alta  |

| RV1 | Compatibilità con Android 10+          | Vincolo | Alta  |

  

---

  

## **6. Piani di test**

  

### **6.1 Descrizione dei test**

**Spiegazione:** Descrive come i requisiti verranno verificati tramite test specifici.

  

**Esempio:**

- **Test Case 1:** Verifica della creazione di un task.  

  - **Input:** Titolo "Spesa", scadenza "15/12/2024".

  - **Output atteso:** Il task appare nell'elenco.

  

- **Test Case 2:** Verifica delle notifiche.  

  - **Input:** Scadenza alle 10:00.  

  - **Output atteso:** Notifica alle 9:50.

  

### **6.2 Report dei test**

**Spiegazione:** Riassume i risultati dei test effettuati sul sistema.

  

**Esempio:**

| Test ID | Requisito verificato | Risultato | Note             |

|---------|-----------------------|-----------|----------------------|

| TC1 | RF1              | Passato   | Task creato correttamente |

| TC2 | RF3              | Passato   | Notifica ricevuta |

  

---

  

## **7. Tracciabilità**

  

**Spiegazione:** Collega i requisiti ai test case e ai moduli del sistema per garantire che ogni requisito sia verificato e implementato correttamente.

  

**Esempio:**

| ID Requisito | Caso d'uso   | Modulo coinvolto  | Test Case  |

|--------------|------------------|-------------------|----------------|

| RF1      | Creazione Task   | Modulo Task   | TC1        |

| RF3      | Notifica Promemoria | Modulo Notifiche | TC2        |