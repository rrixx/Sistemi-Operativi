i processi possono muoversi tra queste code a seconda della loro storia:
- priorità bassa --> alta  se in attesa da molto tempo
- priorità alta --> bassa se hanno utilizzato già molto tempo di CPU

esempio con 3 code

![[Screenshot 2026-03-03 102630.png|256]]

**funzionamento**: 
un processo entra in Q0 e quando acquisisce la CPU ha 8ms per usarla, altrimenti si sposta in Q1 dove dispone per 16ms della CPU, se non termina va in Q2 che (a differenza di Q0 e Q1 che sono code Round Robin) segue la politica FCFS
