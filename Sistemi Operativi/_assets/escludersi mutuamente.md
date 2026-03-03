ad esempio: 
due thread P1 e P2 hanno accesso ad una struttura condivisa organizzata a pila rispettivamente per inserire e prelevare dati. I thread utilizzano le operazioni Inserimento e Prelievo per depositare e prelevare i dati dalla pila

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

esecuzione concorrente 

![[Screenshot 2026-03-03 140731.png|425]]

pertanto se la risorsa è già utilizzata da un processo, l'altro dovrà attendere e riprenderà quando essa viene liberata