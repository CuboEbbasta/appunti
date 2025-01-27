### **Induttore**

==Un induttore è un componente elettrico costituito generalmente da una bobina di filo conduttore==. Quando ==una corrente varia nel tempo attraversa l'induttore==, esso ==genera un campo magnetico== che, ==per la **Legge di Faraday**==, induce una ==forza elettromotrice (f.e.m.) che si oppone al cambiamento di corrente==.

==L'induttanza== L ==quantifica questa capacità di opporsi ai cambiamenti della corrente==.

**L'induttanza misura la sua capacità di opporsi ai cambiamenti della corrente che lo attraversa**.

---
### **Condensatore**

==Un **condensatore** è un componente elettrico utilizzato per immagazzinare energia sotto forma di **campo elettrico**==. È ==costituito da due piastre conduttrici separate da un materiale isolante chiamato **dielettrico**==.

---

### **Definizione di capacità**

==La **capacità** di un condensatore== (C) ==**misura la quantità di carica elettrica che il condensatore può immagazzinare per unità di differenza di potenziale applicata**==.

---
## Impedenza (Ω)

==L'impedenza (Z)== è un concetto fondamentale in elettrotecnica che ==rappresenta **la resistenza complessiva** che un circuito oppone **al passaggio della corrente alternata==** (AC).  È una grandezza complessa, ovvero ==composta da due parti: reale e immaginaria==. 

**1. ==Resistenza (R)==:** ==La parte reale dell'impedenza rappresenta la resistenza== offerta al passaggio della corrente da parte dei componenti resistivi del circuito, come resistori. Ad esempio, un resistore da 10 Ω offre una resistenza di 10 Ω alla corrente.

**2. ==Reattanza (X)==:** La parte immaginaria dell'impedenza rappresenta la resistenza opposta da elementi reattivi come condensatori e induttori.

* ==**Condensatore==:**  La reattanza capacitiva (XC) ==è inversamente proporzionale alla frequenza della corrente alternata e alla capacità del condensatore==. Maggiore è la frequenza, minore è la reattanza capacitiva. Ad esempio, un condensatore da 1 µF avrà una reattanza capacitiva di circa 160 Ω a una frequenza di 1 kHz.
* ==**Induttore:** La reattanza induttiva (XL) è direttamente proporzionale alla frequenza della corrente alternata e all'induttanza dell'induttore==. Maggiore è la frequenza, maggiore è la reattanza induttiva. Ad esempio, un induttore da 10 mH avrà una reattanza induttiva di circa 63 Ω a una frequenza di 1 kHz.

### Formula generale dell'impedenza:

Z = R + jX

Dove:

* Z è l'impedenza (in Ohm).
* R è la resistenza (in Ohm).
* X è la reattanza totale (in Ohm), calcolata come X = XL - XC.
* j è l'unità immaginaria (j² = -1).

### Modulo dell'impedenza:

Il modulo di Z, rappresentato da |Z|, rappresenta la magnitudine dell'impedenza e si calcola come:

|Z| = √(R² + X²)

### Frequenze

* ==**Frequenza di risonanza (fr):** È la frequenza a cui la reattanza induttiva e capacitiva si annullano== a vicenda. In questo caso, l'impedenza è minima. La formula per calcolare la frequenza di risonanza è: fr = 1 / (2π√(LC)), dove L è l'induttanza e C è la capacità del circuito.

* ==**Frequenza di taglio (fc):** È la frequenza a cui il segnale viene attenuato di -3 dB(0,707) rispetto al valore in ingresso.== Viene utilizzata nei filtri per selezionare una specifica banda di frequenze. La formula per calcolare la frequenza di taglio di un filtro RC è: fc = 1 / (2πRC), dove R è la resistenza e C è la capacità del circuito.

### Potenza

* **Potenza istantanea (p(t)):** ==Rappresenta la potenza trasferita o assorbita da un circuito in un dato istante di tempo==. Si calcola come p(t) = v(t) * i(t), dove v(t) è la tensione e i(t) è la corrente nel circuito.

* **Potenza attiva (P):** ==È la parte della potenza totale che viene effettivamente trasformata in lavoro utile==. Si calcola come P = Vrms * Irms * cos(φ), dove Vrms e Irms sono rispettivamente la tensione efficace e la corrente efficace, e φ è l'angolo di fase tra tensione e corrente.

### Corrente elettrica (I)

* **Definizione:** ==La corrente elettrica è il flusso di cariche elettriche attraverso un conduttore==. Si misura in Ampere (A).
* **Formula:** I = Q / t, dove Q è la carica (in Coulomb) e t è il tempo (in secondi).


### Generatore

* **Definizione:** ==Un generatore è un dispositivo che fornisce energia elettrica mantenendo una differenza di potenziale==. 
* **Tipi:**
    * **Generatore di tensione:** *Mantiene una tensione costante*. Esempi: batterie.
    * **Generatore di corrente:** *Mantiene una corrente costante*. Esempi: alternatori.
---
