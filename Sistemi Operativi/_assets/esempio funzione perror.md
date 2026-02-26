```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

#define N 10 //ci saranno 10 processi figli 

int main()
{
    int pid[N], status, i, k;

    // Fase di creazione dei figli
    for (i = 0; i < N; i++)
    {
        pid[i] = fork();
        if (pid[i] == 0)
        {
            printf("figlio: il mio pid è: %d\n", getpid());
            exit(0); // Il figlio termina subito dopo la stampa
        }
    }

    // Fase di attesa di tutti i figli
    while(1) 
    {
        k = wait(&status);
        if (k < 0) 
        {
            // Quando non ci sono più figli da attendere, wait restituisce -1
            perror("wait fallita (non ci sono più figli)");
            exit(1);
        }
        else
        {
            printf("Terminato figlio %d \n", k);
        }
    }
    
    return 0;
}
```

Output perror: wait fallita: No child processes