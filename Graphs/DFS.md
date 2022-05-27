# DFS
## Caratteristiche
Complessità: $\boldsymbol{\Theta(V+E)}$

## Descrizione
DFS (Depth-First Search) è un algoritmo di visita di un grafo. A differenza di [[BFS]], quando viene esplorato un nodo viene subito esplorato un suo vicino.
Non ci sono code, ma viene usato lo stack di attivazione tramite chiamate ricorsive (sostanzialmente, è una pila LIFO).

Per ogni nodo vengono usati i campi:
- distance, che indica il momento in cui è stato esplorato il nodo per la prima volta;
- finish_time, che indica il momento in cui sono stati esplorati tutti i vicini
- ... quelli usati in BFS.

// Immagine

Il risultato di DFS è un albero dei cammini che contiene il seguente tipo di archi:
- C(rossing): è un arco che va da un ramo ad un altro (o da un albero ad un altro) senza scavalcare;
- T(ree): è un comune arco dell'albero;
- B(ackwords): è un arco che torna indietro (va verso l'alto nella rappresentazione degli alberi);
- F(orward): è un arco che permette di "scavalcare" uno o più nodi dell'albero.

Ogni tipo di arco deriva dal colore del vicino:
- Se il nodo è WHITE, l'arco sarà di tipo T;
- Se il nodo è GRAY, l'arco sarà di tipo B;
- Se il nodo è BLACK, l'arco sarà di tipo C oppure F.

Gli intervalli formati possono essere disgiunti o uno sottointervallo dell'altro.

DFS consente inoltre di **rilevare se un grafo è aciclico**, infatti se durante DFS si incontra un nodo GRAY (oppure un arco B).

## Codice
````c
int time;

void DFS(Graph graph){
	for(Node node : graph){
		node.color = WHITE;
		node.prev = NULL;
	}
	time = 0;
	for(Node node : graph){
		if(node.color == WHITE)
			DFS_visit(node);
	}
}

void DFS_visit(Node node){
	node.color = GRAY;
	node.distance = ++time;
	for(Node neighbor : node){
		if(neighbor.color == WHITE){
			neighbor.prev = node;
			DFS_visit(neighbor, time);
		}
	}
	node.color = BLACK;
	node.finish_time = ++time;
}
````

## Dimostrazione