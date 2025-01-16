La suddivisione degli indirizzi in classi può creare un grosso spreco di indirizzi.

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=139&selection=23,0,41,62&color=yellow|Per cercare di porre rimedio a sprechi e carenze, in attesa dell’IPv6, nel 1993 è stato introdotto un nuovo schema di indirizzamento, la CIDR (Classiess Inter Domain Routing, pronunciata “saider”), anche nota come supernetting perché crea una super rete composta da più reti. In pratica la CIDR non applica subnetting ed elimina il concetto di classe di indirizzi (classiess)]]
> > Per cercare di porre rimedio a sprechi e carenze, in attesa dell’IPv6, nel 1993 è stato introdotto un nuovo schema di indirizzamento, la CIDR (Classiess Inter Domain Routing, pronunciata “saider”), anche nota come supernetting perché crea una super rete composta da più reti. In pratica la CIDR non applica subnetting ed elimina il concetto di classe di indirizzi (classiess)

Supponiamo di dover indirizzare 1.500 host e che quindi un indirizzo in classe C non basti (28 - 2 = 254) e uno in classe B sia eccessivo (216 - 2 = 65.534).

Prendiamo allora 6 indirizzi in classe C consecutivi:
1° 200.45. 8.0    11001000.00101101.**00001**0==00==.00000000
2° 200.45. 9.0    11001000.00101101.**00001**0==01==.00000000 
3° 200.45.10.0   11001000.00101101.**00001**0==10==.00000000 
4° 200.45.11.0   11001000.00101101.**00001**==011==.00000000 
5° 200.45.12.0   11001000.00101101.**00001**==100==.00000000 
6° 200.45.13.0   11001000.00101101.**00001**==101==.00000000

Ciascuno di loro consentirà di indirizzare 254 host avendo l'ultimo ottetto interamente libero per gli host, per un totale di 254 x 6 = 1.524 host, quindi misuratamente oltre le richieste di pianificazione.

La maschera verrà settata al valore:
255.255.248.0 = 11111111.11111111.==11111==000.00000000

> [!PDF|yellow] [[Sistemi e reti(Internetworking).pdf#page=140&selection=22,0,28,8&color=yellow|Con la CIDR non è corretto parlare di subnet mask, in quanto non esistono sot toreti e non viene fatto il subnetting. È invece corretto far riferimento a una ma schera per l’intera rete costituita dal blocco di indirizzi IP di rete consecutivi. Tale maschera prende il nome di netmask.]]
> > Con la CIDR non è corretto parlare di subnet mask, in quanto non esistono sot toreti e non viene fatto il subnetting. È invece corretto far riferimento a una ma schera per l’intera rete costituita dal blocco di indirizzi IP di rete consecutivi. Tale maschera prende il nome di netmask.

---
[[VLSM]]