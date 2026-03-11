```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

int ntimes = 0;

void handler(int signo)
{ 
    printf("Processo %d ricevuto #%d volte il segnale %d\n", getpid(), ++ntimes, signo);
}

int main ()
{ 
    int pid, ppid;
    signal(SIGUSR1, handler);
    
    if ((pid = fork()) < 0) /* fork fallita */
    {
        exit(1);
    }
    else if (pid == 0) /* figlio */
    { 
        ppid = getppid(); /* PID del padre */
        for (;;)
        { 
            printf("FIGLIO %d\n", getpid());
            sleep(1);
            kill(ppid, SIGUSR1);
            pause();
        }
    } 
    else /* padre */
    {
        for(;;) /* ciclo infinito */
        { 
            printf("PADRE %d\n", getpid());
            pause();
            sleep(1);
            kill(pid, SIGUSR1);
        }
    }
    return 0;
}
```

![[Screenshot 2026-03-11 113755.png]]
