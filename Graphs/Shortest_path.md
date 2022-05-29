# Cammini minimi (a sorgente singola)
## Caratteristiche

## Descrizione
Il problema dei [[Introduction#Termini usati|cammini minimi]] è la ricerca di tutti i cammini minimi in un grafo da un nodo sorgente a tutte le possibili destinazioni.

Un cammino minimo può anche non esistere come nel seguente caso:

// esempio

il cammino minimo da $s$ a $v$ è infinito, perchè c'è un ciclo negativo.
La questione dei cicli infiniti è risolvibile in due modi:
- Si evita di passare per lo stesso nodo per più di una volta, ma è un problema NP-completo;
- Si lancia un errore nel caso di cicli negativi.

E' possibile rappresentare i cammini minimi con sorgente singola in un albero, radicato nel nodo sorgente.

// esempio

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

// esempio

````c
void relax(Node mid, Node dest, int weight){
	if(dest.distance > mid.distance + weight){
		dest.distance = mid.distance + weight;
		dest.prev = mid;
	}
}
````

## Algoritmo di Dijkstra

## Algoritmo di Bellman-Ford

## Algoritmo per grafi aciclici
