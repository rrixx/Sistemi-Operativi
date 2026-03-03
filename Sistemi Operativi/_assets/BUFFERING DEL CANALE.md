ogni canale è caratterizzato da una _capacità_ che esprime il numero massimo di messaggi che può contenere, questi messaggi vengono messi in una coda FIFO

a seconda della capacità i buffering si classificano in: 
- **capacità nulla**: non vi è accodamento perché la coda non è in grado di gestire messaggi in attesa
- **capacità non nulla (limitata)**: esiste un limite N alla dimensione della coda
- **capacità infinita**: lunghezza della coda teoricamente infinita

a seconda della capacità del canale la send può essere 
- _Send sincrona_ con canale e capacita nulla, se il destinatario non è pronto a ricevere il destinatario attende
- _Send asincrona_ con canale e capacità non null, il mittente deposita il messaggio nel canale e prosegue l'esecuzione (send non sospensiva)
