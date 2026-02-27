![[Screenshot 2026-02-27 114226.png|450]]

- ogni utente può interagire con la shell tramite i comandi 
- ogni comando è nel file system (come eseguibile)
- per ogni comando **shell genera un processo figlio dedicato all'esecuzione del comando** 

si hanno 2 possibili comportamenti
1. **esecuzione in foreground** : padre in attesa terminazione figlio 
```shell
ls -l pippo
```
2. **esecuzione in background** : padre con esecuzione concorrente al figlio 
```shell
	ls -l pippo &
```

