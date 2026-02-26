contiene le seguenti informazioni:
- stato processo
- puntatori alle aree dati e stack associati al processo
- riferimento indiretto al codice 
- info di scheduling (priorità, tempo di CPU, etc...)
- riferimento al processo padre (PID)
- info relative alla gestione di segnali 
- puntatore al processo successivo nella coda dei processi
- puntatore alla User Structure 

tutte le Process Structure sono contenute in un vettore gestito dal SO, chiamato **Process Table** 

![[Screenshot 2026-02-26 092325.png|354]]
