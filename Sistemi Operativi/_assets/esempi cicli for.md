```shell 
# --- 1. Iterazione su tutti i file della directory ---
for i in *; do
    echo "Sto elaborando il file: $i"
done

# --- 2. Iterazione su file che iniziano con 's' (Sostituzione di comando) ---
for i in `ls s*`; do
    echo "File che inizia per s: $i"
done
# NOTA: Oggi si preferisce scrivere: for i in s*; do ... done

# --- 3. Iterazione sulle parole di un file ---
for i in `cat file1`; do
    echo "Parola letta: $i"
done
# --- 4. Iterazione su una lista definita manualmente ---
for i in 0 1 2 3 4 5 6; do
    echo "Valore di i: $i"
done

```