del tipo MLFQ
- 160 livelli di priorità 
- valore di riferimento _pzero_ che è >= o per i processi utente ordinari e < 0 per quelli di sistema
- ogni livello ha una coda Round Robin
- priorità decresce al crescere del tempo di uso della CPU
- l'utente può influire sulla priorità (diminuendola solamente) con il comando _nice_ 