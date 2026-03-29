```shell
awk '{ print $1, $3 }' file.txt
# Stampa il primo e il terzo campo di ogni riga, separati da uno spazio.

awk '/errore/ { print $2 }' log.txt
# Cerca le righe che contengono la parola "errore" (pattern) e ne stampa solo la seconda parola (azione).

awk -F: '{ print $1 }' /etc/passwd
# Cambia il separatore di campo (FS) usando i due punti (-F:) e stampa il primo campo. Ottimo per estrarre i nomi utente dai file di sistema Unix.

awk 'NF > 3 { print $0 }' file.txt
# Stampa l'intera riga ($0) SOLO se il numero di campi (NF) è maggiore di 3.

awk '{ print NR, $0 }' file.txt
# Stampa il numero di riga (NR) seguito dall'intera riga, numerando di fatto l'output.

awk '{ somma += $1 } END { print "Totale:", somma }' fatture.txt
# Legge la prima colonna di ogni riga, la somma in una variabile e, alla fine del file (END), stampa il risultato totale.
```