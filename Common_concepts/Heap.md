# Heap
## Descrizione
Uno heap è un **albero binario semi completo** in cui esiste una **relazione fra** i valori dei nodi **padre e figlio**, tale che il valore della chiave del nodo padre è sempre maggiore (o minore) dei valori delle chiavi dei nodi figli (non c'è ordinamento a pari livello).
I nodi vengono enumerati (e ogni nodo memorizza il proprio ID) dall'alto verso il basso, da sinistra verso destra.

![Esempio di heap](https://i0.wp.com/sir.unl.edu/portal/bios/Binary-Heap-1b08b627.png)
*Esempio di heap, notare le relazioni fra padre e figli*

#### Termini usati
- **heap_size** è il numero di nodi dello heap. Notare che heap_size non è sempre pari al numero di nodi dell'albero, perchè uno heap può essere porzione di un albero più grande;
- Un **nodo foglia** è un nodo dello heap senza figli (perciò intrinsicamente appartenente all'ultimo livello). Notare che i nodi foglia sono al massimo metà di heap_size.
- Un albero binario è chiamato **semi completo** se tutti i livelli dell'albero hanno il massimo numero di nodi, tranne l'ultimo. L'ultimo livello deve però avere nodi continui da sinistra verso destra.
- Viene chiamato **min-heap** uno heap in cui il valore della chiave del padre deve essere minore dei valori delle chiavi dei figli.
- Viene chiamato **max-heap** uno heap in cui il valore della chiave del padre deve essere maggiore dei valori delle chiavi dei figli.
- L'**altezza di un nodo** è il numero di nodi da attraversare per arrivare ad un certo nodo.

In uno heap, ottenere l'elemento più grande (o più piccolo) ha complessità $O(1)$, cioè costante, mentre prendere l'opposto richiede complessità $O(n)$.

## Heapify (da rivedere e aggiungere esempio)
Supponiamo di avere uno max-heap e di eliminare la sua radice, rimpiazzandola con il nodo foglia più a destra. 
Ora la struttura non è più uno heap, come è possibile ottenere nuovamente uno heap?
Per questo scopo viene usato l'algoritmo heapify.

````c
// i è la presunta nuova radice di heap
// già sostiuita al posto della vecchia radice
void heapify(Tree heap, Node i){
	// Prendo i nodi figli di i (figli della vecchia radice)
	Node left = i.left;
	Node right = i.right;
	Node largest;
	// Se il figlio sinistro è nello heap ed ha valore maggiore di i
	if(left <= heap_size(heap) && l.val > i.val)
		largest = left;
	else
		largest = i;
	// Se il figlio sinistro è nello heap ed ha valore maggiore del largest
	// finora trovato
	if(right <= heap_size(heap) && r.val >= largest.val)
		largest = right;
	// Se largest non è i
	if(largest != i){
		// Swappa i valori di i e largest
		swap(i.val, largest.val);
		// Riesegui heapify dal nodo largest (quindi il figlio sx o dx)
		heapify(heap, largest);	
	}
}

// Toglie la root (elemento con valore massimo in uno max-heap)
// la sostituisce con l'ultima foglia dello heap
// e sistema lo heap
void remove_max(Tree heap){
	heap.root.val = heap.last_son.val;
	// Decrementa heap_size perchè la root viene tolta
	heap_size(heap)--;
	heapify(heap, heap.root);
}
````

Heapify ha complessità $O(\log(n))$ dove $n$ è il numero di nodi nello heap, in quanto l'algoritmo scende di un livello ad ogni iterazione.

#### Aggiunta di un nodo
L'aggiunta di un nodo nello heap ha complessità $O(\log(n))$ in quanto è possibile che il nuovo nodo non rispetti l'ordinamento dello heap, e che richieda l'uso della [[#Heapify da rivedere e aggiungere esempio|heapify]].