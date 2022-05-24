# Insertion sort
## Caratteristiche
Complessità:  $\boldsymbol{\Theta(n^2)}$, ma nel caso ottimo si avvicina a $\boldsymbol{O(n)}$
Ordina in loco: **SI**
Stabile: **SI**

## Codice
````c
void insertion_sort(int array[], int length){
	int key; // Contiene l'elemento corrente
	int i; // Scorre l'array all'indietro
	
	// Per ogni elemento a partire dal secondo
	// (il primo è già ordinato)
	for(int j = 2; j < length; j++){
		// Metto l'elemento corrente in key
		key = array[j];
		// Guardo l'elemento precedente
		i = j - 1;

		// Per ogni elemento precendente maggiore di array[j]
		while(i > 0 && array[i] > key){
			// Scorro array[i] una posizione più avanti,
			// per occupare la posizione vecchia di array[j]
			array[i+1] = array[i];
			i--;
		}

		// Ora "i" punta ad un elemento <= di key,
		// la posizione array[i+1] è libera
		// perchè ho spostato tutti gli elementi a dx
		// di una posizione
		array[i+1] = key;
	}
}
````

## Dimostrazioni
**Complessità**: questo sort ha complessità $1 + 2 + 3 + ... + n = \frac{n(n+1)}{2} \simeq n^2$  nel peggiore dei casi (array ordinato inversamente).

**Ordina in loco**: Si, perchè non usa array di supporto, è necessario solo scambiare le posizioni fra gli elementi dell'array.

**Stabile**: E' stabile perchè due elementi con stesso valore non vengono invertiti di posizione (la condizione del `while(...)` è infatti `>` non `>=`).

## Animazione
[Insertion sort](https://www.youtube.com/watch?v=8oJS1BMKE64), in particolare la barra verde rappresenta `array[j]` mentre la barra rossa `array[i]`