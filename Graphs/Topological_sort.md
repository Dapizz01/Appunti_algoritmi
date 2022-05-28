# Ordinamento topologico
## Caratteristiche
Complessità: $\boldsymbol{\Theta(V+E)}$

## Descrizione
Ordinare topologicamente un grafo significa ordinare i nodi in modo che per ogni arco $(u,v)$ valga che $u \lt v$.

L'algoritmo di ordinamento topologico usa [[DFS]] per due motivi:
- DFS consente di determinare se un grafo è ciclico, e quindi di ritornare un errore nel caso lo sia (infatti non è possibile ordinare topologicamente un grafo ciclico);
- DFS calcola il tempo di fine visita (finish_time) che serve per ottenere l'ordinamento.

Viene usato finish_time ordinato in modo decrescente perchè, prendendo come esempio un arco $(u,v)$, si ha che u.finish_time > v.finish_time, in quanto $v$ discende da $u$ (e non ci possono essere intervalli a metà), e quindi $u$ viene prima di $v$.

![](Images/topological_sort.svg)
*Esempio di implementazione di ordinamento topologico*

## Codice
````c
Node[] topological_sort(Graph graph){
	// Uso una variante di DFS che ritorna i nodi in ordine
	// di finish_time decrescente
	Node[] sorted = DFS(graph);
	
	// Se è stato trovato un ciclo nel grafo, non è possibile
	// ordinare i nodi, viene ritornato un errore
	if(sorted == FOUND_CYCLE)
		return ERR_CYCLE;
	
	return sorted;
}
````
## Dimostrazione
[[DFS#Caratteristiche|Come DFS]], perchè le altre istruzioni sono costanti.