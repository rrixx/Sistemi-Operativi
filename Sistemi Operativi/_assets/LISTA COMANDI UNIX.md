```shell
# --- INFORMAZIONI DI SISTEMA E SESSIONE ---
date                    # Mostra data e ora corrente
who                     # Elenca gli utenti connessi al sistema
whoami                  # Mostra il proprio username
top                     # Monitoraggio processi in tempo reale
ps                      # Mostra i processi attivi dell'utente
passwd                  # Cambia la propria password
exit                    # Chiude la shell corrente (non di login)
logout                  # Chiude la shell di login (o CTRL+D)

# --- NAVIGAZIONE FILE SYSTEM ---
pwd                     # Stampa il percorso della directory corrente
cd                      # Torna alla Home directory
cd /percorso/assoluto   # Spostamento tramite percorso assoluto
cd ../percorso/relativo # Spostamento tramite percorso relativo
# .                     # Indica la directory corrente
# ..                    # Indica la directory padre

# --- LISTING E VISUALIZZAZIONE FILE (ls) ---
ls                      # Elenca i file nella directory corrente
ls -l                   # Formato lungo: permessi, proprietari, dimensioni
ls -a                   # Mostra anche i file nascosti (che iniziano con .)
ls -t                   # Ordina per data di ultima modifica
ls -u                   # Ordina per data di ultimo accesso
ls -r                   # Inverte l'ordine di visualizzazione
ls -F                   # Classifica i file (es. / per directory, * eseguibili)
man ls                  # Apre il manuale del comando ls (q per uscire)

# --- GESTIONE FILE E DIRECTORY ---
> file.txt              # Crea un file vuoto (o svuota uno esistente)
mkdir nome_dir          # Crea una nuova directory
rmdir nome_dir          # Elimina una directory (solo se vuota)
rm nome_file            # Elimina un file (operazione definitiva)
cp src dest             # Copia un file o directory
mv src dest             # Sposta o rinomina un file/directory

# --- LETTURA E MANIPOLAZIONE CONTENUTO ---
cat file.txt            # Visualizza tutto il contenuto del file
more file.txt           # Visualizza il file una pagina alla volta
grep "testo" file.txt   # Cerca una stringa dentro il file
wc -l file.txt          # Conta le linee (-w parole, -c caratteri)
cut -f1 -d: file.txt    # Estrae colonne/sezioni di testo

# --- PERMESSI E PROTEZIONE (chmod) ---
# Formato Ottale: R=4, W=2, X=1 (es. 7=rwx, 6=rw-, 5=r-x)
chmod 755 file          # U:rwx, G:r-x, O:r-x
chmod 644 file          # U:rw-, G:r--, O:r--
# Formato Simbolico: u=user, g=group, o=others, a=all
chmod u+x file          # Aggiunge esecuzione al proprietario
chmod a-w file          # Toglie scrittura a tutti
chown user file         # Cambia proprietario (solo root)
chgrp group file        # Cambia gruppo (solo root)
```
