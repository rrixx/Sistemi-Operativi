```c
#include 
main(){
	int fd,n; char buf[100];
	if(fd=open(“/home/miofile”,O_RDWR)<0)
	...;
	lseek(fd,-3,2); /* posizionamento sul terz’ultimo byte del file */
	...
}
```

