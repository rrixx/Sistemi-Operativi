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

# INVOCAZIONE:
# utente~$ ./somma.sh 

# OUTPUT:
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

