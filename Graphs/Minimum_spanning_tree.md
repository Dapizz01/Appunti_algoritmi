# Albero di copertura di costo minimo (MST)
## Caratteristiche
Complessità dell'algoritmo di Kruskal: $\boldsymbol{\Theta(V+E\log(E))}$
Complessità dell'algoritmo di Prim: $\boldsymbol{\Theta((V+E)\log(V))}$ tramite [[Heap|heap]]

## Descrizione
Un albero di copertura di costo minimo (MST, Minimum Spanning Tree) è il sottografo del grafo pesato originale, in cui tutti i nodi sono raggiungibili con il costo minimo rispetto a tutti i possibili sottografi.

Un MST non può contenere cicli (in quanto è possibile togliere un arco dal ciclo e tutti i nodi sarebbero comunque raggiungibili) e dato che per definizione un grafo senza cicli è un albero, la soluzione è un albero.

## Taglio di un grafo
E' una bipartizione dei nodi di un grafo.

// Immagine

Un arco del taglio (ovvero coinvolto nel taglio) è **sicuro** se è l'arco con costo minimo rispetto agli altri archi del taglio.

Dato un arco sicuro $(u,v)$ esiste un MST che contiene $(u,v)$.

// perchè?

## Algoritmo di Kruskal
#### Descrizione
L'algoritmo di Kruskal prevede di ordinare gli archi per peso crescente e di usare gli [[Disjoint_set|insiemi disgiunti]] per tenere traccia dei nodi già considerati.

![](Images/kruskal.svg)
*Esempio di esecuzione dell'algoritmo di Kruskal. I nodi di uno stesso colore appartengono allo stesso insieme e l'arco evidenziato in rosso è quello considerato nell'iterazione*

#### Codice
````c
void kruskal(Graph graph, Weight[][] weights){
	Edge answer[];
	Disjoint_set set;

	// Crea un insieme per ogni nodo
	for(Node node : graph){
		set.make_set(node);
	}

	// Ordina gli archi per peso crescente
	sort(graph.edges, weights, ASCENDING_ORDER);

	// Per ogni arco
	for(Edge edge : graph){
	
		// Se i nodi collegati dall'arco sono in due insiemi diversi
		// significa che questo arco è un taglio sicuro, perchè gli archi
		// sono in ordine di peso crescente.
		// Se i nodi sono nello stesso insieme, è già stato trovato
		// un taglio sicuro
		if(set.find_set(edge.source) != set.find_set(edge.dest)){
			// Aggiungo al MST questo arco e unisco gli insiemi dei due nodi
			answer.add(edge);
			set.union(edge.source, edge.dest);
		}
	}
}
````

#### Complessità
L'algoritmo ha complessità $\Theta(V+E\log(E))$ in quanto itera sui nodi ed effettua l'ordinamento degli archi che ha complessità $E\log(E)$ (è possibile ridurla in alcuni casi con un algoritmo di [[Index#Sorting lineare|sort lineare]]).

## Algoritmo di Prim
#### Descrizione
L'algoritmo di Prim opera con una "barriera" che ha origine in un nodo di partenza definito. I nodi dentro la barriera sono fissati e sono parte della soluzione, i nodi esterni sono invece ancora da elaborare.

Inizialmente, solo il nodo di partenza è dentro la barriera e tutti i nodi sono in una coda a priorità in base alla distanza con un vicino già dentro la barriera.

Per ogni nodo viene controllato il valore degli archi dei vicini e vengono aggiornate le distanze, infine viene inglobato nella barriera.

![Esempio di esecuzione dell'algoritmo di Prim](Images/prim.svg)
*Esempio di esecuzione dell'algoritmo di Prim*

#### Codice
````c
void prim(Graph graph, Weight[][] weights, Node start){
	// Dichiaro una lista a priorità 
	// (in base alla chiave, ordine crescente) con i nodi
	Priority_queue outside = graph.nodes;

	// Inizializzo la distanza di ogni nodo a INFINITE
	for(Node node : graph){
		node.distance = INFINITE;
	}

	// Inizializzo il nodo di partenza
	start.distance = 0;
	start.prev = NULL;

	// Finchè c'è un nodo nella coda
	while(outside.size == 0){
	
		// Considero il nodo con distanza più bassa
		// e lo inglobo nella barriera
		Node current = extract_min(queue);
		
		// Per ogni vicino di quel nodo
		for(Node node : current.neighbours){
		
			// Se devo ancora fissare il nodo nel MST 
			// (ovvero, è al di fuori della barriera) 
			// e la sua distanza è minore del peso dell'arco
			if(queue.contains(node) && WEIGHT_OF(current, node) < node.distance){
				// Cambia il valore della distanza con quello dell'arco
				node.distance = WEIGHT_OF(current, node);
				// Metti il prev del vicino a current
				node.prev = current;
			}
		}
	}
}
````

#### Dimostrazione
L'algoritmo di Prim ha complessità totale $\Theta(V+E+V*c+E*d)$ dove $c$ è il costo della extract_min e $d$ è il costo della reduce_key (viene fatta nell'ultimo if, in quanto viene cambiata la chiave di un valore e ciò comporta la modifica dell'ordine della coda).

Considerando l'implementazione della coda di priorità con uno [[Heap|heap]], si ha che la complessità finale risulta $\Theta((V+E)\log(V))$, complessità migliore di [[#Algoritmo di Kruskal|Kruskal]].

Osservare che le operazioni sullo heap hanno complessità $\Theta(\log(V))$ perchè le operazioni sono fatte sulla coda che ha $V$ elementi.



