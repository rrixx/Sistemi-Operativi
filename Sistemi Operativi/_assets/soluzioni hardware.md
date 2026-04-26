**_1. disabilitazione delle interruzioni durante le sezioni critiche_** 
- prologo: disabilitazione interruzioni
- epilogo: abilitazione interruzioni 
![[Pasted image 20260421164853.png|450]]
problemi:
- limitato a sezioni critiche eseguite sullo stesso processore
- elimina la possobilità di concorrenza
- insensibilità del sistema

precedentemente si è supposta la mutua esclusione tra lettura e scrittura in memoria
_istruzione test_and_set_ 
un istruzione macchina che consente una lettura e scrittura in modo indivisibile
```c
int test-and-set(int *a) { 
	int R; 
	R=*a; 
	*a=0; 
	return R; 
}
```

utilizzandola si può realizzare il meccanismo _Lock e Unlock_
```c
void lock(int *x) { 
	while (!*x); 
	*x=0; 
} 

void unlock(int *x) { 
	*x=1; 
}
```

-> **_2. soluzione con Lock e Unlock_**
- applicabile in ambiente multiprocessore
- attesa accettabile per sezioni corte
![[Pasted image 20260421165633.png|475]]
problemi di attesa attiva e non garantita assenza di starvation 

