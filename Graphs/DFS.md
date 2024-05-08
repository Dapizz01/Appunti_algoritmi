# DFS
## Caratteristiche
Complessità: $\boldsymbol{\Theta(V+E)}$

## Descrizione
DFS (Depth-First Search) è un algoritmo di visita di un grafo. A differenza di [[BFS]], quando viene esplorato un nodo viene subito esplorato un suo vicino.
Non ci sono code, ma viene usato lo stack di attivazione tramite chiamate ricorsive (sostanzialmente, è una pila LIFO).

Per ogni nodo vengono usati i campi:
- distance, che indica il momento in cui è stato esplorato il nodo per la prima volta;
- finish_time, che indica il momento in cui sono stati esplorati tutti i vicini
- ... [[BFS#Descrizione|quelli usati in BFS]] (colori, prev, ...).

![](Images/dfs.svg)
*Esempio di esecuzione di DFS*

Il risultato di DFS è un albero dei cammini che contiene il seguente tipo di archi:
- Crossing: è un arco che va da un ramo ad un altro (o da un albero ad un altro) senza scavalcare;
- Tree: è un comune arco dell'albero;
- Backwords: è un arco che torna indietro (va verso l'alto nella rappresentazione degli alberi);
- Forward: è un arco che permette di "scavalcare" uno o più nodi dell'albero.

Ogni tipo di arco deriva dal colore del vicino:
- Se il nodo è WHITE, l'arco sarà di tipo Tree;
- Se il nodo è GRAY, l'arco sarà di tipo Backwords;
- Se il nodo è BLACK, l'arco sarà di tipo Crossing oppure Forward.

Gli intervalli formati possono essere disgiunti o uno sottointervallo dell'altro.

DFS consente inoltre di **rilevare se un grafo è aciclico**, infatti se durante DFS si incontra un nodo GRAY (oppure un arco Backwords).

![Esempio dei diversi tipi di archi in DFS](Images/dfs_tree.svg)
*Esempio dei diversi tipi di archi in DFS (riprende l'esempio precedente)*

## Codice
````c
// E' una variabile globale, funge da "clock"
int time;

// Applica DFS a tutto il grafo, anche se non è connesso
void DFS(Graph graph){
	// Inizializzazione di ogni nodo
	for(Node node : graph){
		node.color = WHITE;
		node.prev = NULL;
	}
	
	// Reset time
	time = 0;

	// Per ogni nodo, se non è già esplorato chiama DFS_visit sul nodo
	for(Node node : graph){
		if(node.color == WHITE)
			DFS_visit(node);
	}
}

// Applica DFS con un certo nodo sorgente
void DFS_visit(Node node){
	// Marca il nodo come GRAY e segna il tempo di inizio visita
	node.color = GRAY;
	node.distance = ++time;
	
	// Per ogni vicino, se non è esplorato chiama DFS_visit sul vicino
	for(Node neighbor : node){
		if(neighbor.color == WHITE){
			neighbor.prev = node;
			DFS_visit(neighbor, time);
		}
	}
	
	// Tutti i vicini sono stati esplorati, marca il nodo
	// come BLACK e segna il tempo di fine visita
	node.color = BLACK;
	node.finish_time = ++time;
}
````

## Dimostrazione
````dfs_visit```` viene chiamata al massimo una volta per nodo (perchè una volta esplorato diventa BLACK) ed ha costo $\Theta(V+E)$, perchè esplora ogni nodo e ogni arco.

Dato che DFS controlla anche che un grafo sia ciclico, un algoritmo ottimo che verifica la presenza di cicli in un grafo non può avere complessità maggiore di $\Theta(V+E)$.