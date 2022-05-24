# Insiemi disgiunti
## Caratteristiche
##### Con liste concatenate
Complessità make_set: $\boldsymbol{O(1)}$
Complessità union: $\boldsymbol{O(n)}$
Complessità find_set: $\boldsymbol{O(1)}$
Costo di $m$ operazioni di cui $n$ make_set: $\boldsymbol{O(m + n^2)}$
Costo di $m$ operazioni di cui $n$ make_set (con **campo aggiuntivo**): $\boldsymbol{O(m+n\log(n))}$.

##### Con alberi
Complessità make_set: $\boldsymbol{O(1)}$
Complessità union: $\boldsymbol{O(n)}$
Complessità find_set: $\boldsymbol{O(n)}$
Costo di $m$ operazioni di cui $n$ make_set: $\boldsymbol{O(mn)}$
Costo di $m$ operazioni di cui $n$ make_set (con **campo aggiuntivo**): $\boldsymbol{O(m+m\log(n))}$.
Costo di $m$ operazioni di cui $n$ make_set (con **compressione dei cammini**): $\boldsymbol{O(m)}$.

## Definizione
Sono una collezione di insiemi dinamici a 2 a 2 disgiunti. 
Gli insiemi contengono oggetti di un insieme $(x_1, ..., x_n)$.

Gli insiemi sono sempre distinti fra loro (se due insiemi hanno gli stessi elementi allora sono lo stesso insieme).

Viene definito **oggetto rappresentante** l'unico oggetto di un insieme che rappresenta tale insieme, usato per capire se due oggetti $x$ e $y$ appartengono allo stesso insieme.

## Operazioni
Sono 3 le operazioni fatte sugli insiemi disgiunti:
1. make_set(x), costruisce un nuovo insieme composto dall'elemento $x$.
2. union(x, y), unisce gli insiemi a cui appartengono gli elementi $x$ e $y$.
3. find_set(x), restituisce il rappresentante dell'insieme a cui appartiene $x$.

## Implementazioni
### Implementazione con liste concatenate
Ogni insieme è una lista concatenata di elementi.
La testa della lista è l'elemento rappresentante, ed ogni elemento punta direttamente al rappresentante (oltre al prossimo elemento nella lista).

![Rappreentazione di un insieme disgiunto implementato come lista](Images/disjoint_set.png)
*Rappreentazione di un insieme disgiunto implementato come lista*

#### Complessità
La complessità delle operazioni è:
- make_set(x), complessità $O(1)$;
- union(x, y), complessità $O(n)$;
- find_set(x), complessità $O(1)$.

Le operazioni make_set e find_set hanno complessità costante perchè basta prendere la testa della lista, mentre la union ha complessità lineare perchè deve concatenare le liste ed aggiornare i puntatori a rappresentante.

#### Costo $\boldsymbol{n}$ operazioni di cui $\boldsymbol{m}$ make_set
Se eseguo $n$ operazioni di cui $m$ make_set, il costo è di $O(m + n^2)$, dove $m$ è il costo delle make_set, perchè la union ha costo lineare e itera su $1 + 2 + 3 + ... + n = n^2$ elementi.

##### Soluzione alternativa (unione per rango)
Una soluzione per diminuire il costo à aggiungere un nuovo campo che punta direttamente alla coda della lista.
Tale campo va modificato (in una union) solo nel rappresentante, quello degli altri elementi non viene considerato.

![Esempio di insieme disgiunto implementato come lista con il campo tail](Images/ranked_disjoint_set.png)
*Esempio di insieme disgiunto implementato come lista con il campo tail*

E' possibile inoltre usare la tecnica di unione per rango, ovvero le liste più piccole vengo accodate a quelle più grandi.

L'aggiunta del nuovo campo con la tecnica di unione per rango riduce il costo di $m$ operazioni di cui $n$ make_set a $O(m + n\log(n))$.

Il costo diminuisce perchè in un elemento viene cambiato il puntatore a rappresentante solo se è l'elemento della lista più piccola in una union.
Chiamando *big* la lista più grande e _small_ la lista più piccola, si ha che $big \ge small$, formando una lista unica (*bigger*), di dimensione $bigger = big + small$.
Iterando nuovamente si può notare che *small* diventerà al massimo $\frac{1}{4}$ della nuova lista.
Dato che ad un elemento può essere cambiato il puntatore al massimo $\log(n)$ volte e che viene cambiato il puntatore a rappresentante di tutti gli elementi (almeno la metà), si ha che la complessità è $O(m + n\log(n))$.

### Implementazione con liste ordinate
Gli insiemi disgiunti sono rappresentati da alberi, in cui la radice è il rappresentante.
Gli alberi sono esplorati dalle foglie verso la radice (il contrario rispetto agli altri alberi usati finora).

// immagine

#### Complessità
La complessità delle operazioni è:
- make_set(x), complessità $O(1)$;
- union(x, y), complessità $O(n)$;
- find_set(x), complessità $O(n)$.

La operazione make_set ha complessità costante perchè crea un singolo nodo dell'albero, mentre union ha costo lineare perchè bisogna scorrere gli alberi per arrivare alle radici (stesso discorso per find_set).

Da notare che non sono [[RB_tree|RB-alberi]], quindi possono degenerare in una lista.

#### Costo $\boldsymbol{n}$ operazioni di cui $\boldsymbol{m}$ make_set
Se eseguo $n$ operazioni di cui $m$ make_set, il costo è di $O(mn)$, dove $m$ è il costo delle make_set, perchè la union e la find_set hanno complessità lineari.

La complessità è quindi maggiore rispetto all'[[#Implementazione con liste concatenate]].

##### Soluzione alternativa (unione per rango)
Come nelle [[#Soluzione alternativa unione per rango|liste concatenate]] è possibile diminuire il costo delle operazioni con l'unione per rango, in cui, nella union, l'albero con rango (profondità dell'albero) più grande diventa radice dell'albero con rango minore.

Ciò inoltre consente di evitare la degenerazione da albero a lista, infatti l'unione per rango assicura che l'albero ha profondità $\le \log(n)$.

La soluzione ha complessità $O(m\log(n))$, comunque peggiore della controparte.

##### Soluzione alternativa (compressione dei cammini)
La tecnica di compressione dei cammini riprende il concetto di [[Dynamic_programming|memoizzazione]], ovvero, quando viene attraversato un cammino foglia-radice e il prossimo elemento non è la radice, faccio puntare il puntatore a parent del nodo direttamente alla radice.

Questo consente di non dover passare dagli stessi nodi per più di una volta e di ridurre il costo per arrivare alla radice.

// immagine

**Codice compressione dei cammini**
````c
int find_set(Node x){
	// La root ha puntatore a parent, ma punta a sè stesso
	if(x != x.parent){
		// Aggiorno il puntatore a parent con la root
		x.parent = find_set(x.parent);
	}

	// Ritorno la root, così i nodi più in basso vengono aggiornati
	return x.parent;
}
````

La tecnica di compressione dei cammini rende la find_set costante (dimostrato con la funzione di Ackermann), che porta la complessità del problema a $O(m)$.