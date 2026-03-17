è lo strumento che consente di organizzare i file all'interno del file system, si possono contenere a vicenda e consentono di localizzare file su memorie di massa

si possono effettuare **operazioni su directory**:
- creazione/cancellazione di directory
- aggiunta/cancellazione di file
- listing 
- attraversamento 
- ricerca di file in directory 

la loro **struttura logica** puo variare a seconda del SO, gli schemi possono essere:
- _a 1 livello_: una sola directory per ogni file system, presenta problemi di unicitò e multiutenza
![[Screenshot 2026-03-17 100753.png|381]]

- _a 2 livelli_ in cui la directory principale copntirne una directory per ogni utente
![[Screenshot 2026-03-17 100758.png|375]]

- _ad albero_: organizzazione gerearchica ad N livelli 

![[Screenshot 2026-03-17 100804.png|400]]

- _a grafo acilico_ estende quello ad albero con possibiltà di inserire link differenti allo stesso file
![[Screenshot 2026-03-17 100810.png|450]]
