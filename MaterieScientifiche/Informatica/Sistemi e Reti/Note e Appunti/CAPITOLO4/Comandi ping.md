## Comandi Ping e Esempi

Il comando `ping` è uno strumento di rete fondamentale per verificare la connettività tra due dispositivi. Invia pacchetti ICMP (Internet Control Message Protocol) a un indirizzo IP specificato e attende una risposta. 

Ecco alcuni comandi ping utili:

**1. Ping Base:**

```
ping <indirizzo_IP>
```

Questo comando invia quattro pacchetti ICMP al server con l'indirizzo IP specificato.  

* **Esempio:** `ping google.com` verifica la connettività con il server di Google.

**2. Numero di Pacchetti:**

```
ping <indirizzo_IP> -c <numero_pacchetti>
```

Permette di specificare il numero di pacchetti ICMP da inviare. 

* **Esempio:** `ping 8.8.8.8 -c 10` invia dieci pacchetti al server DNS di Google.

**3. Tempo Timeout:**

```
ping <indirizzo_IP> -W <tempo_in_secondi>
```

Definisce il tempo massimo di attesa per una risposta da parte del server.

* **Esempio:** `ping 192.168.1.1 -W 2` attende un massimo di due secondi per ogni risposta.

**4. Tipo di Pacchetto:**

```
ping <indirizzo_IP> -T <tipo_pacchetto>
```

Permette di specificare il tipo di pacchetto ICMP da inviare (ad esempio, ECHO REQUEST o ECHO REPLY). 

* **Esempio:** `ping -T echo-request` invia un pacchetto ECHO REQUEST.

**5. Intervallo:**

```
ping <indirizzo_IP> -i <intervallo_in_millisecondi>
```

Definisce l'intervallo di tempo tra l'invio dei pacchetti ICMP.

* **Esempio:** `ping -i 100` invia un pacchetto ogni 100 millisecondi.



Questi sono solo alcuni esempi di comandi ping. Per una lista completa e dettagliata, consulta la documentazione del sistema operativo che stai utilizzando.
