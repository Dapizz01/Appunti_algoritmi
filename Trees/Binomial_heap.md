# Heap binomiali
## Caratteristiche
Complessità unione: $\boldsymbol{\Theta(\log(n))}$
Complessità inserimento nodo: $\boldsymbol{\Theta(\log(n))}$
Complessità estrazione nodo minimo: $\boldsymbol{\Theta(\log(n))}$
Complessità estrazione nodo: $\boldsymbol{\Theta(\log(n))}$
Complessità riduzione chiave: $\boldsymbol{\Theta(\log(n))}$
Complessità trasformazione in array ordinato: $\boldsymbol{\Theta(n\log(n))}$

## Definizione
Uno heap binomiale è una lista di [[Binomial_tree|alberi binomiali]] tali che:
- Per ogni dimensione $K$ c'è al più un albero binomiale di dimensione $K$;
- I nodi contengono chiavi ordinate, all'interno di ogni albero binomiale, secondo le regole di uno [[Heap|heap]].

![Esempio di heap binomiale](https://i.stack.imgur.com/QYvTi.jpg)
*Esempio di heap binomiale*

#### Struttura di un nodo
Un nodo di un albero binomiale possiede diversi campi:
- **Parent**: puntatore al nodo padre;
- **Key**: è il valore contenuto nel nodo;
- **Dimension**: indica la dimensione dell'albero di cui si è radice;
- **Child**: puntatore al figlio sinistro (per accedere al figlio destro bisogna visitare il figlio sinistro e poi visitarlo attraverso Sibling);
- **Sibling**: punta al nodo pari livello destro.

![Rappresentazione di un nodo](https://media.geeksforgeeks.org/wp-content/uploads/Binomial-Heap-node.jpg)
*Rappresentazione di un nodo (in figura, dimension = degree e left = child)*

## Unione di heap binomiali
L'algoritmo per l'unione di heap binomiali può essere comparato alla somma di numeri binari, in particolare:
- se uno heap binomiale ha un albero binomiale di dimensione $K$, allora considero il $K$ bit del numero binario come $1$.
- altrimenti, considero il $K$ bit del numero binario come $0$.

Vengono uniti gli heap ordinati in base alla loro dimensione.

// immagine

Si possono distinguere 3 casi:
1. Il caso 1 è corrispondente alla somma binaria $(0) + 1 + 1 = 0$ con il riporto di $1$. Ovvero, ci sono 2 alberi binomiali della stessa dimensione, che vengono accorpati in uno solo di dimensione maggiore (ovvero il riporto) mentre non ci sono più alberi binomiali con la loro dimensione originale.
2. Il caso corrisponde a $(1) + 1 + 1 = 1$ con il riporto di $1$. In questo caso c'è il riporto dalla somma precedente e viene creato un nuovo albero binomiale di dimensione superiore ed un albero viene mantenuto tale.
3. Il terzo caso equivale a $(0) + 1 = 1$, dato che non ci sono altri alberi con la stessa dimensione viene mantenuto l'albero.

In ogni caso il puntatore scorre di un albero (oppure ne riduce il numero) di 1, perciò ha complessità $\Theta(\log(n))$, dove $n$ è il numero di nodi.

Questo perchè il numero di alberi è logaritmico rispetto al numero di nodi, ed ogni caso ha complessità costante.

## Inserimento nodo
Si considera l'inserimento di un nodo come l'unione fra lo heap binomiale esistente ed uno heap binomiale con dimensione $0$ (ovvero il nodo in input).

Dato che il costo della [[#Unione di heap binomiali|union]] è logaritmico, anche l'inserimento di un nodo ha complessità $\Theta(\log(n))$.

## Estrazione del nodo con valore minimo
Dato che il nodo di valore minimo è sicuramente in una delle radici degli alberi binomiali, viene estratta tale radice minima.

A questo punto si toglie dallo heap binomiale l'albero binomiale con la radice estratta, si separa i figli dell'albero in sotto alberi e poi viene eseguita la union fra i sotto alberi e l'heap binomiale.

Anche in questo caso, l'operazione ha costo $\Theta(\log(n))$.

## Estrazione di un nodo qualsiasi
Viene dato al nodo un valore minimo (ovvero la chiave più piccola possibile) e poi viene eseguita l'[[#Estrazione del nodo con valore minimo|estrazione minima]].

## Diminuzione del valore di un nodo
Ovvero, dato un nodo e una chiave, bisogna assegnare al nodo la chiave fornita, sapendo che ``k <= x.key``.

Dato che sostituire la chiave potrebbe causare un'anomalia nello heap, propago l'anomalia verso l'alto, lavorando sulla profondità dell'albero.

Ha complessità $\Theta(log(n))$.

## Da heap binomiale ad array ordinato
Ha complessità $\Omega(n\log(n))$.