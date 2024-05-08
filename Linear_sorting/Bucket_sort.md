# Bucket sort
## Caratteristiche
Complessità: $\boldsymbol{\Theta(n)}$ in media, ma tempo pessimo $\boldsymbol{\Theta(n^2)}$
Ordina in loco: **NO**
Stabile: **SI**
Condizione: deve essere nota la distribuzione di probabilità dei valori in input.

## Descrizione
Bucket sort sfrutta la distribuzione di probabilità dei valori per dividere i valori in gruppi ("bucket") equiprobabili.

Ogni bucket è una lista concatenata, che contiene i valori appartenenti a quel bucket.

![Esempio di bucket sort](http://www.geeksforgeeks.org/wp-content/uploads/BucketSort.png)
*Esempio di bucket sort*

Nell'esempio sopra, i valori di input sono distribuiti in 10 bucket, ognuno contenente i valori in un certo intervallo (es: il bucket 0 contiene i valori $n$ tali che $0 \le n \lt 0.1$, mentre il bucket 6 gli $n$ tali che $0.6 \le n \lt 0.7$).

I valori sono poi inseriti nei corrispettivi bucket usando [[Insertion_sort|insertion sort]].