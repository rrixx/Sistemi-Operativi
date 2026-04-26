P1 e P2 hanno accesso ad un vettore stack formato da variabili che contengono la posizione (variabile top) dell'ultimo elemento della pila e possono inserire e prelevare dati 

```c
typedef ... item;
item stack[N];
int top=-1;

void Inserimento(item y)
{ 
    top++;
    stack[top]=y;
}

item Prelievo()
{ 
    item x;
    x= stack[top];
    top--;
    return x;
}
```

l'esecuzione contemporanea porterebbe ad un uso scorretto della risorsa 
![[Pasted image 20260421155925.png|323]]
