# BFS
## Caratteristiche
Complessità: $\boldsymbol{\Theta(V+E)}$

## Descrizione
BFS (Breadth-First Search) è un algoritmo di visita dei grafi (ovvero, visita tutti i nodi di un grafo) in larghezza. A differenza di [[DFS]], esplora prima tutti i vicini diretti, poi tutti i vicini dei vicini e così via.

BFS lavora sia su grafi orientati che non orientati.

BFS inoltre trova i cammini ($u$, $v$) con il minor numero di nodi intermedi (se il grafo non ha archi pesati, corrispondono ai cammini minimi).

Ad ogni nodo vengono assegnati degli attributi:
- Un colore, che indica se il nodo è già stato visitato. I colori usati sono:
	- *WHITE*, il nodo non è mai stato visitato prima;
	- *GRAY*, il nodo è stato visitato da BFS, ma i suoi vicini non sono stati esplorati;
	- *BLACK*, il nodo e i suoi vicini sono stati esplorati.
- Una distanza, che indica il numero di nodi attraversati per arrivare in questo nodo dal nodo di partenza;
- Un campo $\pi$ (o prev) indica il predecessore di questo nodo nel cammino dalla sorgente a questo nodo.

Non è necessario usare i colori per BFS, servono solo a rendere il codice più leggibile.

Il risultato è un albero con radice il nodo sorgente e che contiene i nodi raggiungibili da essa.

![Esempio di esecuzione di BFS](Images/bfs.png)
*Esempio di iterazione di BFS*

## Codice
````c
// Esegue BFS su una parte connessa del grafo,
// se ci sono altri nodi non connessi questi non vengono esplorati.
// Per essere esplorati occorre chiamare BFS in ogni nodo (evitando
// di chiamarlo dove sui nodi già esplorati)
void BFS(Graph graph, Node start){

	// Dichiaro una coda FIFO in cui contenere i nodi
	Queue queue;

	// Inizializzazione dei nodi del grafo
	for(Node node : graph){
		node.color = WHITE;
		node.distance = INFINITE;
		node.prev = NULL;
	}

	// Inizializzazione nodo di partenza
	start.color = GREY;
	start.distance = 0;
	queue.add(start);

	// Finchè la coda non è vuota
	while(queue.size != 0){
		// Guarda la testa della coda
		Node current = queue.peek();

		// Per ogni vicino della testa
		for(Node neighbor : current.neighbours){
			// Se non è mai stato esplorato questo vicino,
			// mettilo come GREY, assegna i campi distance
			// e prev e aggiungilo in fondo alla coda
			if(neighbor.color == WHITE){
				neighbor.color = GREY;
				neighbor.distance = current.distance + 1;
				node.prev = current;
				queue.add(neighbor);
			}
		}

		// Togli la testa (già esplorata)
		queue.poll();
		current.color = BLACK;
	}
}

// Stampa il percorso fatto con BFS da source a dest ricorsivamente
// partendo dalla destinazione e andando indietro
void path(Node source, Node dest){
	// Se non è ancora arrivato alla sorgente, vai al prev
	if(dest != source)
		return path(source, dest.prev);
	// Sto stampando dalla sorgente alla destinazione, stampa
	// questo nodo
	print(dest);
}
````

## Dimostrazione
BFS itera su tutti i nodi e su tutti gli archi al massimo una volta, quindi $\Theta(V+E)$.
La complessità è lineare, ma varia in base al tipo di grafo:
- Se è un grafo sparso (ci sono pochi nodi), allora la complessità diventa $\Theta(V)$.
- Se è un grafo completo (ogni nodo è collegato direttamente ad ogni altro nodo), la complessità diventa $\Theta(E)$ che è simile a $\Theta(V^2)$.