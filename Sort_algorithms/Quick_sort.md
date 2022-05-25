# Quick sort
## Caratteristiche
Complessità quick_sort: 
- Nel caso migliore $\boldsymbol{\Theta(n\log(n))}$
- Nel caso peggiore $\boldsymbol{\Theta(n^2)}$
Complessità partition: $\boldsymbol{O(n)}$
Ordina in loco: **SI**
Stabile: **NO**

#### Descrizione
Quick sort è un algoritmo Divide ed Impera ricorsivo simile come concetto a [[Merge_sort|merge sort]], ma applicato in modo diverso.

Quick sort, per ogni subarray, individua un pivot e sposta tutti i numeri minori di pivot a sinistra del pivot, e tutti i numeri maggiori a destra del pivot ed esegue la stessa operazione sulla metà sinistra e destra del subarray.

![Esempio di esecuzione di una partition](Images/partition_animation.gif)
*Esempio di esecuzione di una partition*

#### Codice
````c
void quick_sort(int array[], int start, int end){
	// Per ogni subarray
	if(start < end){
		// Chiama partition su array
		int pivot = randomized_partition(array, start, end);
		// Chiamata ricorsiva di quick_sort
		// sulle parti sx e dx di array
		quick_sort(array, start, pivot);
		quick_sort(array, pivot + 1, end);
	}
}

// Divide l'array in 2 parti usando come pivot
// il primo elemento in array, poi
// mette tutti i numeri < pivot alla sx di pivot
// e tutti i numeri > di pivot alla sua dx
int partition(int array[], int start, int end){
	// Considera come pivot il valore del primo
	// elemento di array
	int pivot = array[start];
	// Dichiarazione puntatori sx e dx:
	// left_ptr scorre da sx verso dx
	// right_ptr scorre da dx verso sx
	int left_ptr = start - 1;
	int right_ptr = end + 1;
	while(true){
		// Sposta il right_ptr verso sx finchè non trova
		// un elemento con valore minore di pivot (che andrebbe
		// quindi a sx di pivot)
		while(array[right_ptr] > pivot)
			right_ptr--;
		// Come sopra, ma con left_ptr verso dx
		while(array[left_ptr] < pivot)
			left_ptr++;

		// Se left_ptr e right_ptr non si sono incrociati
		if(left_ptr < right_ptr)
			// Non hanno ancora finito di iterare array, quindi
			// swappa gli elementi fuori posto in entrambe le metà
			// e ricomincia il ciclo while(true)
			// N.B. right_ptr e left_ptr continuano a scorrere array
			// dal punto in cui erano rimasti
			swap(array[left_ptr], array[right_ptr]);
		else
			// L'array è stato interamente controllato
			// perchè i puntatori si sono incrociati
			return right_ptr;
	}
}

// Prende un elemento in array casuale come pivot
// lo scambia con il primo e poi chiama partition.
// Ha prestazioni migliori rispetto alla partiion.
int randomized_partition(int array[]. int start, int end){
	int random_pivot = random(start, end);
	swap(array[start], array[random_pivot]);
	return partition(array, start, end);
}
````


#### Dimostrazioni
**Complessità**: Se il pivot è ottimale (ovvero è il mediano degli elementi dell'array) si ottiene l'equazione$$T(n) = 2T(\frac{n}{2}) + n$$
dove $n$ è il costo della partition, mentre $2T(\frac{n}{2})$ sono le chiamate ricorsive di quick sort sulle due metà. Risolvendo l'equazione con il [[Master_theorem|master theorem]] il risultato è $\Theta(n\log(n))$.

Se invece il pivot è l'elemento più piccolo (o più grande) dell'array, si ottiene l'equazione$$T(n) = n + T(1) + T(n-1)$$
che ha complessità $\Theta(n^2)$.

**Ordina in loco**: Quick sort ordina in loco perchè non usa array di supporto, ma effettua delle permutazioni sull'array originale.

**Stabile**: Quick sort non è stabile perchè l'ordine relativo degli elementi può cambiare se un elemento è scelto come pivot, e anche durante le operazioni in partition.

#### Animazione
[Spiegazione](https://www.youtube.com/watch?v=Hoixgm4-P4M) e [visualizzazione](https://www.youtube.com/watch?v=8hEyhs3OV1w).