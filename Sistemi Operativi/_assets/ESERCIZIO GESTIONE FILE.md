Realizzare un programma in C che implementi uno schema di comunicazione e sincronizzazione tra due processi (padre e figlio) sfruttando un file temporaneo come canale dati e i segnali Unix per coordinare gli accessi. 

**Specifiche del programma:**

- **Ruoli dei processi:** Il processo **figlio** assume il ruolo di mittente, mentre il **padre** è il destinatario.
    
- **Struttura dei dati:** Lo scambio prevede un numero prefissato di messaggi (es. 10 messaggi), ciascuno di lunghezza costante (es. 15 byte).
    
- **Sincronizzazione:** Gli accessi al file devono essere rigorosamente sincronizzati tramite l'invio e la ricezione di segnali (es. `SIGUSR1`, `SIGUSR2`), affinché il padre legga solo dopo la scrittura del figlio, e il figlio scriva il messaggio successivo solo dopo la lettura del padre.
    
- **Astrazione:** Le operazioni di scrittura (`write`) e lettura (`read`) devono essere incapsulate in due apposite funzioni personalizzate: `send` e `receive`.
    
- **Condivisione delle risorse:** * Il file temporaneo deve essere creato e aperto **prima** della chiamata a `fork()`, in modo che padre e figlio condividano lo stesso _I/O pointer_.
    
    - Al termine della comunicazione, il file temporaneo deve essere rimosso dal file system tramite la chiamata `unlink`.



```c
#include <signal.h> /* uso i segnali*/
#include <fcntl.h>  /* uso i file*/
#include <stdio.h>  /* per manipolare i messaggi*/
#include <unistd.h>
#include <string.h>
#include <stdlib.h>

#define max 10 /* numero di messaggi */
#define dim 15 /* dimensione messaggio */

typedef char msg[dim];
int fd; /* file descriptor*/
int pid, ppid; /* id figlio e padre */
int i=0; /* contatore dei messaggi */
msg buff;

void send(msg m);
void receive(msg *m);
void ricevuto(int signo);
void OK_to_send(int signo);
void fine(int signo);

main()
{   int cont=1;
    
    fd=creat("mailbox.tmp", 0777); /*creaz. File temp. */
    close(fd);
    fd=open("mailbox.tmp",O_RDWR); /*apertura file */
    signal(SIGUSR1, ricevuto); /* sblocco receive*/
    
    pid=fork(); /*figlio eredita fd: I/O pointer condiviso*/
    if (pid==0) /*codice figlio: mittente*/
    {   ppid=getppid();
        signal(SIGUSR1, OK_to_send); /* sblocco send */
        signal(SIGUSR2, fine); /* sblocco e fine comunic. */
        
        for(;;)
        {   sprintf(buff, "Ciao babbo %2d\n",cont++ );
            send(buff);
        }
    } 
    else if (pid>0) /* codice padre */
    {   for(i=0; i<max; i++)
            receive(&buff);
    }
} /* fine main */

void send(msg m) 
{   int n;
    
    lseek(fd,0,0); /*reset dell’I/O pointer*/
    n=write(fd, m, dim); /*stampa*/
    sleep(1);
    kill(ppid, SIGUSR1); /* avverto il padre: MESSAGGIO RICEVUTO*/
    pause(); /* send "sincrona" */
    
    return;
}

void receive(msg *m)
{   int status;
    
    pause();
    lseek(fd, 0,0); /* reset dell’I/O pointer */
    read(fd, m, 15); /* lettura dal file */
    write(1, m, 15); /* VERIFICA: stampa su stdout il msg.*/
    sleep(1);
    
    if (i!=max-1)
        kill(pid,SIGUSR1); /* ancora messaggi: OK_TO_SEND */
    else
    {   close(fd); /*chiusura file*/
        kill(pid, SIGUSR2); /* ultimo messaggio: FINE */ 
    }
    
    return;
}

void fine(int signo)
{   char buff[25]= "FINE\n";
    
    close(fd); /* chiusura file*/
    write(1,buff , strlen(buff)); /* stampa */
    unlink("mailbox.tmp"); /* cancell. file */
    exit(0); 
}

void ricevuto(int signo) /* arrivo mess */
{   char buff[25]= "ricevuto...\n";
    
    write(1,buff , strlen(buff)); /* stampa */
}

void OK_to_send(int signo) /* segnale OK per invio nuovo messaggio */
{   char buff[25]= "..fine receive.\n";
    
    write(1,buff , strlen(buff)); /* stampa */
}
```

**osservazioni**:
- file come mailbox
- un messaggio alla volta con sincronizzazione stretta 



