> [!PDF|important] [[Sistemi e reti(Internetworking).pdf#page=118&selection=23,0,26,81&color=important|II protocollo IP, nelle versioni 4 e 6 si occupa dell’indirizzamento, della suddivi sione in pacchetti e del trasferimento dei dati che arrivano dal Transport Layer.]]
> > II protocollo IP, nelle versioni 4 e 6 si occupa dell’indirizzamento, della suddivisione in pacchetti e del trasferimento dei dati che arrivano dal Transport Layer.

> II protocollo IP, nelle versioni 4 e 6 si occupa dell’indirizzamento, della suddivisione in pacchetti e del trasferimento dei dati che arrivano dal Transport Layer. **IP è connectionless**, dunque consente a due host di scambiarsi PDU, denominate **IP *datagram***, senza stabilire una connessione.

**Datagram**: Il termine datagram è usato per indicare la PDU di un protocollo connectionless, come IP o UDP (protocollo di livello Transport).

---
Il protocollo IP **aggiunge ai dati (payload) un header, della lunghezza minima di 20 byte**, **per formare il pacchetto** (massimo 65.535 byte) **da inoltrare al livello Physical**. I campi più importanti dell'header sono rappresentati dagli indirizzi IP del mittente e del destinatario. [[Sistemi e reti(Internetworking).pdf#page=118&selection=76,0,78,1|figura1]]


