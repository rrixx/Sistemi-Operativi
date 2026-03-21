caratteristiche:
- unidirezionale
- molti a molti: piu processi possono spedire/ricevere attraverso la stessa pipe
- capacità limitata, gestione in modo FIFO
- OMOGENEITA’ con i FILE in accesso, infatti si usano le stesse system call 

[[COMUNICAZIONE INDIRETTA]] tramite mailbox

![[Screenshot 2026-03-20 161719.png|475]]

**bidirezionalità**: 
uno stesso processo può **sia depositare che prelevare messaggi dalla pipe** 

![[Screenshot 2026-03-20 161803.png|400]]
