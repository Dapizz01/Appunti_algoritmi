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

##### Caratteristiche degli algoritmi

^48e514

Le caratteristiche degli algoritmi sono descritte attraverso 3 parametri:
* **Complessità temporale**: è il numero di iterazioni massime che può compiere un algoritmo. Per gli algoritmi di sorting, non può essere minore di $\boldsymbol{O(n\log(n))}$ (in media).
* **Ordinamento in loco**: indica se la complessità spaziale dell'algoritmo è costante oppure no.
* **Stabilità**: un algoritmo è stabile se l'ordine degli elementi con lo stesso valore (ordine relativo) non viene alterato.

##### Algoritmi di sorting
* [[Insertion_sort#|Insertion sort]]
* [[Merge_sort|Merge sort]]
* [[Heap_sort|Heap sort]]
* [[Quick_sort|Quicksort]]

## Sorting lineare
Come per [[#Sorting]], ma gli algoritmi lineari di sorting hanno delle limitazioni (da sapere).

##### Algoritmi di sorting lineare
- [[Counting_sort|Counting sort]]
- [[Radix_sort|Radix sort]]
- [[Bucket_sort|Bucket sort]]

## Selezione
Capitano raramente domande sugli algoritmi di selezione e nel caso, sono riguardo i soliti parametri.

##### Definizione del problema
**Input**:
- Array su cui è definita una relazione di ordinamento (ma non è detto che sia ordinato)
- Indice $i$ compreso tra 1 e $n$, dove $n$ è il numero di elementi nell'array
**Output**: Valore che, nell'array ordinato, occupa la posizione $i$

##### Limiti sulle complessità
Gli algoritmi di selezione hanno complessità al massimo $O(n\log(n))$, perchè è la complessità minima degli algoritmi di ordinamento, in cui basta ordinare l'array e restituire l'elemento $i$.

Hanno complessità minima $\Omega(n)$ perchè è necessario controllare ogni elemento dell'array in input.

##### Algoritmi di selezione
- [[Min_max]]
- [[Randomized_select]]

## Strutture dati
Ci sono sempre crocette sulle complessità delle strutture dati, e vengono anche usate molto spesso negli esercizi.

#### Strutture dati viste
- [[RB_tree|RB-alberi]]
- [[Binomial_heap|Heap binomiali]]

## Approcci di programmazione
## Altre strutture dati
## Grafi
