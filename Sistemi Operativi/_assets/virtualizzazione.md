virtualizzare il sistema significa presentare all’utilizzatore una visione delle risorse del sistema diversa da quella reale  

![[Screenshot 2026-02-24 105126.png|600]]

l'obiettivo delle macchine virtuali è quello di disaccoppiare il comportamento delle risorse hardware e software tramite la :
- **virtualizzazione dei dati** semplificando un oggetto fisico in uno stratto (virtuale) 
- **virtualizzazione delle istruzioni** utilizzando un linguaggio di alto livello 

**VIRTUALIZZAZIONE DI SISTEMI DI ELABORAZIONE** 
la macchina fisica viene trasformata in N interfacce, ognuna delle quali è una replica della macchina fisica dotata di : 
- tutte le istruzioni (privilegiate e non) 
- risorse di sistema (memoria, dispositivi di I/O)
su ogni macchina virtuale è possibile installare ed eseguire un sistema operativo

il software che realizza la virtualizzazione è il **Virtual Machine Monitor** (VMM)

una singola piattaforma viene condivisa da più sistemi operativi ognuno dei quali è installato su una diversa macchina virtuale 

![[Screenshot 2026-02-24 110054.png]]

il VMM è il mediatore e l'hardware alla base garantisce **isolamento tra le VM e stabilità del sistema** 

1. **VMM di Sistema** 

![[Screenshot 2026-02-24 110243.png]]

HOST= piattaforma sulla quale si realizzano le macchine virtuali (comprende la macchina fisica e il VMM)
GUEST= macchi a virtuale (comprende le applicazioni e sistema operativo)

2. **VMM ospitato**  
il VMM viene installato come un'applicazione sul SO esistente e accede all'hardware tramite le [[system call]] del SO su cui è installato 

![[Screenshot 2026-02-24 110542.png]]


**VANTAGGI VIRTUALIZZAZIONE**
- **uno o più SO sulla stessa macchina**
- **isolamento degli ambienti di esecuzione** che permette di effettuare testing e costituiscono un ambiente idealmente sicuro 
- **consolidamento HW** abbattendone costi, anche amministrativi 
- **gestione facilitata delle macchina** in quanto possono essere create e amministrate con estrema facilita