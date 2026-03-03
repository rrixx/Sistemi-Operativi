caratteristiche:
- la ready queue è gestita come una coda FIFO
- ad ogni processo la CPU viene allocata per un intervallo $\Delta$t 

(può essere visto come un estensione del FCFS con pre-emption periodica)

**problematiche**:
- dimensionamento del tempo: se $\Delta$t è piccolo, tempo di risposta ridotto ma tanti context switch; se $\Delta$t è grande context switch ridotti ma tempo di risposta più alto  
- trattamento equo di tutti i processi 
