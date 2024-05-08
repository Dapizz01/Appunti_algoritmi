# Counting sort
## Caratteristiche
Complessità: $\boldsymbol{\Theta(n)}$
Ordina in loco: **NO**
Stabile: **SI**
Condizione: deve essere noto un limite superiore al valore degli elementi (nell'algoritmo, ```int max```).

## Descrizione
Counting sort verte sul conoscere in anticipo un limite massimo di valore degli elementi (es: se l'elemento con valore più grande è $n$, allora $max\ge n$ ).

Viene inoltre usato un array di supporto (chiamato d'ora in poi **counter**, così valorizzato:

![Esempio del contenuto di counter. Notare che A è l'array di input, C ed S i vari stati assunti da counter](https://www.researchgate.net/profile/Bruno-Feijo-2/publication/220686480/figure/fig4/AS:667707569614851@1536205298801/Example-of-counting-sort.png)
*Esempio del contenuto di counter. Notare che A è l'array di input, C ed S i vari stati assunti da counter*

Nello stato C (corrispondente al secondo ciclo for) counter[i] contiene, per ogni cella, il numero di volte in cui compare i nell'array di input.

Nello stato S invece (terzo ciclo for) counter contiene, per ogni distinto valore che può essere contenuto nell'array, l'indice destro in cui deve essere posizionato nell'array risultante.

Viene infine usato usato counter per popolare l'array risultante.

## Codice
````c
void counting_sort(int array_in[], int array_out[], int max){
	int counter[max];

	// Popolo counter di 0
	for(int i = 1; i <= max; i++)
		counter[i] = 0;

	// Conto quanti elementi di valore n ci sono
	// in array_in e metto la frequenza i questi valori
	// in counter[n]
	for(int j = 1; j <= length(array_in); j++)
		counter[array_in[j]]++;

	// Metto in counter[n] quanti elementi di valore <= n
	// ci sono in array_in
	for(int i = 2; i <= max; i++)
		counter[i] += counter[i - 1];

	// Ora counter[n] contiene l'indice più a dx in cui
	// posizionare n

	// Itero array_inda dx verso sx, e metto array_in[j]
	// in array_out all'indice counter[array_in[j]]
	for(int j = length(array_in); j >= 1; j--){
		array_out[counter[array_in[j]]] = array_in[j];
		
		// Decremento la cella di counter usata, perchè
		// ho usato una posizione
		counter[array_in[j]]--;
	}
}
````
## Dimostrazione

## Animazione
[Counting sort](https://www.youtube.com/watch?v=7zuGmKfUt7s)