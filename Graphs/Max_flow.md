# Flusso massimo
## Caratteristiche
Complessità di Ford-Fulkerson: $\boldsymbol{O(|f^*|(V+E))}$

## Descrizione
Il problema del flusso massimo riguarda la massima quantità di flusso che è possibile inviare in una rete di flusso da un nodo $s$ (source) ad un nodo $t$ (target).

Una rete di flusso è un grafo composto da archi e nodi, dove ogni arco contiene una capacità massima ed un valore di flusso.

// esempio

La capacità è una funzione $c = V*V \to R^{\ge 0}$ , ed indica la capacità massima di un arco. Se un arco ha capacità $0$ è come se non esistesse.

Il flusso è una funzione $f: V*V \to R$, ed indica il flusso presente in un arco. Può assumere diversi valori:
- Se $f(u,v) \gt 0$, allora vengono trasmesse $n$ unità di flusso da $u$ a $v$;
- Se $f(u,v) = 0$, l'arco non ha flusso;
- Se $f(u,v) \lt 0$, vengono trasmesse $n$ unità di flusso da $v$ a $u$. 

#### Proprietà
Vigono le seguenti proprietà:
- Relazione flusso - capacità$$\forall (u,v), f(u,v) \le c(u,v)$$la quantità di flusso deve sempre essere minore della capacità massima;
- Antisimmetria$$\forall (u,v), f(u,v) = -f(v,u)$$se un arco ha $n$ come quantità di flusso, l'arco opposto ha $-n$ quantità di flusso;
- Conservazione$$\forall(u \in V - \{s,t\}), \sum\limits_{v} f(u,v) = 0$$la somma dei flussi entranti ed uscenti di un nodo deve sempre essere $0$.

#### Taglio della rete di flusso
Un qualsiasi taglio $(U,V)$ tale che $s \in U$ e $t \in V$, in cui $$c(U,V) \triangleq \sum_{u,v} c(u,v)$$ e$$f(U,V) \triangleq \sum_{u,v} f(u,v)$$
si ha che $f(U,V)$ è sempre la stessa per ogni taglio del grafo, questo grazie alla proprietà di conservazione.

#### Capacità residua
La capacità residua è definita come $c_f(u,v) = c(u,v)-f(u,v)$, mentre la rete residua è la rete formata dalle capacità residue.

Viene definito **cammino aumentante** un cammino da $s$ a $t$ nella rete residua.
L'**arco critico** di un cammino aumentante è l'arco con la minor capacità residua.

// esempio

## Algoritmo di Ford-Fulkerson
#### Pseudocodice
````c
void ford-fulkerson(){
	// Parti dal flusso nullo
	Flow_graph graph;
	// Finchè esistono cammini aumentanti
	while(exists_augmenting(graph)){
		// Trova un cammino aumentante
		Path augmenting = graph.find_augmenting();
		// Aumenta il flusso lungo il cammino di una quantità pari 
		// alla capacità residua dell'arco critico
		augmenting.increase_flow(augmenting.critical_edge.residual);
	}
}
````

#### Descrizione
L'algoritmo di Ford-Fulkerson incrementa tutti i cammini aumentanti per il valore dell'arco critico del cammino.

Ha complessità $O(|f^*|(V+E))$, dove $f^*$ è il flusso massimo, $|f^*|$ è il valore del flusso di un qualsiasi taglio e $V+E$ è la complessità delle operazioni dentro il while.

Ford-Fulkerson non termina nel caso di numeri irrazionali, ma garantisce di trovare sempre il flusso massimo.

#### Dimostrazione complessità
Ford-Fulkerson nel peggiore dei casi itera tante volte quante il valore del flusso massimo.

// esempio

## Algoritmo di Karp
