i processi cooperanti non sono tenuti a conoscersi reciprocamente, ma si scambiano dei messaggi tramite una _mailbox_ che funge da contenitore di messaggi 

```c
send(Mailbox, msg)
```
si scambiano la mailbox 

**proprietà**: 
- il canale può essere associato a più di due processi (mailbox molti-a-molti o porta)
- per ogni coppia di processi possono esistere più canali 
