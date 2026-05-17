Si consideri una toiette unica per uomini e donne. 
Si realizzi un'applicazione concorrente che gestisca l'accesso condiviso alla risorsa 

politica di sincronizzazione:
- non vi siano uomini e donne insieme nella toilette
- le donne hanno la priorità in accesso 

architettura:
- risorsa condivisa: Bagno con lock e Conditions 
- due Thread concorrenti: Uomo e Donna che cercano di accedere alla risorsa

## Monitor Toilet
```java
import java.util.concurrent.locks*

public class Toilet{
	
	private final int MAX=10 // capacità 
	int ND; //numero donne
	int NU; //numero uomini
	
	private Lock lock= new ReentrantLock();
	Condition codaD;
	Condition codaU; 
	
	int sospD;
	int sospU;
	
	public Toilet(){
	
		ND=0;
		NU=0;
		
		codaD = lock.newCondition();
		codaU = lock.newCondition(); 
		
		sospD=0;
		sospU=0;
	}
	
	// funzioni di acesso e uscita separate tra donne e uomini
	public void entraD(){
		
		lock.lock();
		
		try{
			
			while( NU>0 || ND == MAX){ //bagno con uomini o pieni
				
				codaD.await(); //attende
				sospD--;
			}
			
			ND++; //entra
		
		}finally{
			
			lock.unlock();
		}
	}
	
	public void entraU(){
	
		lock.lock();
		
		try{
		
			while( ND>0 || NU==MAX || sospD>0){ //bagno con donne, pieno o donne in attesa (prioritarie)
			
				sospU++;
				codaU.await(); //attende
				sospU--;
			}
			
			NU++; //entra
		
		}finally{
		
			lock.unlock();
		}
	}
	
	public void esceD(){
		
		lock.lock();
		
		ND--;
		
		if(sospD>0){ //donne in attesa
			
			codaD.signal(); 

 		}else if(sospU>0 && ND==0){ //uomini in attesa e bagno senza donne
 		
		 	codaU.signalAll(); //sveglia tutti
 		}
 		
 		lock.unlock();
	}
	
	
	public void esceU(){
	
		locl.lock();
		
		NU-- 
		
		if(sospD>0 && NU==0){ //donne in attesa e bagno senza uomini (entrata donne prioritaria)
		
			codaD.signalAll(); //sveglia tutte
		
		}else if(sospU>0 && sospD==0){ //uomini in attesa e nessuna donna in attesa
		
			codaU.sigal(); 
		}
		
		lock.unlock();
	}
}
```


## Thread Uomo
```java
import java.util.Random

public class Uomo extends Thread{
	
	Toilet t;
	Random r;
	
	public Uomo(Toliet T, Random R){
		
		this.t=T;
		this.r=R;
	}
	
	public void run(){
	
		try{
			
			Thread.sleep(r.nextInt(5)*500);
			
			t.entraU();
			
			Thread.sleep(r.nextInt(5)*1000);
			System.out.println("thread uomo "+ getName() + " in bagno");
			
			t.esceU();
		
		}catch(InterruptedException e){
			
			e.printStackTrace();
		}
	}
}
```

## Thread Donna
```java

import java.util.Random

public class DOnna extends Thread{
	
	Toilet t;
	Random r;
	
	public Donna(Toliet T, Random R){
		
		this.t=T;
		this.r=R;
	}
	
	public void run(){
	
		try{
			
			Thread.sleep(r.nextInt(5)*500);
			
			t.entraD();
			
			Thread.sleep(r.nextInt(5)*1000);
			System.out.println("thread donna "+ getName() + " in bagno");
			
			t.esceD();
		
		}catch(InterruptedException e){
			
			e.printStackTrace();
		}
	}
}

```


## classe Main
```java
import java.util.*

public class Bagno_Ristorante{
	
	public static void main(String[] args){
		
		final int NT=10; //numero thread
		
		Random r = new Random(System.currentTimeMillis());
		Toilet t = new Toliet();
		Uomo[] U = new Uomo[NT];
		Donna[] D = new Donna[NT];
		
		for(int i=0; i<NT; i++){
		
			U[i] = new Uomo(t, r);
			D[i] = new Donna(t, r);
 		}
 		
 		for(int i=0; i<NT; i++){
		
			U[i].start();
			D[i].start();
		}
		
		for(int i=0; i<NT; i++){
		
			U[i].join();
			D[i].join();
		}
	}
}

```