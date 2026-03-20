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