il SO SI occupa anche della realizzazione del file system sui dispositivi di memorizzazione secondaia quindi: 
- **allocazione blocchi fisici**
- **gestione dello spazio libero**
- **realizzazione dei descrittori** 

il blocco dunque è l'unita di allocazione dul disco ed esistono vari **METODI DI ALLOCAZIONE**:

**alliocazione contigua**
ogni file viene mappato su un insieme di blocchi contigui 
![[Screenshot 2026-03-17 103931.png|179]]  

**allocazione a lista concatenata**
i blocchi dove vengono mappati i file sono organizzati in una lista concatenata
![[Screenshot 2026-03-17 104059.png|191]]
alcuni SO la realizzano in modo più robusto, utilizzando la **tabella di allocazione dei file** in cui ogni elemento rappresenta un blocco 

**allocazione a indice**
i puntatori ai blocchi utilizzati per l'allocazione di un determinatp file sono concentrati in un solo _blocco indice_ per quel file (nell'allocazione a lista i puntatori sono distribuiti sul disco)
![[Screenshot 2026-03-17 104409.png|208]]

esistono SO con più metodi di allocazione
file piccoli -> allocazione contigua
file grandi -> allocazione a indice 


