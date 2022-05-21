# Algoritmi
## Descrizione
#### Scopo e contenuto
Qui vengono riassunti gli argomenti chiave per passare la parte delle crocette dell'esame di Algoritmi (e anche per la parte teorica delle domande aperte, ma senza esempi di esercizi veri e propri).
#### Convenzioni adottate
In questo riassunto vengono adottate molte convenzioni usate anche dal docente, ma con alcune piccole differenze:
- Gli array partono con indice 1, come da lezione;
- I nomi delle variabili sono modificati per rendere più scorrevole la lettura degli algoritmi.
- La sintassi usata in questo testo è un misto C - pseudocodice, adottata principalmente per avere un corretto highlighting del codice.

## Calcolo complessità
Di questa parte viene sempre fatta una domanda all'esame, che verte esclusivamente sul [[Master_theorem | Master Theorem]] (o Tema del Maestro).

## Sorting
C'è sempre una parte di crocette sugli algoritmi di sorting, ma riguardano solamente [[#^48e514|questi parametri]].

##### Definizione del problema
**Input**: sequenza $(a_1, a_2, ..., a_n)$ di oggetti su cui è definita una relazione di ordinamento totale (ovvero, tutti gli oggetti sono comparabili fra loro).
**Output**: permutazione (o riordinamento) degli oggetti in ordine non decrescente.

##### Valutazione degli algoritmi

^48e514

La valutazione degli algoritmi avviene attraverso 3 parametri:
* **Complessità temporale**: è il numero di iterazioni massime che può compiere un algoritmo. Per gli algoritmi di sorting, non può essere minore di $\boldsymbol{O(n\log(n))}$.
* **Ordinamento in loco**: indica se la complessità spaziale dell'algoritmo è costante oppure no.
* **Stabilità**: un algoritmo è stabile se l'ordine degli elementi con lo stesso valore non viene alterata

##### Algoritmi di sorting
* [[Insertion_sort#|Insertion sort]]
* [[Merge_sort|Merge sort]]
* [[Heap_sort|Heap sort]]
* [[Quick_sort|Quicksort]]

## Sorting lineare

