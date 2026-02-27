la funzione fork() consente ad un processo di creare uni figlio:
- padre e figlio condividono lo stesso codice
- il figlio eredita una copia dei dati del padre 

```c
 int fork(void); 
```

- non richiede parametri 
- restituisce un int che: 
	- vale 0 per il processo figlio 
	- per il padre è >0 e rappresenta il PID del figlio 
	- <0 in caso di errore 

**effetti della fork()**: 
- allocazione di una **nuova process structure** nella Process Table del processo figlio 
- allocazione di una **nuova user structure** contente la copia di quella del padre 
- allocazione dei **segmenti di dati e stack del figlio** nei quali vengono copiati dati e stack del padre
- aggiornamento del riferimento text al codice eseguito 

**relazione padre-figlio in UNIX**:
- **concorrenza**
- **spazio indirizzi duplicato** 
- **user structure duplicata**: il figlio nasce con lo stesso program counter del padre ed esegue l'istruzione immediatamente dopo la fork() 

``` c 
#include <stdio.h>
main() {
	int pid;
	pid = fork();
	if(pid==0){        //getpid() da il pid del processo che la chiama
		printf("sono il processo figlio! (pid: %d)\n", getpid());
	}
	else if(pid>0){
		printf("sono il processo padre: pid del figlio: %d\n", pid)
	}
	else printf("creazione fallita");
}
```

andranno dunque avanti due processi distinti 

**esempio esecuzioni differenziate** 

![[Screenshot 2026-02-27 113257.png|550]]