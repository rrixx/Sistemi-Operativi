un insieme di processi è in deadlock se **ogni processo dell'insieme è in attesa** di un evento che può essere causato da un altro processo dell'insieme

per descriverlo si usano i **grafi di allocazione delle risorse** 
![[Pasted image 20260421161153.png|350]]

dati due processi, essi si trovano in uno stato di deadlock **se e solo se** si verificano le 4 condizioni:
1. [[mutua esclusione]] 
2. **possesso e attesa**: ogni processo che ha una risorsa può richiederne un altra
3. **impossibilità di prelazione**: una volta assegnata una risorsa non può essere sottratta
4. **attesa circolare**: in un gruppo di processi (P0, P1, ..., Pn) ognuno attende una risorsa posseduta dal successivo 

**TRATTAMENTO BLOCCO CRITICO**
- **prevenzione** 
	- statica: vincoli scelti a priori
	- dinamica: controllo del SO durante l'esecuzione
- **rilevazione / ripristino** il SO rileva il deadlock -> algoritmo di ripristino 