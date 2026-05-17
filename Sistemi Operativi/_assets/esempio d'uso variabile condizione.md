 
```java
monitor Risorsa() {
    boolean risorsa_libera = true;
    condition C;
    int turno = ...;

    entry void acquisizione(int id) {
        while (turno != id || risorsa_libera == false) {
            C.wait();
        }
        risorsa_libera = false;
    }

    entry void rilascio(int id) {
        risorsa_libera = true;
        <attribuzione nuovo valore a turno>
        C.signal();
    }
}
```