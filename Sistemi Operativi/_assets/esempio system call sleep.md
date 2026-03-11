```c
/* provasleep.c */
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
#include <stdlib.h>

void stampa(int signo)
{ 
    printf("risvegliato dal segnale %d !!\n", signo);
}

main()
{ 
    int k;
    signal(SIGUSR1, stampa);
    k=sleep(1000);
    printf("Mancavano ancora %d sec..\n", k);
    exit(0);
}
```