realizzazione del comando ls 
```c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <unistd.h>
#include <string.h>

void miols(char name[])
{   DIR *dir; 
    struct dirent * dd;
    char buff[80];
    
    dir = opendir(name);
    while ((dd = readdir(dir)) != NULL) //finche la directory contiene ancora degli elementi 
    {   sprintf(buff, "%s\n", dd->d_name);
        write(1, buff, strlen(buff));
    }
    closedir(dir);
    return;
} 

main(int argc, char **argv)
{   if (argc <= 1)
    {   printf("Errore\n");
        exit(1);
    }
    miols(argv[1]);
    exit(0);
}
```

esplorazione di una gerarchia 
```c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <string.h>
#include <unistd.h>

void esplora (char *d, char *n);

main (int argc, char **argv)
{   if (argc != 3) {
        printf("Errore par.\n"); 
        exit(1);
    }
    if (chdir(argv[1]) != 0)
    {   perror("Errore in chdir");
        exit(1);
    }
    esplora(argv[1], argv[2]);
}

void esplora (char *d, char *f)
{   char nd[80]; 
    DIR *dir;
    struct dirent *ff;
    
    dir = opendir(d);
    while ((ff = readdir(dir)) != NULL)
    {   if ((strcmp(ff->d_name, ".") != 0) && (strcmp(ff->d_name, "..") != 0)) /* salto . e .. */
            if (chdir(ff->d_name) != 0) /* è un file */
            {   if (strcmp(f, ff->d_name) == 0)
                    printf("file %s nel dir %s\n", f, d);
            } 
            else /* abbiamo trovato un direttorio */
            {   strcpy(nd, d); 
                strcat(nd, "/");
                strcat(nd, ff->d_name);
                esplora(nd, f);
                chdir(".."); 
            } /* salgo 1 livello */
    }
    closedir(dir);
}
```