# Componenti fortemente connesse
## Caratteristiche
Complessità ricerca componenti connesse: $\boldsymbol{\Theta(V+E)}$
Complessità ricerca componenti fortemente connesse: $\boldsymbol{\Theta(V+E)}$

## Descrizione
Una componente connessa di un grafo è un insieme di nodi raggiungibili fra loro.
L'algoritmo usato per la ricerca di queste componenti usa gli [[Disjoint_set|insiemi disgiunti]].

Una componente **fortemente** connessa di un grafo è un insieme di nodi raggiungibili fra loro attraverso cammini percorribili sia per l'andata che per il ritorno.
Una SCC (componente fortemente connessa) è *elementare* se è composta da al massimo 2 nodi.

Una SCC è intrinsicamente ciclica.

// immagine + spiegazione

## Codice
````c
void connected_components(Graph graph){
	// Inizializza un insieme disgiunto
	Disjoint_set cc;
	
	// Per ogni nodo, crea un set
	for(Node node : graph){
		cc.make_set(node);
	}

	// Per ogni arco, unisci i set. I set rimanenti
	// sono le componenti connesse
	for(Edge edge : graph){
		cc.union(edge.source, edge.dest);
	}
}

void strongly_cc(Graph graph){
	// Applica DFS al grafo per trovare i finish_time
	DFS(graph, ANY_ORDER);
	
	// Ottiene il grafo trasposto
	Graph trasposed = traspose(graph);
	
	// Applica nuovamente DFS sul grafo trasposto controllando
	// i nodi in ordine di finish_time decrementale
	DFS(graph, DECREASING_FINISH_TIME);
}
````
## Dimostrazione
