**VINCOLO DI PRECEDENZA**
![[Pasted image 20260421172444.png|422]]
![[Screenshot 2026-04-21 172402.png|425]]

**COMUNICAZIONE CON BUFFER DI CAPACITA 1**
![[Pasted image 20260421172536.png|419]]

**COMUNICAZIONE CON BUFFER DI CAPACITA N**
![[Pasted image 20260426093646.png|247]]
P: produttore
C: consumatore

_vincoli_: 
- produttore non può inserire se il buffer è pieno 
- consumatore non può prelevare se vuoto 

per la _sincronizzazione_ inseriti i due semafori:
- **spazio_disp**= indica gli elementi liberi del buffer (inizializzato a n)
- **msg_disp**= indica il numero di messaggi nel buffer (inizializzato a 0)
![[Pasted image 20260426094343.png|475]]


**PIU PRODUTTORI E CONSUMATORI** 
![[Pasted image 20260426094455.png|283]]

_vincoli_ aggiuntivi:
- solo un produttore alla volta
- solo un consumatore alla volta

si aggiungono _due semafori per la mutua esclusione_:
- **mutex1** per i produttori
- **mutex2** per i consumatori 
![[Pasted image 20260426094736.png|475]]

