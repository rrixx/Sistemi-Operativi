assunzione di base: hardware garantisce la mutua esclusione solo su lettura e scrittura di una singola parola in memoria 

**_soluzione 1_**
_(A,B)_ classe di sezioni critiche
_libero_ variabile logica associata alla classe 
![[Pasted image 20260421163254.png|400]]
(entrambi i processi in sezione critica: violazione del requisito 1)

**_soluzione 2_**
_(A,B)_ classe di sezioni critiche
_turno_ varibile associata alle classi e asume val 1 e 2 
![[Pasted image 20260421163407.png|400]]
(impone un vincolo di alternanza: violazione del requisito 2)

**_soluzione 3_** 
_(A,B)_ classe di sezioni critiche
_busy1_, _busy2_ variabili associate alle classi inizializzate a false
![[Pasted image 20260421163604.png|400]]
(deadlock: violazione requisito 3)

**_soluzione 4: Algoritmo di Dekker_**
soddisfa tutti i requisiti
_busy1_, _busy2_ indicano che il processo vuole entrare in sezione critica
_turno_ indica a chi passare in caso di conflitto 
![[Pasted image 20260421163853.png|400]]
prima dell'esecuzione ogni processo controlla la variabile turno, in caso indichi se stesso esso entra in sezione critica, altrimenti aspetta

**_soluzione 5: Algoritmo di Peterson_** 
le variabili sono le stesse dell'algoritmo di Dekker
![[Pasted image 20260421164431.png|400]]
come l'algoritmo di Dekker ma senza while annidati e tutto in un unica condizione 

nonostante questi algoritmi funzionino, si resa in attesa in un while -> **attesa attiva** e **starvation** (non garantito di  accedere in un tempo finito)



