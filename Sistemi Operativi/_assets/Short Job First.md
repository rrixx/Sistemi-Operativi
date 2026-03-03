quando il processo è nella ready queue, viene fatta una stima della lunghezza del prossimo processo CPU burst e quello con la minor stima viene selezionato 

![[Screenshot 2026-03-03 100516.png]]

SJF può essere sia pre-emptive che non 

i**problema sostanziale**: sta nella difficoltà di fare una stima del tempo di utilizzo di un processo 

**Stimare la lunghezza di un processo CPU burst**
si basa sui precedenti CPU burst di quel processo, la tecnica utilizzata è quella del _exponential averaging_ (tecnica ricorsiva) 

![[Screenshot 2026-03-03 100931.png|348]]
ogni termine ha meno peso del termine precedente 
