![[Pasted image 20260320171928.png|242]]

```c
#include <stdio.h>
#include <unistd.h>

main()
{   int pid;
    char msg[]="ciao babbo";
    int fd[2];
    
    //creazione pipe
    pipe(fd);
    pid=fork();
    
    if (pid==0)
    {   /* figlio */
	    //si aggancia al lato di scrittura
        close(fd[0]);
        write(fd[1], msg, 10);
        ...
    }
    else /* padre */
    {   //si aggancia al lato di lettura 
	     close(fd[1]);
        read(fd[0], msg, 10);
        ...
    }
}
```