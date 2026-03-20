```c
#include 
...
main()
{ int fd1, fd2, fd3;
fd1=open(“/home/anna/ff.txt”, O_RDONLY);
if (fd1<0) perror(“open fallita”);
...
fd2=open(“f2.new”,O_WRONLY);
if (fd2<0)
{ perror(“open in scrittura fallita:”);
fd2=open(“f2.new”,O_WRONLY|O_CREAT, 0777);
/* è equivalente a:
fd2=creat(“f2.new”, 0777); */}
/*OMOGENEITA`: apertura dispositivo di output:*/
fd3=open(“/dev/prn”, O_WRONLY);
... }
```
