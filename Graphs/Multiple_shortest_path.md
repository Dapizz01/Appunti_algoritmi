# Cammini minimi a sorgente multipla
## Caratteristiche
Complessità Bellman-Ford applicato a tutti i nodi: $\boldsymbol{\Theta(V^2E)}$
Complessità Floyd-Warshall: $\boldsymbol{\Theta(V^3)}$
Complessità Johnson: $\boldsymbol{VE\log(V)}$

## Descrizione
Il problema dei cammini minimi a sorgente multipla è il [[Shortest_path|problema dei cammini a sorgente singola]] applicato su tutti i nodi del grafo.

Le soluzioni vengono rappresentate da due matrici, $\boldsymbol{D}$ e $\boldsymbol{\pi}$, dove:
- $d_{ij}$ è il costo del cammino minimo dal nodo $i$ al nodo $j$;
- $\pi_{ij}$ è il predecessore del nodo $j$ nel cammino minimo con sorgente $i$.

La matrice $D$ viene inizializzata con degli zeri sulla diagonale principale e $\infty$ su tutte le altre celle.   

// esempio?

## Possibili soluzioni
#### Algoritmo di Bellman-Ford
E' possibile applicare l'[[Shortest_path#Algoritmo di Bellman-Ford|algoritmo di Bellman-Ford]] su tutti i nodi, con complessità $\Theta(V^2E)$.

#### All_pairs_sp
Questo algoritmo è simile all'algoritmo di Bellman-Ford, ma applicato in modo diverso.

// Farlo oppure no?

````c
bool all_pairs_sp(Graph graph, int[][] weights){
	int[][][] D = init(graph, weights);
	int nodes_count = graph.nodes.count;
	for(int i = 1; i < nodes_count - 1; i++){
		D[i] = extend_sp(D[i - 1], weights);
	}
	D[nodes_count] = extends_sp(D[nodes_count - 1], weights);
	if(D[nodes_count] != D[nodes_count - 1])
		return false;
	return true;
}

int[][] extend_sp(int[][] D, int[][] weights){
	int size = rows(D);
	int[][] next_D;
	for(int i = 1; i < size; i++){
		for(int j = 1; j < size; j++){
			next_D[i][j] = INFINITE;
			for(int j = 1; k < size; k++){
				next_D[i][j] = min(D[i][j], D[i][k] + weights[k][j]);
			}
		}
	}
	return next_D;
}
````

#### Algoritmo di Floyd-Warshall
L'algoritmo di Floyd-Marshall analizza tutti i possibili percorsi nel grafo (il grafo può avere pesi negativi, ma non cicli negativi).

In particolare analizza tutti i cammini minimi che contengono un certo gruppo di nodi, compresi nell'insieme $\{1..K\}$ e rilassa i nodi.

// Da esportare zoomata

![Esempio di applicazione di Floyd-Marshall ad un nodo](Images/floy_warshall.svg)
*Esempio di applicazione di Floyd-Marshall ad un nodo*

````c
int[][] Floyd_Warshall(int[][] weights){
	// Array di matrici
	int[][][] D;
	// Numero di nodi
	int limit = rows(weights);
	// Aggiungo un nodo all'insieme (la destinazione non conta)
	for(int k = 1; k < limit; k++)
		// Per ogni riga (ovvero per ogni sorgente)
		for(int i = 1; i < limit; i++)
			// Per ogni colonna (ovvero per ogni destinazione)
			for(int j = 1; j < limit; j++)
				// Rilassa il cammino considerando il nodo k
				// e metti il nuovo costo nella matrice k
				D[k][i][j] = min(D[k-1][i][j], D[k-1][i][k] + D[k-1][k][j]);
}
````

Ha complessità $\Theta(V^3)$.

#### Algoritmo di Johnson
L'algoritmo di Johnson punta a trasformare i pesi degli archi (senza alterare la semantica del grafo) affinchè sia possibile usare l'[[Shortest_path#Algoritmo di Dijkstra|algoritmo di Dijkstra]] per trovare tutti i percorsi minimi.

Se infatti fosse possibile usare Dijkstra, il problema dei cammini minimi a sorgente multipla avrebbe complessità $V^2\log(V)+VE\log(V)$, in particolare:
- Nel caso di grafi sparsi, la complessità diventa $V^2\log(V)$, migliore rispetto all'[[#Algoritmo di Floyd-Warshall|algoritmo di Floyd-Warshall]].
- Se il grafo è connesso, $V^3\log(V)$, perchè $|E|=|V|^2$, complessità peggiore di Floyd-Warshall.

Per fare ciò non è sufficiente aggiungere un peso arbitrario a tutti gli archi, perchè i cammini minimi possono subire delle variazioni rispetto al grafo originale.

![Esempio di errato cambiamento dei pesi. Notare come il cammino minimo varia](Images/wrong_johnson.png)
*Esempio di errato cambiamento dei pesi. Notare come il cammino minimo varia*

Viene usata una formula per calcolare i nuovi pesi: $\hat{w}(u,v) \triangleq w(u,v) +h(u)-h(v)$ , dove $\hat{w}(u,v)$ è il nuovo costo non negativo e $h$ è la funzione che associa un valore ad ogni nodo del grafo.

Viene usato [[Shortest_path#Algoritmo di Bellman-Ford|Bellman-Ford]] per creare i nuovi pesi, creando un nuovo nodo $s$ che è connesso con costo 0 a tutti i nodi del grafo.
Bellman-Ford associa ad ogni nodo il costo minimo per arrivare a quel nodo (nel grafo originale) e viene usato tale costo come funzione, tale che $h(node)$ è il costo per raggiungere $node$ da $s$.

// esempio

Usando poi Dijkstra su ogni nodo la complessità diventa $VE+VE\log(V)$, dove $VE$ è la complessità di Bellman-Ford e $VE\log(V)$ la complessità dell'applicazione di $V$ volte Dijkstra.

Se viene rilevato un ciclo negativo, Bellman-Ford segnerebbe il ciclo come errore ma ciò non è detto che sia corretto, infatti i nodi del ciclo potrebbero non essere collegati in alcun modo alla destinazione.
In questo caso è necessario controllare attraverso quali nodi è possibile andare dalla sorgente alla destinazione.
Per farlo, basta fare una visita dei nodi dalla sorgente verso la destinazione e considerare solo quelli durante l'esecuzione di Dijkstra.

// rivedere spiegazione, non molto chiara