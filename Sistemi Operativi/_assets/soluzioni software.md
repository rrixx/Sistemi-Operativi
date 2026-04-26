
## **_SEMAFORI_**  
consentono di risolvere qualunque problema di sincornizzazione 
definizione:
==un semaforo è un intero non negativo a cui si può accedere solo tramite due operazioni atomiche p(s) e v(s) definite come segue== 

![[Pasted image 20260421170537.png|307]]
(atomiche quindi sezioni critiche), il valore del semaforo viene modificato da un solo processo alla volta

esempio 
![[Pasted image 20260421170710.png|323]]

**_realizzazione semafori_**
- valore interno: _value_
- coda con i descrittori dei processi in attesa: _Qs_ 
```c
typedef struct{ 
	unsigned int value; 
	queue Qs;
} semaphore;

void p(semaphore *s) {
	if (s->value==0)
	/* s->Qs descrittore processo inserito nella coda */
	else s->value--;
}

void v(semaphore *s) {
	if (/* Qs non e` vuota*/)
	else s->value++;
}
```

deato che p(s) e v(s) sono sezioni crfitiche, devono essere realizzate come operazioni atomiche --->  uso di _lock/unlock_ 

```c
// definizione della struttura del semaforo
typedef struct { 
    int value;      // valore del semaforo (contatore 0 o 1)
    queue Qs;       // coda dei processi sospesi
    int lock;       // variabile di lock per l'atomicità (inizializzata a 1)
} semaphore;

// operazione P (wait/sospensione)
void p(semaphore *s) {
    lock(s->lock);          // entrata in sezione critica per garantire l'atomicità
    if(s->value == 0) {
        unlock(s->lock);    // esce dalla sez. critica prima di sospendersi (evita deadlock)
        <Sospensione in Qs> // il processo viene messo in coda e sospeso
        lock(s->lock);      // rientra in sezione critica una volta risvegliato
    }
    else {
        s->value--;         // decrementa se la risorsa è disponibile
    }
    unlock(s->lock);        // uscita definitiva dalla sezione critica
}

// operazione V (signal/risveglio)
void v(semaphore *s) {
    lock(s->lock);          // inizio protezione atomica
    if (<Qs non è vuota>) {
        <risveglio processo da Qs> // se ci sono processi in attesa, ne risveglia uno
    }
    else {
        s->value++;         // altrimenti incrementa il valore del semaforo
    }
    unlock(s->lock);        // fine protezione atomica
}
```

[[esempi d'uso dei semafori ]] 


_**REALIZZAZIONE DI POLITICHE DI GESTIONE DELLE RISORSE**_
![[Pasted image 20260426095236.png|425]]
_politica_: un lettore aspetta solo se la risorgsa è gia stata assegnata ad un processo scrittore, dunque la priorità nell'accesso alla risorsa è dei lettori 

![[Pasted image 20260426095433.png|370]]
