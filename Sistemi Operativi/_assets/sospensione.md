per rilevare lo stato di terminazione di un processo, il padre usa la system call wait()

```c
int wait(int * status) 
```
- il parametro **status** è l'indirizzo della variabile dove viene salvato lo stato di terminazione del figlio 
- il risultato è il PID del processo terminato oppure un cod. errore <0 

**effetti della wait()**:
- il processo che la chiama può avere figli:
	- se tutti i figli non ancora terminano il processo sospende finché non termina il primo 
	- se almeno un figlio è terminato e si trova in stato Zombie, la wait() ritorna immediatamente il suo stato di terminazione 
- se non esiste nessun figlio la wait() torna errore <0 

**Rilevazione dello stato**
nell'ipotesi in cui lo stato sia un intero a 16 bit: 
- se il byte meno significativo di status è zero, il più significativo rappresenta lo stato di terminazione (terminazione volontaria, ad esempio con exit)
- in caso contrario, il byte meno significativo di status descrive il segnale che ha terminato il figlio (terminazione involontaria)

```c
//.....
main()
{
    int pid, status;
    pid = fork();
    
    if (pid == 0)
    {
        printf("figlio");
        exit(0);
    }
    else 
    { 
        pid = wait(&status); //status è un indirizzo!!!
        printf("terminato processo figlio n.%d", pid);
        
        if ((char)status == 0) //byte meno significativo == 0
            printf("term. volontaria con stato %d", status >> 8);
        else //byte meno significativo != 0
            printf("terminazione involontaria per segnale %d\n",(char)status);
    }
}
```

ci sono delle macro definite in _<sys/wait.h>_ per l'analisi dello stato di terminazione, come:
- **WIFEXITED(status)** che restituisce true se il processo figlio è terminato **volontariamente** e in questo caso la macro **WEXITSTATUS(status)** restituisce lo **stato di terminazione** 
- **WIFSIGNALED(status)** che restituisce true se il processo è terminato **involontariamente** e in questo caso la macro **WTERMSIG(status)** restituisce il **numero del segnale che causa la terminazione** 

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

main()
{
    int pid, status;
    pid = fork();

    if (pid == 0)
    {
        printf("sono il figlio\n");
        exit(0);
    }
    else 
    { 
        pid = wait(&status);
        
        if (WIFEXITED(status))
            printf("Terminazione volontaria di %d con stato %d\n", pid, WEXITSTATUS(status));
        else if (WIFSIGNALED(status))
            printf("terminazione involontaria per segnale %d\n", WTERMSIG(status)); 
    }
}
```


_FUNZIONE waitpid()_

sintassi: 
```c
#include<sys/wait.h> //libreria 

int waitpid(int pid, int *status, int options);
```
restituisce il pid del figlio terminato o -1 in caso di errore


- **pid**  indica quale processo in particolare il padre dovrà aspettare (se passato -1 si  comporta come la wait normale )
- **status** è il puntatore alla variabile interna (come nella wait normale)
- **options** permette di  cambiare il comportamento della funzione, passando 0  la funzione è bloccante, quindi il padre si ferma e aspetta pazientemente finché quel figlio non termina
