```shell
anna@lab3-linux:~/esercizi$ vi segnali1.c
anna@lab3-linux:~/esercizi$ gcc segnali1.c
anna@lab3-linux:~/esercizi$ ./a.out&
[1] 313
anna@lab3-linux:~/esercizi$ kill -SIGUSR1 313
anna@lab3-linux:~/esercizi$ ricevuto sigusr1
anna@lab3-linux:~/esercizi$ kill -SIGUSR2 313
anna@lab3-linux:~/esercizi$ ricevuto sigusr2
anna@lab3-linux:~/esercizi$ kill -9 313
anna@lab3-linux:~/esercizi$
[1]+ Killed a.out
anna@lab3-linux:~/esercizi$
```