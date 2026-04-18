
```shell
# ==========================================================
# INFORMAZIONI DI SISTEMA E SESSIONE
# ==========================================================
date                    # Visualizza la data e l'ora corrente del sistema 
who                     # Elenca gli utenti attualmente connessi al sistema 
whoami                  # Restituisce lo username della sessione corrente 
top                     # Monitora in tempo reale i processi e l'uso delle risorse 
ps [opzioni]            # Mostra i processi attivi; 'aux' elenca tutti i processi 
passwd                  # Permette all'utente di cambiare la propria password di accesso 
exit                    # Termina la sessione di una shell (anche non di login) 
logout                  # Chiude la sessione della shell di login corrente 

# ==========================================================
# NAVIGAZIONE E FILE SYSTEM
# ==========================================================
pwd                     # Print Working Directory: stampa il percorso assoluto corrente [cite: 1880, 695]
cd [directory]          # Cambia directory di lavoro; senza argomenti torna alla home 
ls [opzioni] [file/dir] # Elenca i file e le cartelle nel direttorio specificato
# Opzioni ls comuni:
# -l (long format), -a (tutti inclusi i nascosti), -t (ordine cronologico), 
# -u (ordine per accesso), -r (ordine inverso), -F (classifica tipo file) 

# ==========================================================
# GESTIONE FILE E DIRECTORY
# ==========================================================
> nome_file             # Crea un file vuoto o sovrascrive uno esistente 
mkdir nome_directory    # Crea una nuova directory nel percorso specificato 
rmdir nome_directory    # Elimina una directory solo se è vuota 
rm nome_file            # Rimuove/elimina uno o più file [cite: 2232, 1047]
cp [opzioni] src dest   # Copia file o directory; '-R' copia ricorsivamente le cartelle 
mv src dest             # Sposta o rinomina file e directory 

# ==========================================================
# VISUALIZZAZIONE E MANIPOLAZIONE DATI
# ==========================================================
cat [file...]           # Visualizza l'intero contenuto di uno o più file di testo 
more [file...]          # Visualizza il contenuto di un file una schermata alla volta 
grep "stringa" [file]   # Ricerca una sequenza di caratteri specifica in un file
wc [opzioni] [file]     # Conta linee (-l), parole (-w) o caratteri (-c) 
cut -f[N] -d[sep] file  # Seleziona e stampa colonne specifiche con un delimitatore 
head -n [N]             # Mostra le prime N righe di un output o di un file 
sort [opzioni]          # Ordina le righe di testo; '-n' per ordinamento numerico 

# ==========================================================
# PERMESSI E PROPRIETÀ
# ==========================================================
chmod [mode] file       # Modifica permessi (R=4, W=2, X=1) in formato ottale o simbolico
chown utente file       # Cambia l'utente proprietario del file (richiede privilegi root)
chgrp gruppo file       # Cambia il gruppo proprietario del file (richiede privilegi root)

# ==========================================================
# UTILITÀ DELLA SHELL
# ==========================================================
man comando             # Apre il manuale elettronico per consultare la documentazione 
help                    # Visualizza la lista dei comandi integrati (builtin) della shell 
type comando            # Indica se un comando è definito internamente o esternamente 
echo [testo]            # Stampa il testo o le variabili sullo standard output 
expr [espressione]      # Valuta espressioni aritmetiche (es: somma tra variabili) 
apt-get install [pkg]   # Scarica e installa pacchetti software (es: Debian/Ubuntu) 
```