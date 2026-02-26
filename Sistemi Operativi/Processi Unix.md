caratteristiche del processo UNIX:
- **processo pesante** con codice **rientrante**, quindi dati non condivisi e codice condivisibile tra processi 
- modello **ad ambiente locale** (ad eccezione del codice) , quindi scambio di messaggi tra processi, 

![[Screenshot 2026-02-26 090710.png|147]]


**GERARCHIE PROCESSI UNIX**

![[Screenshot 2026-02-26 090718.png|375]]


**STATI DI UN PROCESSO UNIX** 
- **Init**: caricamento in memoria del processo e inizializzazione strutture dati del SO 
- **Ready**: processo pronto 
- **Running**: il processo usa la CPU 
- **Sleeping**: il processo è sospeso in attesa si un evento 
- **Terminated**: eliminazione di un processo dalle memoria e dal SO
- _**Zombie**_: processo terminato e in attesa che il padre ne rilevi lo stato di terminazione
- _**Swapped**_: il processo o parte di esso viene temporaneamente spostato in memoria secondaria 

![[Screenshot 2026-02-26 090730.png|425]]


**RAPPRESENTAZIONE DEI PROCESSI UNIX**
sostanzialmente il SO gestisce una struttura dati in cui sono sono contenuti i puntatori ai codici utilizzati, chiamata [[text table]] 

**il Process Control Block** (PCB) **in UNIX** è rappresentato da due strutture dati distinte:
- [[Process Structure]]: informazioni per gestione processi 
- [[User Structure]]: informazioni necessarie solo se il processo risiede in memoria centrale 

**IMMAGINE DI UN PROCESSO UNIX**
è l'insieme delle aree di memoria e strutture dati associate al processo, le due caratteristiche principali sono: 
- **Protezione**, infatti non è tutta accessibile in modalità user ma ha una parte kernel e una utente
- **Presenza in memoria centrale**: ogni processo può essere swappato ma non tutta l'immagine, infatti ha una parte swappable una non swappable

[[componenti Immagine di un processo UNIX]]

**_SYSTEM CALL PER GESTIONE DI PROCESSI_** 
- [[creazione di processi]]: **fork()**
- [[terminazione]]: **exit()**
- [[sospensione]] in attesa della terminazione di figli: **wait()**
- [[sostituzione di codice e dati]]: **exec()** 

**_GESTIONE ERRORI_** 
- in caso di fallimento ogni system call ritorna un **valore negativo**
- UNIX prevede la variabile di sistema **errno** alla quale il kernel assegna il codice errore generato dall'ultima system call, per interpretarne il valore si usa la funzione presente nella seguente libreria 
```c
	#include <sys/errno.h>
		perror("stringa") 
```

[[esempio funzione perror]] 