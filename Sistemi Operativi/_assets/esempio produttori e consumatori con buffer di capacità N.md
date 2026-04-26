![[Pasted image 20260426104503.png|396]]

classe ==semaforo risorsa== 
```java
import java.util.concurrent.Semaphore;

public class risorsa {
    // Definizione buffer condiviso
    final int N = 30; // Capacità del buffer
    int lettura, scrittura; // Indici di lettura e scrittura
    int[] buffer;

    Semaphore sP; // Sospensione dei Produttori (posti liberi)
    Semaphore sC; // Sospensione dei Consumatori (messaggi disponibili)
    Semaphore sM1, sM2; // Semafori di mutua esclusione

    public risorsa() {
        lettura = 0;
        scrittura = 0;
        buffer = new int[N];
        sP = new Semaphore(N); // Inizializzato alla capacità N
        sC = new Semaphore(0); // Inizializzato a 0
        sM1 = new Semaphore(1); // Mutex per la scrittura
        sM2 = new Semaphore(1); // Mutex per la lettura
    }

    public void inserimento(int M) {
        try {
            sP.acquire(); // Attende che ci sia un posto libero
            sM1.acquire(); // Inizio sezione critica scrittura
            
            buffer[scrittura] = M;
            scrittura = (scrittura + 1) % N; // Buffer circolare
            
            sM1.release(); // Fine sezione critica scrittura
            sC.release(); // Incrementa i messaggi disponibili per i consumatori
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public int prelievo() {
        int messaggio = -1;
        try {
            sC.acquire(); // Attende che ci sia almeno un messaggio
            sM2.acquire(); // Inizio sezione critica lettura
            
            messaggio = buffer[lettura];
            lettura = (lettura + 1) % N; // Buffer circolare
            
            sM2.release(); // Fine sezione critica lettura
            sP.release(); // Incrementa i posti liberi per i produttori
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return messaggio;
    }
}
```

classe ==thread produttori== 
```java
public class threadP extends Thread {
    int i = 0;
    risorsa r; // Oggetto che rappresenta il buffer condiviso

    // Costruttore: riceve il riferimento alla risorsa comune
    public threadP(risorsa R) {
        this.r = R;
    }

    @Override
    public void run() {
        try {
            System.out.println("\nThread PRODUTTORE: il mio ID è: " + getName() + "..");

            while (i < 100) {
                sleep(100);        // Attesa di 100ms per simulare il tempo di produzione
                r.inserimento(i);  // Metodo critico: inserisce il dato nel buffer
                i++;
                System.out.println("\n" + getName() + ": inserito messaggio " + i);
            }
        } catch (InterruptedException e) {
            // Gestione dell'eccezione se il thread viene interrotto durante lo sleep
        }
    }
}
```

classe ==thread consumatori== 
```java
public class threadC extends Thread { // Consumatore
    int msg;
    risorsa r;

    // Costruttore: riceve lo stesso oggetto risorsa del produttore
    public threadC(risorsa R) {
        this.r = R;
    }

    @Override
    public void run() {
        try {
            System.out.println("\nThread CONSUMATORE: il mio ID è: " + getName() + "..");

            while (true) {
                // Metodo critico: preleva un messaggio dal buffer
                // Se il buffer è vuoto, questo thread rimarrà in attesa (wait)
                msg = r.prelievo(); 
                
                System.out.println("\n" + getName() + " consumatore ha letto il messaggio " + msg + "...");
            }
        } catch (InterruptedException e) {
            // Il thread termina se viene interrotto
        }
    }
}
```

classe con ==main== 
```java
import java.util.concurrent.*;

public class prodcons {
    public static void main(String args[]) {
        final int NP = 10; // num produttori
        final int NC = 10; // num consumatori
        
        threadP[] TP = new threadP[NP];
        threadC[] TC = new threadC[NC];
        
        risorsa R = new risorsa(); // creaz. buffer condiviso

        for (int i = 0; i < NP; i++)
            TP[i] = new threadP(R);

        for (int i = 0; i < NC; i++)
            TC[i] = new threadC(R);

        for (int i = 0; i < NP; i++)
            TP[i].start();

        for (int i = 0; i < NC; i++)
            TC[i].start();
    }
}
```