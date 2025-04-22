## COSA SONO I FILTRI

Un **filtro** è un circuito in grado di modificare il contenuto in frequenza di un segnale. Il suo scopo principale è **lasciare passare alcune frequenze** e **attenuarne o bloccarne altre**.

==Un **filtro** è un **circuito elettronico** che serve a **modificare la risposta in frequenza** di un segnale.==  
==Il suo scopo principale è **lasciare passare alcune frequenze** (quelle “utili”) e **bloccarne altre** (quelle indesiderate o dannose)==.

In pratica, ==un filtro agisce selettivamente sullo **spettro del segnale**==, ==cioè sul contenuto in frequenza==, permettendo il passaggio solo di alcune componenti e riducendo le altre.

---

## TIPI DI FILTRO

### 1. Filtro Passa-Basso (Low-Pass Filter - LPF)

- Lascia passare solo le frequenze inferiori a una certa frequenza di taglio `fc`
    
- Attenua le frequenze superiori a `fc`
    
- Viene usato per rimuovere i segnali ad alta frequenza (rumore, aliasing)
    

### 2. Filtro Passa-Alto (High-Pass Filter - HPF)

- Lascia passare solo le frequenze superiori a `fc`
    
- Attenua le frequenze inferiori a `fc`
    
- Utile per eliminare il rumore a bassa frequenza o i segnali di offset
    

### 3. Filtro Passa-Banda (Band-Pass Filter - BPF)

- ==Lascia passare solo un intervallo di frequenze compreso tra `f1` e `f2`==
    
- Attenua sia le frequenze inferiori a `f1` che quelle superiori a `f2`
    
- Utilizzato per selezionare un canale radio o una frequenza specifica
    

### 4. Filtro Elimina-Banda (Band-Stop Filter o Notch Filter)

- ==Attenua solo una determinata banda di frequenze==, ==lasciando passare tutto il resto==
    
- Impiegato per eliminare disturbi a frequenze precise, come i ==50 Hz della rete elettrica==
    

### 5. Filtro Selettivo

- ==È un filtro molto preciso con una banda passante molto stretta==
    
- Consente di isolare solo una frequenza (o una gamma ristretta) con grande precisione
    
- È un tipo particolare di filtro ==passa-banda, caratterizzato da un alto fattore di qualità==
    

---

## PARAMETRI DEI FILTRI

- **Frequenza di taglio (`fc`)**: l==a frequenza alla quale il segnale è attenuato di circa -3 dB== (cioè ridotto a circa il 70% del valore massimo)
    
- **Banda passante**: ==l’intervallo di frequenze che il filtro lascia passare==
    
- **Banda attenuata**: ==le frequenze che vengono fortemente attenuate o bloccate==
    
- **Pendenza (roll-off)**: indica la ==rapidità con cui il filtro attenua le frequenze fuori dalla banda utile== (ad esempio -20 dB/decade)
    
- **Fattore di qualità (`Q`)**: ==rapporto tra la frequenza centrale e la larghezza della banda passante== (utile nei filtri passa banda e selettivi)
    

---

## FILTRI ANALOGICI RC, RL, RLC

I filtri possono essere realizzati con **componenti passivi**:

- **Resistori (R)**
    
- **Condensatori (C)**
    
- **Induttori (L)**
    

Esempi:

- Filtro passa basso RC: resistenza in serie, condensatore verso massa
    
- Filtro passa alto RC: condensatore in serie, resistenza verso massa
    
- Filtri RLC: permettono la realizzazione di filtri passa banda, selettivi, elimina banda
    

Esistono anche filtri **attivi**, realizzati con amplificatori operazionali, e **filtri digitali**, realizzati via software nei DSP.

---

## FUNZIONE DI TRASFERIMENTO g(f)

- ==La funzione di trasferimento `g(f)` indica come il filtro modifica ogni frequenza `f` in ingresso==

- ==La G(f) oltre ad essere la risposta in frequenza del segnale==, serve per indicare a quali frequenze passa il segnale.

- Si analizza nel **dominio della frequenza**
    
- Di solito si rappresenta con due grafici:
    
    - Modulo: |g(f)| → quanto passa una frequenza
        
    - Fase: ∠g(f) → di quanto viene sfasata la frequenza
        

---

## SPETTRO DI UN SEGNALE

- ==Lo spettro rappresenta la **scomposizione in frequenze** di un segnale==

- ==Lo **spettro** di un segnale è **la sua rappresentazione nel dominio della frequenza**.==

- Immagina un segnale audio (una canzone):

	- Nel dominio del tempo, vedi l'onda che varia nel tempo.
    
	- Nel dominio della frequenza (cioè **lo spettro**), vedi le **note** (frequenze) presenti nella canzone e quanto sono forti.

- ==Si ottiene tramite trasformata di Fourier==
    
- È fondamentale per capire come un filtro agisce su un segnale
    
- Ogni segnale reale ha uno spettro finito o continuo, che può contenere armoniche, rumore, disturbi
    

---

## ARMONICHE

- ==Quando un segnale è **periodico ma non sinusoidale**, può essere scomposto in una **serie di sinusoidi**==

- Le **armoniche** sono **componenti sinusoidali** di un segnale **periodico**, che hanno **frequenze multiple** della **frequenza fondamentale**.

- ==La frequenza più bassa si chiama **frequenza fondamentale (f₀)**==
    
- ==Le altre sono le **armoniche**==: 2f₀, 3f₀, 4f₀, ecc.
    
- ==Le armoniche definiscono il "timbro" del segnale==
    
- I filtri possono essere usati per attenuare o amplificare specifiche armoniche
    

---
## TRASFORMATA DI FOURIER

- La **trasformata di Fourier** ci permette di **analizzare un segnale nel dominio della frequenza**.

- Ogni segnale (anche molto complesso) può essere scritto come somma di sinusoidi di diverse frequenze, ampiezze e fasi.

- Somma di infinite armoniche di un segnale.

---
## DOMINIO DEL TEMPO E DOMINIO DELLA FREQUENZA

- **Dominio del tempo**: ==si analizza il segnale come funzione del tempo==. Si usano strumenti come l’oscilloscopio.
    
- **Dominio della frequenza**: ==si analizza come il segnale è composto da diverse frequenze==. Si usa la trasformata di Fourier o la FFT (Fast Fourier Transform).
    
- Il filtro viene progettato nel dominio della frequenza ma agisce nel tempo.
    

---

## COMPONENTI ELETTRICI: IMPEDENZA E COMPORTAMENTO

### Impedenza

- È una **generalizzazione della resistenza** per i segnali in corrente alternata
    
- Si indica con `Z` ed è un numero complesso: `Z = R + jX`
    
- La parte immaginaria `X` è la **reattanza**
    

### Resistore (R)

- ==Dissipa energia sotto forma di calore==
    
- Non ha dipendenza dalla frequenza
    
- Impedenza: `Z = R`
    

### Condensatore (C)

- ==È composto da **due armature conduttrici** separate da un **dielettrico (isolante)**==.

- ==Quando si applica tensione, si crea un **campo elettrico**, che accumula **cariche opposte** sulle due armature.==
    
- ==Si comporta da **corto circuito** alle alte frequenze e da **aperto** alle basse==
    
- Impedenza: `Z = 1 / (jωC)` → diminuisce con l’aumentare della frequenza
    

### Induttore (L)

- ==È una **bobina**: filo conduttore avvolto in spire==

- ==Quando la corrente scorre, crea un **campo magnetico** attorno alla bobina==
    
- ==Si comporta da **corto circuito** alle basse frequenze e da **aperto** alle alte==
    
- Impedenza: `Z = jωL` → aumenta con l’aumentare della frequenza
    

---

## CONCLUSIONI

Un filtro è un sistema progettato per operare sullo **spettro** di un segnale. A seconda della sua configurazione, può lasciar passare certe frequenze, bloccarne altre, o selezionarne solo alcune. È uno strumento fondamentale nelle telecomunicazioni, nell’elettronica e nel trattamento dei segnali.
