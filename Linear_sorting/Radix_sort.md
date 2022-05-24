# Radix sort
## Caratteristiche
Complessità: $\boldsymbol{\Theta(n)}$
Ordina in loco: **NO**
Stabile: **SI**
Condizione: l'algoritmo è efficiente solo se i valori in input non hanno un alto numero di cifre.

## Descrizione
Radix sort ordina i valori in input confrontando fra loro le cifre nella stessa posizione, dalle cifre meno significative (quindi da destra verso sinistra).

![Esempio di esecuzione di radix sort](https://ds055uzetaobb.cloudfront.net/brioche/uploads/IEZs8xJML3-radixsort_ed.png?width=1200)
*Esempio di esecuzione di radix sort*

Viene solitamente usato [[Counting_sort|counting sort]] per ordinare i numeri in base alle cifre (dato che le cifre hanno valore fra 0 e 9).

## Dimostrazione
La complessità è $\Theta(kn)$, perchè applica per un numero limitato di volte [[Counting_sort|counting sort]], dove $k$ è il numero di cifre massimo, mentre $n$ è il numero di elementi. Dato che il numero di cifre solitamente è basso, si può approssimare a $\Theta(n)$.

Non ordina in loco perchè [[Counting_sort|counting sort]] non ordina in loco.

E' stabile, perchè [[Counting_sort|counting sort]] è stabile.

## Animazione
[Radix sort](https://www.youtube.com/watch?v=LyRWppObda4)