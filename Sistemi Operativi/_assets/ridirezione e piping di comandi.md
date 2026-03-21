- ridirezione: **<,>,>>**
- piping: **|**  

**RIDIREZIONE** 

**ridirezione in output**: 
```shell
$ Comando > F
```
output del comando scritto nel file F

**ridirezione in append**
```shell
$ Comando >> F
```
output del comando scritto in coda al file 

**ridirezione in input**
```shell 
$ Comando < F
```
input del comando acquisito dal file


**PIPING**
```shell 
Comando1 | Comando2 | Comando3
```
consente di realizzare pipeline di comandi, i quali vegono eseguiti in modo **concorrente** 

## RIDIREZIONE IN OUTPUT: REALIZZAZIONE
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/wait.h>

main(int argc, char **argv)
{   int pid, fd, status;
    
    pid=fork();
    if (!pid) /* processo figlio: com1 */
    {   close(1); // chiusura dispositivo stdout
        fd=open(argv[2], O_WRONLY); //argv[2] sostituisce disp. di stdout
        execlp(argv[1], argv[1], (char *)0);
        exit(-1);
    }
    
    wait(&status);
    if((char)status!=0)
        printf("figlio term. per segnale%d\n", (char)status);
}
```

## RIDIREZIONE IN INPUT: REALIZZAZIONE
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/wait.h>

main(int argc, char **argv)
{   int pid, fd, status;
    
    pid=fork();
    if (!pid) /* processo figlio: com1 */
    {   close(0); // chiusura dispositivo stdout
        fd=open(argv[2], O_RDONLY); //argv[2] sostituisce il disp. di stdin
        execlp(argv[1], argv[1], (char *)0);
        exit(-1);
    }
    
    wait(&status);
    if((char)status!=0)
        printf("figlio term. per segnale%d\n", (char)status);
}
```