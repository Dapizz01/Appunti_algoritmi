# Cammini minimi (a sorgente singola)
## Caratteristiche

## Descrizione
Il problema dei [[Introduction#Termini usati|cammini minimi]] è la ricerca di tutti i cammini minimi in un grafo da un nodo sorgente a tutte le possibili destinazioni.

Un cammino minimo può anche non esistere come nel seguente caso:

![Esempio di cammino minimo di un grafo ciclico con ciclo negativo](Images/cyclic_path.svg)
*Esempio di cammino minimo di un grafo ciclico con ciclo negativo*

il cammino minimo da $s$ a $v$ è infinito, perchè c'è un ciclo negativo.
La questione dei cicli infiniti è risolvibile in due modi:
- Si evita di passare per lo stesso nodo per più di una volta, ma è un problema NP-completo;
- Si lancia un errore nel caso di cicli negativi.

E' possibile rappresentare i cammini minimi con sorgente singola in un albero, radicato nel nodo sorgente.

#### Funzioni comuni
###### Init
La funzione init viene usata per inizializzare il grafo, ha complessità $\Theta(V)$.
````c
void init(Graph graph, Node source){
	// Per ogni nodo, metti la distanza ad INFINITE e nessun predecessore
	for(Node node : graph){
		node.distance = INFINITE;
		node.prev = NULL;
	}
	// Il nodo sorgente ha invece distanza 0
	source.distance = 0;
}
````
###### Relax
La funzione relax controlla che il miglior costo trovato finora per raggiungere dest sia migliore del costo per andare dalla sorgente del cammino al nodo mid + il costo dell'arco da mid a dest.

Se il costo attuale è maggiore, viene sostituito con il costo calcolato e il predecessore di dest diventa mid.

![Esempio di relax](Images/relax.svg)
*Esempio di relax*
````c
void relax(Node mid, Node dest, int weight){
	if(dest.distance > mid.distance + weight){
		dest.distance = mid.distance + weight;
		dest.prev = mid;
	}
}
````

## Algoritmo di Dijkstra
#### Descrizione
L'algoritmo di Dijkstra opera similarmente all'[[Minimum_spanning_tree#Algoritmo di Prim|algoritmo di Prim]] e **non si occupa del caso dei cicli negativi**.

Esplora il grafo a partire dal nodo di partenza e associa ad ogni nodo una priorità, in base alla distanza con il nodo vicino, ed esplora il nodo con priorità più bassa.

Una volta che l'algoritmo di Dijkstra opera su un nodo, vuol dire che è già stato trovato il cammino minimo per quel nodo.

// esempio

#### Codice
````c
void Dijkstra(Graph graph, int[][] weights, Node start){
	// Inizializza il grafo
	init(graph, weights);
	// Crea una priority_queue con i nodi del grafo
	Priority_queue queue = graph.nodes;

	// Finchè non sono stati esplorati tutti i nodi
	while(queue.size > 0){
		// Prendi quello con priorità più bassa
		Node current = extract_min(queue);
		// Per ogni vicino
		for(Node n : current.neighbours){
			// Rilassa l'arco con il vicino
			relax(current, n, weights[current][n]);
		}
	}
}
````

#### Complessità
La complessità dell'algoritmo è $\Theta(V+E+V*(c)+E*(d))$ dove $c$ è il costo della extract_min e $d$ il costo della reduce_key.

La complessità varia quindi in base all'implementazione della coda con priorità.

La coda con priorità può essere implementata con liste (ordinate oppure meno), [[Heap|heap]] o heap di fibonacci (non trattati a lezione, reduce_key ha complessità costante, extract_min ha complessità $\Theta(\log(n))$).

Alcune implementazioni sono migliori nel caso di grafi sparsi, altre nel caso di grafi completi.

## Algoritmo di Bellman-Ford

## Algoritmo per grafi aciclici
