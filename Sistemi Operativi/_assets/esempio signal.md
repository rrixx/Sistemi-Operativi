```c
#include <signal.h>

void gestore(int);

int main()
{
    ...
    signal(SIGUSR1, gestore); /*SIGUSR1 gestito */
    ...
    signal(SIGUSR1, SIG_DFL); /*USR1 torna a default */
    signal(SIGKILL, SIG_IGN); /*errore! SIGKILL non è ignorabile */
    ...
}
```