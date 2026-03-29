Script che risponde “si” se invocato con “si” e un numero <= 24
```shell
#!/bin/bash

if test "$1" = "si" -a "$2" -le 24
then 
    echo sì  # Eseguito se il test è VERO
else 
    echo no  # Eseguito se il test è FALSO (es. $1 non è "si" oppure $2 > 24)
fi           # Fine del blocco if

# VERSIONE STANDARD
#!/bin/bash

if [ "$1" = "si" -a "$2" -le 24 ]; then
    echo "sì"
else
    echo "no"
fi
```

Script che verifica che un argomento si stato inizializzato
```shell
if test $1; then 
    # test $1 -> Verifica se la stringa $1 NON è vuota (lunghezza > 0)
    echo OK
    # Eseguito se l'utente ha passato almeno un argomento allo script
else 
    echo "Almeno un argomento"
    # Eseguito se lo script è stato lanciato senza argomenti ($1 è vuoto)
fi
```