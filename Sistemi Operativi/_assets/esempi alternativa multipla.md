Lettura risposta
```shell
read risposta 
case $risposta in 
	S* | s* | Y* | y* ) echo “riposta positiva”;; # DOPPIO ;;
	* ) echo “riposta negativa”;; esac
```

Aggiunge il contenuto a un file
```shell
# Utilizzo: ./append.sh [file_sorgente] file_destinazione

case $# in
  # CASO 1: Un solo argomento fornito ($# = 1)
  # Lo script legge dallo Standard Input (quello che scrivi in tastiera)
  # e lo aggiunge (>>) al file indicato come $1.
  1) cat >> $1 ;;

  # CASO 2: Due argomenti forniti ($# = 2)
  # Legge dal primo file ($1) e ne appende il contenuto 
  # alla fine del secondo file ($2).
  2) cat < $1 >> $2 ;;

  # CASO DEFAULT (Qualsiasi altro numero di argomenti)
  # Stampa un messaggio di errore sull'uso corretto ed esce
  # con codice 1 (segnalando un fallimento).
  *) echo "uso: append [in_file] out_file"; exit 1 ;;
esac
```