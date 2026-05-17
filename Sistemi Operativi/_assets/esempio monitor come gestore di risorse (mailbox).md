comunicazione tra processi mediante un buffer di dimensione N 

- struttura dati -> monitor (send e recieve mutuamente esclusive) 
- monitor -> buffer dei messaggi, gestito in modo ciscolare
- processi Produttori inseriscono messaggi con la **funzione entry Send definita nel monitor** 
- processi Consumatori prelevano messaggi con la **funzione entry Recieve definita nel monitor** 

![[Pasted image 20260517101524.png|405]]

vincoli di struttura:
- un produttore non può inserire se il buffer è pieno
- un consumatore non può prelvare se il buffer è vuoto

**SEMANTICA: signal&wait**

```java
monitor buffer_circolare{
	
	messaggio buffer[N];
	
	int contatore=0; 
	int testa=0;
	int coda=0;
	
	condition non_pieno;
	condition non_vuoto;
	
	//funzioni entry
	
	entry void send(messaggio m){
		
		if (contatore == N){
			non_pieno.wait;
		}
		buffer[coda]=m;
		coda=(coda + 1) % N;
		++contatore;
		non_vuoto.signal
	}
	
	entry messaggio recieve(){
	
		messaggio m;
		if( contatore == 0 ){
			 non_vuoto.wait;
		}
		m=buffer[testa];
		testa=(testa + 1) % N;
		--contatore;
		non_pieno.signal
		
		return m;
	}
}

```

**SEMANTICA: signal&continue**

```java
monitor buffer_circolare{

	messaggio buffer[N];
	
	int contatore=0;
	int testa=0;
	int coda=0;
	
	condition non_pieno;
	condition non_vuoto;
	
	//funzoni entry 
	
	entry void send(messaggio m){
		while(contatore==N) { //condizione testata con while
			non_pieno.wait;
		}
		buffer[coda]=m;
		coda=(coda + 1) % N;
		++contatore;
		non_vuoto.signal
	}
	
	entry messaggio recieve(){
		messaggio m;
		whille(contatore==0){ //condizione testata con while
			non_vuoto.wait
		}
		
		m=buffer[testa];
		testa=(testa + 1) % N;
		--contatore;
		non_pieno.signal
		
		return m;
	}
}
```