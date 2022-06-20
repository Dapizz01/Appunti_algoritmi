# Randomized select
## Caratteristiche
Complessità: $\boldsymbol{\Theta(n)}$

## Descrizione
Random select, chiamato anche *quickselect*, è un algoritmo di selezione che usa la funzione randomized_partition di [[Quick_sort|quicksort]].

A differenza di quicksort, quickselect non esegue chiamate ricorsive su entrambe le metà, ma solo su quella dove è contenuto l'elemento desiderato, ordinando solo parzialmente l'array.

## Codice
````c
int quickselect(int[] array, int start, int end, int target_index){
	// Caso base
	if(start == end)
		return array[start];
	// Chiama randomized_partition sulla parte di array
	int pivot = randomized_partition(array, start, end);
	// Se l'indice target è a sx del pivot, richiama quickselect
	// sulla parte sx
	if(target_index <= pivot)
		quickselect(array, start, pivot, target_index);
	// Altrimenti su quella dx
	else
		quickselect(array, pivot + 1, end, target_index);
}
````
## Dimostrazione
Se randomized_partition ottiene sempre l'elemento centrale dell'array, la funzione di complessità di quickselect è $T(n) = T(n/2)+n$, che risolto con il [[Master_theorem|Master theorem]] diventa $\Theta(n)$.

Nel caso peggiore invece randomized_partition ottiene sempre un elemento estremo dell'array (quello più a sinistra, oppure quello più a destra).
La funzione di complessità è $T(n) = T(n-1)+n$, ovvero $\Theta(n^2)$.

E' possibile tuttavia implementare un miglior algoritmo di ricerca del pivot con complessità $\Theta(n)$, portando la complessità finale di quickselect a $\Theta(n)$, ma con costanti molto elevate.