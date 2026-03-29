```shell
ls ese*
# elenca i file i cui nomi iniziano con la stringa “ese”, seguita da un
# qualunque numero di caratteri.

ls [a-p,1-7]*[c,f,d]?
# elenca i file i cui nomi hanno come iniziale un carattere compreso tra 'a'
# e 'p' oppure tra 1 e 7, e il cui penultimo carattere sia 'c', 'f', o 'd‘

cat esempio.txt > out\*.txt
# Scrive il contenuto del file esempio.txt nel file di nome “out*.txt”.

ls *\**
# Elenca i file che contengono nel nome, in qualunque posizione, il
# carattere *
```