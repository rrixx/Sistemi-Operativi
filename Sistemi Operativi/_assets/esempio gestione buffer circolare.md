## classe del Monitor
```java
public class Mailbox{
	
	//dati
	ptivate int[] contenuto;
	private int contatore;
	private int testa;
	private int coda; 
	
	private Lock lock=new ReentratLock();
	private Condition non_pieno= lock.newCondition();
	private Condition non_vuoto= lock.newCondition();
	
	//costruttore
	public Mailbox(){
	
		contenuto= new int[N];
		contatore=0;
		testa=0;
		coda=0;
	}
	
	// metodi entry 
	public int preleva() throws InterruptedException {
	
		int elemento; 
		
		lock.lock() // inizio mutua esclusione
		try{
			
			while(contatore==0){
				non_vuoto.await();
			}
			
			elemento=contenuto[testa];
			testa=(testa + 1) % N;
			--contatore
			non_pieno.signal(); // notifica che non è pieno il buffer
		
		}finally { // blocco finally dopo il try che rilascia la mutua esclusione
		
			lock.unlock();
		}
		
		return elemento;
	}
	
	void deposita(int valore) throws InterruptedException {
		
		lock.lock(); //inizio mutua esclusione
		try{
		
			while(contatore==N){
				non_pieno.await();
			}
			
			contenuto[coda]=valore;
			coda=(coda + 1) % N;
			++contatore 
			non_vuoto.signal(); // notifica che non è vuoto il buffer
		
		} finally{ // blocco finally dopo il try che rilascia la mutua esclusione
			
			lock.unlock();
		}
	}
}
```


## classe dei Thread
```java
public class Produttore extends Thread{

	int messaggio;
	Mailbox m; 
	
	public Produttore(Mailbox M){
		this.m=M;
	}
	
	public void run(){
		
		while(1){
			//produce messaggi ...
			m.deposita(messaggio);
		}
	}
}

public class Consumatore extends Thread{
	
	int messaggio;
	Mailbox m;
	
	public Consumatore(Mailbox M){
		this.m=M;
	}
	
	public void run(){
		
		while(1){
			messaggio=m.preleva();
			//usa il messaggio...
		}
	}
}

```


## classe di Main
```java
public class BufferMonitor{
	
	public static void main(String args[]){
		
		Mailbox M = new Mailbox();
		Consumatore C = new Consumatore(M);
		Produttore P = new Produttore(M);
		
		C.start();
		P.start(); 
		
		//... 
	}
}
```