# Heap sort
## Caratteristiche
Complessità heap_sort:  $\boldsymbol{\Theta(n\log(n))}$
Complessità build_heap: $\boldsymbol{\Theta(n)}$
Ordina in loco: **SI**
Stabile: **NO**

## Descrizione
Lo heap sort si basa sul concetto di [[Heap]]. In particolare, nel considerare un array come uno heap, interpretandolo come di seguito:

![Rappresentazione di un array come heap](https://www.geeksforgeeks.org/wp-content/uploads/binaryheap.png)
*Rappresentazione di un array come heap*

Heap sort inizialmente costruisce un [[Heap#Termini usati|max-heap]] con [[Heap#Heapify da rivedere e aggiungere esempio|build_heap]].

Poi per ogni elemento dell'array, prende la root dello heap (che è sicuramente l'elemento più grande dello heap), lo swappa con l'ultima foglia, posizionando la vecchia root nell'indice corretto dell'array ordinato (infatti viene trovato, per ogni iterazione, l'i-esimo valore più grande). 

Infine, usando la funzione [[Heap#Heapify da rivedere e aggiungere esempio|heapify]], sistema lo heap per la prossima iterazione.

![Esempio di applicazione di heap sort](Images/heap_sort_animation.gif)
*Esempio di applicazione di heap sort*

## Codice
````c
// Dato un array, ne costruisce uno heap
void build_heap(int array[]){
	// Considero l'array come heap (come nella figura sopra)
	Tree heap = (Tree) array;
	heap.heap_size = length(array);

	// Per ogni sotto albero nello heap (non ha senso fare
	// la heapify su un sotto albero composto da un nodo solo)
	// a partire dall'ultimo (quello più in basso a dx)
	for(int i = heap.heap_size / 2; i >= 1; i--){
		// Esegui la heapify da radice i
		heapify(heap, i);
	}
}

void heap_sort(int array[]){
	// Dato array, ne costruisce uno heap (max-heap in questo caso)
	build_heap(array);
	// Per ogni elemento dell'array a partire dall'ultimo
	// (tranne il primo)
	for(int i = length(array); i >= 2; i--){
		// Dato che la root dello heap è l'elemento più grande
		// dello heap, lo swappo con l'ultima foglia
		swap(array[i], array[1]);
		// Diminuisco la dimensione dello heap, perchè la root precedente
		// è ora nel posto corretto dell'array ordinato
		array.heap_size--;
		// Sistema lo heap (che ha la foglia come root) 
		// per la prossima iterazione
		heapify(array, 1);
	}
}
````

## Dimostrazioni
La complessità di build_heap è $O(n)$, ma viene chiamato una sola volta da heap_sort.
Heap sort ha complessità $O(n\log(n))$ perchè chiama $n$ volte heapify, che a sua volta ha complessità $O(\log(n))$.

Ordina in loco perchè non vengono usati array di supporto, tutti gli ordinamenti vengono fatti permutando l'array originale.

Non è stabile perchè tutti gli elementi (tranne il primo) vengono swappati con il primo, quindi l'ordine relativo viene invertito (mentre la heapify è stabile).


## Animazione
Spiegazione video del [build_heap](https://www.youtube.com/watch?v=WsNQuCa_-PU) e di [heap_sort](https://www.youtube.com/watch?v=_bkow6IykGM).