Un’azienda elettronica produce schede a microprocessore. La produzione di ogni scheda avviene in due fasi diverse: 
1) Assemblaggio: in questa fase avviene l’assemblaggio automatico dei diversi componenti; 
2) Inscatolamento: le schede assemblate vengono introdotte in scatole di capacita N.

Si supponga di affidare ognuna delle 2 fasi a un thread distinto incaricato di controllare la macchina automatica dedicata alla realizzazione di quella particolare fase. Utilizzando i semafori, si realizzi una politica di sincronizzazione che tenga conto dei seguenti vincoli: 
- l’inscatolamento puo essere attivato soltanto quando N nuovi prodotti sono stati assemblati 
- il thread dedicato all’assemblaggio non possa effettuare una nuova fase di assemblaggio se vi sono ancora MAX schede da inscatolare (MAX > N). 
- la soluzione dovra consentire un soddisfacente grado di concorrenza tra i threads.

classe ==risorsa==
```java
import java.util.concurrent.Semaphore;

public class risorsa {
    final int max = 15;    // Capacità massima di stoccaggio per pezzi assemblati
    final int N = 4;      // Capacità di una scatola (pezzi necessari per il confezionamento)
    int pronti;           // Contatore dei pezzi assemblati pronti
    int i;

    Semaphore sA;  // Spazio disponibile per nuovi pezzi (inizializzato a max)
    Semaphore sI;  // Numero di scatole pronte per essere confezionate (inizializzato a 0)
    Semaphore sM;  // Mutua esclusione per l'accesso alle variabili condivise (inizializzato a 1)

    public risorsa() {
        sA = new Semaphore(max); // Gestisce i posti liberi nel magazzino
        sI = new Semaphore(0);   // Gestisce il segnale di "scatola pronta"
        sM = new Semaphore(1);   // Mutex per proteggere la variabile 'pronti'
        pronti = 0;
    }

    /**
     * Metodo chiamato dal thread che deposita un pezzo assemblato
     */
    public void nuovoA() {
        try {
            sA.acquire();       // Verifica che ci sia spazio (max 15)
            sM.acquire();       // Entra in sezione critica

            pronti = pronti + 1;
            
            // Ogni N pezzi (4), segnala che una scatola può essere confezionata
            if (pronti % N == 0) {
                sI.release();
            }

            sM.release();       // Esce dalla sezione critica
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    /**
     * Metodo chiamato dal thread che preleva N pezzi per confezionare una scatola
     */
    public void nuovaS() {
        try {
            sI.acquire();       // Attende che ci sia una scatola pronta (ogni N pezzi)
            sM.acquire();       // Entra in sezione critica

            pronti = pronti - N; // Rimuove N pezzi dal magazzino
            
            // Libera N spazi nel magazzino per i produttori
            for (i = 0; i < N; i++) {
                sA.release();
            }

            sM.release();       // Esce dalla sezione critica
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

classe ==threadA assemblatore==
```java
public class threadA extends Thread { // Definizione Assemblatore
    int i = 0;
    int da_produrre;
    risorsa r;

    // Costruttore: riceve il riferimento alla risorsa e il numero di pezzi da produrre
    public threadA(risorsa R, int pezzi) {
        this.r = R;
        this.da_produce = pezzi;
    }

    @Override
    public void run() {
        try {
            System.out.println("\nThread ASSEMBLAGGIO: il mio ID è: " + getName());
            
            while (i < da_produrre) {
                sleep(100);       // Simula il tempo di assemblaggio
                r.nuovoA();       // Tenta di depositare un nuovo pezzo nella risorsa
                i++;
                System.out.println("\n" + getName() + ": nuovo assemblato...." + i);
            }
        } catch (InterruptedException e) {
            // Gestione dell'interruzione
        }
    }
}
```

classe ==thread inscatolatore==
```java
public class threadS extends Thread { // Thread che inscatola
    int i, scatole = 0;
    risorsa r;

    // Costruttore: riceve il riferimento alla risorsa condivisa
    public threadS(risorsa R) {
        this.r = R;
    }

    @Override
    public void run() {
        try {
            System.out.println("\nThread INSCATOLAMENTO: il mio ID è: " + getName() + "..");
            
            while (true) {
                // Tenta di prelevare un blocco di N pezzi
                // Se non ce ne sono a sufficienza, il thread si sospende su sI.acquire()
                r.nuovaS(); 
                
                sleep(100); /* Durata simulata dell'operazione di inscatolamento */
                scatole++;
                
                System.out.println("\n" + getName() + " inscatolamento " + scatole + "...");
            }
        } catch (InterruptedException e) {
            // Il thread termina se viene interrotto
        }
    } 
}
```

clase con ==main==
```java
public class supplychain {
    public static void main(String args[]) {
        // 1. Istanza della risorsa condivisa (gestita tramite semafori)
        risorsa R = new risorsa();

        // 2. Istanza del thread Assemblatore (produce 1000 pezzi)
        threadA TA = new threadA(R, 1000);

        // 3. Istanza del thread Inscatolatore
        threadS TS = new threadS(R);

        // 4. Avvio dei thread: iniziano a lavorare in parallelo sulla risorsa R
        TA.start();
        TS.start();
    }
}
```