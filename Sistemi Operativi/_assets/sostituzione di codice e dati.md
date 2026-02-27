per differenziare il codice di due processo con una system call

**effetto principale**:
- vengono sostituiti codice ed eventuali argomenti di invocazione del processo chiamante, per essere sostituiti con _codice e argomenti del processo specificato come parametro_ della system call 

```c
int excel(char * pathname, char * arg0,..., char * argN, (char *)0);
```

- **pathname** : nome dell'eseguibile da caricare
- **arg0**: nome del programma
- **arg1,...., argN**: argomenti da passare al programma
- **(char * )0**: puntatore nullo che indica la fine degli argomenti 

N.B. excel è una chiamata senza ritorno, in caso di fallimento ritorna -1 e continua ad eseguire il codice iniziale, e la var di sistema **errno** assume il valore associato all'errore 

**esempio d'uso**
per differenziare il comportamento del figlio dal processo padre 

```c
pid = fork();

if (pid == 0) { /* figlio */
    printf("Figlio: esecuzione di ls\n");
    execl("/bin/ls", "ls", "-l", (char *)0);
    
    // Se execl fallisce, viene eseguito il codice seguente
    perror("Errore in execl");
    exit(1); 
}

if (pid > 0) { /* padre */
    // ...
    printf("Padre ....\n");
    exit(0); 
}

if (pid < 0) { /* fork fallita */
    printf("Errore in fork\n");
    exit(1); 
}

```

[[effetti excel() sull'immagine]] 

**effetti generali**:
- mantiene la stessa process structure (info relative al codice)
- ha **codice, dati globali, stack e heap** nuovi 
- riferisce un nuovo text 
- mantiene la stessa user structure e stack del kernel 

[[varianti system call exec()]]

