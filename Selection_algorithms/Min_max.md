# Min_max
## Caratteristiche
Complessità: $\boldsymbol{\Theta(n)}$
Seleziona in loco: **SI**
Stabile: **SI**
Condizione: questo algoritmo trova solamente l'elemento minimo e quello massimo (ovvero il primo e l'ultimo elemento dell'array ordinato).

## Descrizione
Considera come minimo e come massimo il primo valore dell'array, poi controlla tutti i valori dell'array:
- Se il valore corrente è minore del minimo finora trovato, considero il valore corrente come minimo;
- Se il valore corrente è maggiore del massimo finora trovato, considero il valore corrente come massimo.

## Codice
````c
int min_max(int array[]){
	int min = array[0];
	int max = array[0];

	for(int i = 2; i <= length(array); i++){
		if(array[i] < min)
			min = array[i];
		if(array[i] > max)
			max = array[i];
	}

	return min, max;
}
````
