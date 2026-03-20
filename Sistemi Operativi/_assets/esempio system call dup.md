ridirezione standard output sulla pipe 
```c
#include <stdio.h>
#include <unistd.h>

main()
{   int pid, fd[2]; 
    char msg[3]="bye";
    
    pipe(fd);
    pid=fork();
    
    if (!pid) /* processo figlio */
    {   close(fd[0]);
        close(1); // chiudo disp. stdout
        dup(fd[1]); // ridirigo stdout sul lato di scrittura della pipe
        close(fd[1]); /* elim. seconda copia lato scritt.*/
        write(1, msg, sizeof(msg)); // scrivo su pipe
        close(1);
    } 
    else /* processo padre */
    {   close(fd[1]);
        read(fd[0], msg, 3);
        close(fd[0]);
    }
}
```


piping di due comandi senza argomenti
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

main(int argc, char **argv)
{   int pid1, pid2, fd[2], i, status;
    
    pipe(fd);
    pid1=fork();
    
    if (!pid1) /* primo processo figlio: com2 */
    {   close(fd[1]);
        close(0);
        dup(fd[0]); /* ridirigo stdin sulla pipe */
        close(fd[0]);
        execlp(argv[2], argv[2], (char *)0);
        exit(-1);
    } 
    else /* processo padre */
    {   pid2=fork();
        if (!pid2) /* secondo figlio: com1 */
        {   close(fd[0]);
            close(1);
            dup(fd[1]); /* ridirezione pipe-stdout */
            close(fd[1]);
            execlp(argv[1], argv[1], (char *)0);
            exit(-1);
        }
        
        for (i=0; i<2; i++)
        {   wait(&status);
            if((char)status!=0)
                printf("figlio terminato per segnale%d\n", (char)status);
        }
        exit(0);
    }
}
```
