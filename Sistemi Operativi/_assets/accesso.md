il SO garantisce accesso on-line ai file e tipicamente le **operazioni sui file** sono:
- creazione
- lettura
- scrittura
- eliminazione dal file system

per migliorare l'efficienza in nella realizzazione di queste operazioni il SO 
- mantiene aperta in memoria la **tabella dei file aperti** che registra i file attualmente in uso
- fa il **memory mapping** dei file aperti, temporaneamente copiandoli in memoria centrale

a livello di _accesso_ i file sono _record logici_ ovvero unità di trasferimento logico
a livello di _dispositivo virtuale_ i file sono _blocchi_ ovvero unità di trasferimento fisico 

_dimensione blocco >> dimensione record logico_

_**METODI DI ACCESSO**_
è indipendente dal tipo di sipositivo usato e può essere di diverso tipo:

**accesso sequenziale**
il file è una sequenza di record logici
![[Screenshot 2026-03-17 102602.png|366]]
le operazioni sono del tipo readnext e writenext ed è necessario registrare la posizione corrente del puntatore al file, ogni operazione lo posizione sull elemento successivo

**accesso diretto** 
il file è un insieme di record logici numerati, e dunque si può accedere direttamente ad un record specificsandone il numero
le operazione sono del tipo read i, write i 

**accesso a indice**
ad ogni file viene associata una struttura dati contentente l'indice delle informazioni contenute, dunque per accedere ad un record si ricerca nell'indice usando una chiave 
![[Screenshot 2026-03-17 102950.png|330]]



