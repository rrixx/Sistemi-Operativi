
al messaggio viene associato l'identificatore del processo destinatario

```c
send(Proc, msg);
```

il canale é: 
- creato automaticamente
- bidirezionale 
```c
  //P0
  send(query, P1); 
  
  //P1
  send(answ, P0); 
```

esempio produttore-consumatore 

**simmetrica**: destinatario fa il naming esplicito del mittente

![[Screenshot 2026-03-03 120227.png|450]]

**asimmetrica**: il destinatario non è obbligato a conoscere l’identificatore del mittente

![[Screenshot 2026-03-03 120350.png|475]]
