## 1.  monitoraggio dei processi 
Questo script visualizza i processi di sistema. Se non viene fornito alcun argomento, mostra tutti i processi; altrimenti, mostra solo i primi $N$ processi specificati 

```bash 
#!/bin/bash

# Controlla se il primo argomento ($1) è una stringa vuota [cite: 1140]
if [ -z $1 ] 
then
    # Se non c'è argomento, mostra tutti i processi con dettagli (aux) [cite: 1142]
    ps aux 
else
    # Se c'è un numero N, mostra i primi N+1 processi (N + riga intestazione) [cite: 1144, 1145]
    # L'output di 'ps aux' viene passato (pipe) al comando 'head' [cite: 1144]
    ps aux | head -n $(expr $1 + 1) 
fi
```


## 2.  conteggio righe del file 
Lo script elenca i file in una directory e conta le loro linee, ordinandoli in modo crescente o decrescente


```bash 
#!/bin/bash

# Verifica che siano stati passati esattamente 2 argomenti ($#) 
if [ $# -ne 2 ]
then
    echo "SINTASSI: lines_counter.sh <directory> [up|down]"
    exit 1 # Esce con un codice di errore [cite: 1160]
fi

# Verifica se il primo argomento è effettivamente una directory [cite: 1161]
if [ -d $1 ]
then
    # Se il secondo argomento è "up", ordina in modo crescente [cite: 1162]
    if [ $2 = "up" ]
    then
        # Conta le linee di tutti i file nella directory e ordina numericamente (-n) [cite: 1164, 1165, 1167]
        wc -l $1/* | sort -n
    # Se il secondo argomento fosse "down", si aggiungerebbe l'opzione -r a sort
    fi
fi
```


## 3.  script di backup
Questo script crea copie di sicurezza. Se l'argomento è una directory, ne crea una copia ricorsiva; se è un file, ne crea cinque copie numerate

```bash
#!/bin/bash

# Controllo iniziale sul numero di argomenti [cite: 1172]
if [ $# -ne 2 ]
then
    echo "USAGE: backup.sh <filename> <backupstring>"
    exit 1 [cite: 1174]
fi

# Se il primo argomento è una directory [cite: 1175, 1176]
if [ -d $1 ]
then
    # Copia ricorsivamente (-R) la directory aggiungendo la stringa di backup [cite: 1177]
    cp -R $1 "$1_$2"
# Altrimenti, se è un file regolare [cite: 1179]
elif [ -f $1 ]
then
    # Esegue un ciclo da 1 a 5 [cite: 1182]
    for i in 1 2 3 4 5
    do
        # Crea 5 copie del file. I doppi apici permettono l'uso di variabili ($i, $2) 
        # ma impediscono l'espansione di caratteri jolly come '*' 
        cp $1 "$1_$i_$2"
    done
else
    # Messaggio di errore se l'input non è né file né directory [cite: 1184]
    echo "$1 should be a valid directory or file"
fi
```