```c 
/* Invocazione: provastat nomefile */
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

main(int argc, char *argv[])
{   struct stat sb;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s \n", argv[0]);
        exit(1); }
    if (stat(argv[1], &sb) == -1) {
        perror("stat");
        exit(1);} 
    printf("Tipo del file:\t");
    if (S_ISREG(sb.st_mode)) printf("file ordinario\n");
    if (S_ISBLK(sb.st_mode)) printf("block device\n");
    if (S_ISCHR(sb.st_mode)) printf("character device\n");
    if (S_ISDIR(sb.st_mode)) printf("directory\n");
    printf("I-number:\t%ld\n", (long) sb.st_ino);
    printf("Mode:\t%lo (octal)\n", (unsigned long) sb.st_mode);
    printf("numero di link:\t%ld\n", (long) sb.st_nlink);
    printf("Proprietario:\tUID=%ld GID=%ld\n",(long) sb.st_uid,(long) sb.st_gid);
    printf("I/O block size:\t %ld bytes\n", (long) sb.st_blksize);
    printf("dimensione del file:\t%ld bytes\n", (long) sb.st_size);
    printf("Blocchi allocati: \t%ld\n",(long ) sb.st_blocks);
    exit(0);
}
```  

