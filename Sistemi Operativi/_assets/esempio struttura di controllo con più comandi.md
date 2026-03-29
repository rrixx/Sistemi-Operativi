```shell
if ls; cat u; then
    # L'if esegue PRIMA 'ls' (elenca i file)
    # POI esegue 'cat u' (legge il file "u")
    # L'if valuta SOLO l'Exit Status dell'ULTIMO comando della lista (cat u)
    echo ok
else
    # Se l'ultimo comando (cat u) fallisce (es. il file non esiste), 
    echo error
fi

# ESEMPIO DI OUTPUT
# bash-2.05:~$ ./testscript
# file1 f2 f3 pippo.txt           <-- Risultato di 'ls' (successo)
# cat: u: No such file or directory <-- Errore di 'cat' (fallimento)
# error                           <-- Output del blocco 'else'
``` 
