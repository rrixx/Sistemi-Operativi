un processo può terminare :
- **involontariamente** ad esempio azioni illegali o interruzioni mediante segnale 
  (salvataggio dell'immagine nel core)
- **volontariamente** ad esempio dopo che esegue l'ultima istruzione o viene chiamata la funzione exit()

```c
void exit(int status); 
```
il parametro status permette di comunicare al padre informazioni sul suo stato di terminazione 

**effetti exit()**:
- chiusura file aperti non condivisi
- terminazione processo, se il processo terminante ha figli in esecuzione, il processo **Init li adotta**, mentre se il suo stato di terminazione non ancora è stato rilevato entra in **stato Zombie** con la system call wait() 

**parentela processi e terminazione**
![[Screenshot 2026-02-26 100056.png|425]]