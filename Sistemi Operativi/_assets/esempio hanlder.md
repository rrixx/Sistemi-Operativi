```c 
#include <signal.h>
#include <stdio.h>

void handler(int);

main()
{ 
    if (signal(SIGUSR1, handler)==SIG_ERR)
        perror("prima signal non riuscita\n");
    if (signal(SIGUSR2, handler)==SIG_ERR)
        perror("seconda signal non riuscita\n");
    for (;;); //ciclo infinito (attesa segnali)
}

void handler (int signum)
{ 
    if (signum==SIGUSR1) printf("ricevuto sigusr1\n");
    else if (signum==SIGUSR2) printf("ricevuto sigusr2\n");
}
```

gestione segnale SIGCHLD, il segnale che il kernel invia al processo padre quando un figlio termina 

```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void handler(int);

main()
{ 
    int PID, i;
    signal(SIGCHLD,handler);
    PID=fork();
    
    if (PID>0) /* padre */
    { 
        for (i=0; i<10000000; i++) /* attività del padre..*/
            printf("il padre sta lavorando...\n");
        exit(0); 
    }
    else /* figlio */
    { 
        signal(SIGCHLD,SIG_DFL);
        for (i=0; i<1000; i++); /* attività del figlio..*/
        exit(1); 
    }
}

//definizione dell handler...
void handler(int signum){ //... }
```