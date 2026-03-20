
visualizzazione sull standard output del contenuto di un file
```c
#include 
main(){
	int fd,n;
	char buf[10];
	if((fd=open(“/home/miofile”,O_RDONLY))<0) {
		perror(“errore di apertura:”);
		exit(-1);
	}
	while ((n=read(fd, buf,10))>0)
		write(1,buf,n); /*scrittura su stdout */
	close(fd);
} 
```


comando mycp (copia del file di nome argv[1] nel file di nome argv[2])
```c
#include 
#include 
#define BUFDIM 1000
#define perm 0777
main (int argc, char **argv){
	 int status, infile, outfile, nread;
	char buffer[BUFDIM];
	if (argc != 3){ 
		printf (" errore \n"); exit (1); 
		}
	if ((infile=open(argv[1], O_RDONLY)) <0){ 
		perror(“apertura sorgente: “);
	exit(1); 
	} 
	if ((outfile=creat(argv[2], perm )) <0){ 
		perror(“apertura destinazione:”);
	close (infile); exit(1); 
	}
// copia:
	while((nread=read(infile, buffer, BUFDIM)) >0 ){ 
		if((write(outfile, buffer, nread))< nread){ 
			close(infile);
			close(outfile);
			exit(1);
		}
	}
	close(infile);
	close(outfile);
	exit(0);
}
```