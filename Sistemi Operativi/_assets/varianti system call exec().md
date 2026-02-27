- _l_: argomenti da passare al programma indicati in una **lista** terminata da null -> _execl()_ 
```c
execl("/bin/ls", "ls", "-l", (char *)0);
```
-   _p_: il nome del file eseguibile viene ricercato nel path passato (cerca da solo il file nel path) -> _execlp()_
```c
   execlp("ls", "ls", "-l", (char *)0);
```

-  _v_: gli argomenti da passare al programma vengono  specificati mediante un **vettore** nei parametri   -> _execv()_  
```c
	char *args[] = {"ls", "-l", NULL};
	 execv("/bin/ls", args); 
```

-  _e_: la system call riceve un vettore **envp[]** che rimpiazza l'environment del processo chiamante -> _execle()_ 
```c
  char *env[] = {"USER=studente", "PATH=/bin:/usr/bin", NULL}; 
  execle("/bin/ls", "ls", "-l", (char *)0, env);
```


**esempio co execve()** 
```c
int execve(char *pathname, char *argV[], char * env[]);
```

- pathname= nome dell eseguibile da caricare
- argV= vettore con gli argomenti del programma da eseguire
- env= vettore variabili d'ambiente da sostituire 

```c
//NUOVE VARIABILI DA PASSARE 

char *env[] = {"USER=paolo", "PATH=/home/paolo/d1", (char *)0 
char *argv[] = {"ls", "-l", "pippo", (char *)0};

int main() 
{
    int pid, status;
    pid = fork();

    if (pid == 0) 
    {
        /* Processo figlio */
        execve("/bin/ls", argv, env);
        
        /* Se execve fallisce */
        perror("exec fallita a causa dell’errore:");
        exit(1);
    } 
    else if (pid > 0) 
    {
        /* Processo padre */
        pid = wait(&status); /* gestione dello stato.. */
    } 
    else 
    {
        /* Errore nella fork */
        perror(" fork fallita a causa dell’errore:");
    }
}
```