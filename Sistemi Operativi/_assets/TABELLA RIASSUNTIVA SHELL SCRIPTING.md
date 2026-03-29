```shell
# --- 1. VARIABILI E ASSEGNAZIONE ---
VAR="valore"        # Assegnazione (ATTENZIONE: no spazi prima/dopo =)
echo $VAR           # Espansione/Uso della variabile
read NOME COGNOME   # Legge input e lo divide nelle variabili
readonly COSTANTE=5 # Variabile non modificabile

# --- 2. PARAMETRI POSIZIONALI (Argomenti dello script) ---
$0                  # Nome dello script eseguito
$1, $2, ... $9      # Argomenti passati (es: ./script.sh arg1 arg2)
${10}, ${11}        # Argomenti dal decimo in poi (richiedono parentesi)
$#                  # Numero totale di argomenti passati
$*                  # Tutti gli argomenti come stringa unica "arg1 arg2 arg3"
$@                  # Tutti gli argomenti come lista separata (più sicuro)
$?                  # Exit status dell'ultimo comando (0 = Successo, 1+ = Errore)
$$                  # Process ID (PID) dello script corrente

# --- 3. COMANDI DI MANIPOLAZIONE PARAMETRI ---
shift               # Fa scalare i parametri a sinistra ($2 diventa $1, scarta $1)
set A B C           # Sovrascrive i parametri correnti: ora $1=A, $2=B, $3=C

# --- 4. CALCOLI E SOSTITUZIONI ---
RES=`expr $A + $B`  # Vecchia sintassi (backticks) per calcoli
RES=$(expr $A + $B) # Nuova sintassi (consigliata)
RES=$((A + B))      # Espansione aritmetica nativa Bash (migliore per performance)
OUT=$(ls)           # Command Substitution: salva l'output di un comando in una variabile

# --- 5. IL COMANDO TEST [ ... ] ---
# Nota: [ ] è un alias di test. Richiede spazi dopo [ e prima di ]
# Stringhe:
[ "$A" = "$B" ]     # Uguale
[ "$A" != "$B" ]    # Diverso
[ -z "$A" ]         # Vero se la stringa è vuota
[ -n "$A" ]         # Vero se la stringa NON è vuota

# Numeri:
[ $A -eq $B ]       # Equal (Uguale)
[ $A -ne $B ]       # Not Equal (Diverso)
[ $A -gt $B ]       # Greater Than (Maggiore)
[ $A -ge $B ]       # Greater or Equal (Maggiore o uguale)
[ $A -lt $B ]       # Less Than (Minore)
[ $A -le $B ]       # Less or Equal (Minore o uguale)

# File:
[ -f file ]         # Esiste ed è un file regolare
[ -d dir ]          # Esiste ed è una directory
[ -r file ]         # Leggibile (-w scrivibile, -x eseguibile)

# --- 6. STRUTTURE DI CONTROLLO ---

# IF / ELSE
if [ condizione ]; then
    # comandi se vero
elif [ altra_condizione ]; then
    # comandi se vero
else
    # comandi se falso
fi

# CASE (Pattern Matching)
case $VARIABILE in
    "si"| "SI" | "S") 
        echo "Hai detto sì" ;;
    "no") 
        echo "Hai detto no" ;;
    *) 
        echo "Input non valido" ;; # Caso di default
esac

# FOR (Cicli)
for i in 1 2 3; do echo $i; done        # Lista manuale
for f in *.txt; do cat $f; done        # Su file (Globbing)
for p in $(cat lista); do echo $p; done # Su parole di un file

# WHILE (Cicla finché la condizione è vera)
while [ $CONT -lt 10 ]; do
    echo $CONT
    CONT=$((CONT + 1))
done

# --- 7. LOGICA E INIBIZIONE ---
# Operatori logici DENTRO [ ]
# -a (AND), -o (OR), ! (NOT)
# Operatori logici TRA comandi
# && (Esegui se precedente OK), || (Esegui se precedente FALLITO)

'testo'             # Apici singoli: protezione TOTALE (testo puro)
"testo $VAR"        # Doppi apici: protegge spazi ma permette espansione di $ e `
\                   # Backslash: protegge il singolo carattere successivo
```