[[LISTA COMANDI UNIX]]
i comandi in Unix si comportano come **filtri**, ovvero programi che da un input producono risultati su uno o più output 

_comandi shell filtri_: 
```shell
grep <pattern> [...]
# Ricerca di testo. Input: (lista di) file. Output: video

tee <file> [...]
# «Sdoppia» l’input scrivendolo sia su file, sia su video

sort <options> [...]
# Ordina alfabeticamente le linee. Output: video

rev [...]
# Inverte l’ordine delle linee di file. Output: video

cut [-options] [file...]
# Seleziona colonne da file. Output: video

head [-options] [file...]
# Filtra la «testa» del file. Output: video

tail [-options] [file...]
# Filtra la «coda» del file. Output: video

```

**_RIDIREZIONE DI INPUT E OUTPUT_**
è possibile fasre in modo che non si legga/scrive da stdin/stdout ma da file senza cambiare il comando:
- comando < file_input
- comando > file_output (nuovo o sovrascritto)
- comando >> file_output (scrittura in append)
 
[[esempi ridirezione input e output]]

**_PIPING DI COMANDI_**
l'output di un comando può essere rediretto (diventare input) di un altro comando
si realizza con il carattere ' | ' :  comando1 | comando2 | comando3

## comando AWK
permette di fare delle ricerche di testo ed eseguire delle azioni
```shell
awk '<pattern> { azione }' [file...]
```
- _pattern_ specifica quando eseguire l'azione
- _azione_ definisce cosa fare 
[[esempi comando awk]] 


**_METACARATTERI_**
caratteri speciali 
- _*_  ->  una qualunque stringa 0 o più caratteri in un nome di file 
- _?_  -> un qualunque carattere in un nome di un file
- [zfc] -> un qualunque carattere compreso tra quell insieme, si possono esprimere anche intervalli es. [a-f]
- _#_  -> commento fino a fine riga
- \  -> escape: indica di non interpretare il carattere successivo come speciale 
[[esempi metacaratteri]]


**_VARIABILI NELLA SHELL_** 
in ogni shell è possibile definire variabili con nome e valore 
- _VAR_ nome della variabile
- _$VAR_ valore della variabile 
assegnamento: _nomevariabile=$nomevariabile_ (senza spazi)
[[esempi variabili nella shell]]   

**valutazione di espressioni** 
per valutare un espressione si usa il comando _expr_ che stampa sullo stout il valore dell'espressione passata come argomento (spazi importanti)
[[esempio valutazione di espressione]] 

è possibile utilizzare i caratteri _‘‘_ (backquote) per racchiudere un espressione che indica un valore ad esempio:
```shell
echo risultato: 'expr 5 + 1'
# risultato: 6
```
 

**_SHELL SCRIPTING_**
è possibile creare dei file che contengono comandi da eseguire in sequenza (.sh) 
```shell
#!/bin/bash file somma.sh
A=5
B=8
echo A=$A, B=$B
C=expr $A + $B
echo C=$C
D=`expr $A + $B`
echo D=$D

# ESECUZIONE
# utente~$ ./somma.sh
# A=5, B=8
# ./somma.sh: line 6: 5: command not found (mancano gli '' per assegnare expr)
# C=
# D=13
```

**_FLUSSO ESECUZIONE SHELL_** 
passi che la shell fa nel momento in cui viene invocato un comando 
![[Pasted image 20260329112237.png|475]]

**prima dell'esecuzione**
- individua eventuali redirezioni e piping
- la shell principale crea un clone (fork()), in questo processo figlio la shell cerca tutti i caratteri speciali e li traduce (**ESPANSIONE**) 
**esecuzione** 
- dopo aver tradotto i caratteri speciali la shell si sostituisce con il programma da lanciare passanfo i parametri tradotti

l'**ESPANSIONE** si articola in vari passaggi: 
1. **sostituzione di comandi** : esegue prima i comandi tra backquote ''
2. **sostituizione delle variabili**: cerca il simbolo $ legge il nome della variabile e lo sostituisce con il valore
3. **metacaratteri**: cerca i caratteri jolly e li usa per cercare nella directory corrente i nomi dei file, sostituendoli 

a volte tuttavia è necessario evitare che determinati caratteri vengano trattati in un certo modo, per questo è possibile l'**INIBIZIONE DELL'ESPANSIONE**:
- **protezione singola** \ (backslash): annulla il signigicato speciale del carattere immediatamente successvo
- **protezione forte** _''_ : qualsiasi cosa scritta al loro interno viene considerata testo puro 
- **protezione debole** _""_ : proteggono il testo da metacaratteri dei file ( * o ?) ma permettono la traduzione di variabilo ($), eseguire comandi ('') e usare i backslash ( \ ) 

**_REALIZZAZIONE DI FILE COMANDI_**
un file comandi è una sequenza di comandi e può comprendere:
- controllo di flusso (if, else, for)
- variabili
- passaggio di argomenti

i comandi contenuti in ogni file vengono eseguiti da una shell dedicata, infatti per ogni comando la shell (principale) crea un processo dedicato alla sua esecuzione 

**scelta della shell**
la prima riga di un file comandi deve specificare la shell che si vuole utilizzare 
```shell
#!<shell voluta>

#!/bin/bash
```
se assente viene scelta la shell di preferenza dell'utente 

**assegnamento variabili**
```shell
#!/bin/bash  
name=Mario #NO SPAZI
echo hello $name!

# hello Mario
```

**passaggio di argomenti**
gli argomenti sono variabili posizionali:
- $0 rappresnta il comando stesso
- $1 rappresenta il primo argomento (... $n)
```shell
# file: hello
#!/bin/bash 
echo hello $1 and $2!

# ESECUZIONE:
# utente~$ ./hello Anna Lucia
# hello Anna Lucia!
```

# comando SHIFT
fa scorrere gli argomenti verso sinistra, $0 viene mantenuto mentre $1 perso
```shell 
# file: hello
#!/bin/bash

echo "hello $1, $2 and $3!"
shift
echo "hello $1, $2 and $3!"

# ESECUZIONE:
# utente~$ ./hello uno due tre quattro
# hello uno, due and tre!
# hello due, tre and quattro!
```

# comando SET
riassegna gli argomenti $1 ... $n sovrascivendoli 
```shell
# file: hello
#!/bin/bash

echo "hello $1, $2 and $3!"
set Pluto Pippo Paperino
echo "hello $1, $2 and $3!"

# ESECUZIONE:
# bash-2.05:~$ ./hello Daniela Luca Paolo
# hello Daniela, Luca and Paolo!
# hello Pluto, Pippo and Paperino!
```

**variabili notevoli**:
- _$*_ insieme di tutte le variabili posizionali
- _$#_ numero di argomenti passati ($0 escluso)
- _$ $_ pid del processo in esecuzione
- _$?_ valore (int) restituito dall'ultimo comando eseguito

**NB** il comando per restituire il pid da risultati diversi a seconda di come viene chiamato il comando

**$?** può essere utilizzato per controlli di flusso successivo, in quanto lo stato vale 0 in caso di successo e > 0 in caso di errore 

# comandi READ e ECHO
per leggere e scrivere da stdin e stdout
```shell 
read var1 var2 var3

echo "var1 contiene $var1 e var2 contiene $var2"
```

# comando TEST
per la valutazione di un espressione
```shell
test[expression]

# ESEMPIO
SOT@studente:~$ test A = A #SPAZI NECESSARI 
SOT@studente:~$ echo $?
0

SOT@studente:~$ test A = B
SOT@studente:~$ echo $?
1
```
ritorna **0 se è true, != 0 se è false** 

**test rilevanti**
```shell 
# --- TEST SU FILE E DIRECTORY ---
test -f nome_file     # file esiste ed è un file regolare (non una cartella)
test -d nome_dir      # argomento esiste ed è una directory
test -e nome_file     # file esiste (indipendentemente dal tipo)

# --- TEST SUI PERMESSI ---
test -r nome_file     # file esiste ed è leggibile (read)
test -w nome_file     # file esiste ed è scrivibile (write)
test -x nome_file     # file esiste ed è eseguibile (execute)

# --- TEST SU STRINGHE ---
test -z "$stringa"    # stringa è vuota (lunghezza zero)
test -n "$stringa"    # stringa NON vuota (lunghezza maggiore di zero)
test "$s1" = "$s2"    # stringhe identiche
test "$s1" != "$s2"   # stringhe diverse

# --- TEST SU NUMERI (INTERI) ---
test $val1 -eq $val2  # equal
test $val1 -ne $val2  # not equal
test $val1 -gt $val2  # greater than
test $val1 -ge $val2  # greater or equal
test $val1 -lt $val2  # less than
test $val1 -le $val2  # less or equal

# --- OPERATORI LOGICI (PER COMBINARE I TEST) ---
test cond1 -a cond2   # AND
test cond1 -o cond2   # OR
test ! cond1          # NOT
```

# alternativa a test: \[ .... \] 
presnta esattamente la stessa semantica
```shell
#verifica se è una directory
test -d mydir
[ -d mydir ]   #SPAZI FONDAMENTALI 

#uguaglianza tra stringhe
test $a = "a_string" 
[ $a = "a_string" ]   

#verifica se <= 3 
test $a -le 3 
[ $a -le 3 ]
```

# keyword di linguaggio: \[\[ ... \]\] 
(come if, for, ...) 
vantaggi:
- si possono usare gli op. logici &&, || 
- si possono usare > < solo per confrontare stringhe 
- si possono usare i metacatartteri nella condizione 
- si può usare l'operatore _=~_ per fare confronti complessi 

# strutture di controllo 
![[Screenshot 2026-03-29 154820.png|450]]
**NB** le keyword o a capo o dopo il separatore
[[esempi struture di controllo]] 

**per eseguire più comandi** 
![[Pasted image 20260329155521.png|301]]
[[esempio struttura di controllo con più comandi]] 

**alternativa multipla**
![[Pasted image 20260329155806.png|450]]
**NB** si possono usare i metacaratteri per fare matching
[[esempi alternativa multipla]] 

**cicli enumerativi**
![[Pasted image 20260329160437.png|264]]
scrivendo _for i_ si itera con i valori di $* 
[[esempi cicli for]] 

**cicli non enumerativi**
con _while_ o _until_ 
![[Pasted image 20260329160806.png|328]] 


[[TABELLA RIASSUNTIVA SHELL SCRIPTING]]
