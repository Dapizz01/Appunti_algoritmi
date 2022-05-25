# Merge sort
## Caratteristiche
Complessità:  $\boldsymbol{\Theta(n\log(n))}$
Ordina in loco: **NO**
Stabile: **SI**

## Descrizione
Merge sort si basa su divide et impera, ovvero la divisione di un problema grande in più sotto problemi e si presta ad un approccio ricorsivo.

Sostanzialmente, divide il problema fino a trovare tutti i sotto problemi più piccoli (ovvero coppie di numeri).
Ordina tali coppie e le coppie ordinate vengono poi usate per ordinare gruppi di 2 coppie e così via, fino a ordinare l'intero array.

![Esempio di esecuzione di merge sort](Images/merge_sort_animation.gif)
*Esempio di esecuzione di merge sort*

## Codice
````c
// start = indice di partenza del subarray
// end = indice di fine del subarray
void merge_sort(int array[], int start, int end){
	// Se il subarray è di almeno 2 elementi
	if(start < end){
		int pivot = (start + end)/2;
		// Richiama ricorsivamente merge_sort sulle parti
		// a sx e dx di array
		merge_sort(array, start, pivot);
		merge_sort(array, pivot + 1, end);
		// Una volta arrivato qui, i subarray sx e dx
		// sono già ordinati (perchè hanno già eseguito merge)
		// quindi unisco le due parti
		merge(array, start, pivot, end);
	}
}

// Date in input le metà sx e dx dell'array (già ordinate)
// ricompone l'array in modo ordinato
void merge(int array[], int start, int pivot, int end){
	int i = 1;
	// Puntatore che scorre la metà sx di array
	// da sx verso dx
	int left_ptr = start;
	// Come left_ptr ma per la metà dx
	int right_ptr = pivot + 1;
	// Array di supporto
	int support_array[end - start + 1];

	// Per ogni elemento
	while(left_ptr <= pivot || right_ptr <= end){
		// Se la metà sx non è terminata e 
		// se quella dx o è terminata
		// o il valore attualmente puntato da right_ptr
		// è maggiore di quello puntato da left_ptr,
		if(left_ptr <= end && 
		(right_ptr > end || array[left_ptr] <= array[right_ptr])){
			// Aggiungi l'elemento puntato da left_ptr
			// alla soluzione, perchè è il più piccolo
			support_array[i] = array[left_ptr];
			// Scorri il puntatore sx
			left_ptr++;
		}
		else{
			// Aggiungi l'elemento puntato da right_ptr
			// alla soluzione, perchè è il più piccolo
			support_array[i] = array[right_ptr];
			// Scorri il puntatore dx
			right_ptr++;
		}
		i++;
	}

	// Copia ogni elemento di support_array
	// in array (a partire da start)
	for(i = 1; i < end - start; i++){
		array[start + i - 1] = support_array[i];
	}
}

````

## Dimostrazione
**Complessità**: dato che merge sort è ricorsivo, la sua complessità si può facilmente esprimere con la seguente formula:$$T(n) = T(\frac{n}{2}) + T(\frac{n}{2}) + T(n)$$
Dove $T(\frac{n}{2})$ sono le chiamate ricorsive, mentre $T(n)$ è il costo della funzione merge.
Risolvendo l'equazione con il [[Master_theorem|Master Theorem]] si ha che la complessità è $\Theta(n\log(n))$.

**Ordina in loco**: dato che viene usato l'array di supporto, merge sort non ordina in loco.

**Stabile**: l'algoritmo è stabile perchè viene sempre favorito il subarray sinistro in merge, mantenendo l'ordine.

## Animazione
[Merge sort](https://www.youtube.com/watch?v=ZRPoEKHXTJg)