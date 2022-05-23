# RB-albero
## Caratteristiche
Complessità aggiunta nodo: $\boldsymbol{O(\log(n))}$
Complessità estrazione nodo: $\boldsymbol{O(\log(n))}$
Complessità trasformazione in array: $\boldsymbol{\Theta(n)}$
Complessità costruzione RB-albero da array già ordinato: $\boldsymbol{\Theta(n)}$
Complessità costruzione RB-albero da array non ordinato: $\boldsymbol{\Theta(n\log(n))}$
Complessità selezione su RB-albero: $\boldsymbol{\Theta(\log(n))}$

#### Descrizione
Un RB-albero è un [[Binary_search_tree|albero binario di ricerca]] su cui valgono le seguenti proprietà:
1. Ogni nodo può essere rosso (red) o nero (black);
2. Ogni nodo foglia è di colore nero;
3. I figli di un nodo rosso sono neri;
4. Ogni cammino radice - foglia contiene lo stesso numero di nodi neri

![Esempio di RB-albero](https://cdn.programiz.com/sites/tutorial2program/files/red-black-tree_0.png)
*Esempio di RB-albero*

Notare che la proprietà 3. viene rispettata usando dei nodi NIL come nodi foglia neri.

#### Termini usati
- La **B-altezza** di un nodo X è il numero di nodi neri che si incontrano in un cammino da X ad una foglia, senza contare X;

#### Rotazione di un sotto albero
![Esempio di rotazione](https://i.stack.imgur.com/RVSev.png)
*Esempio di rotazione*

La rotazione di un sotto albero, come illustrato sopra, non viola le proprietà di un RB-albero ed ha complessità $\boldsymbol{\Theta(1)}$, perchè è una modifica locale e non coinvolge tutto l'albero

#### Inserimento nodo
Il nodo viene inserito nella corretta locazione che rispetta le proprietà degli [[Binary_search_tree|alberi binari di ricerca]].
Il colore del nodo viene messo di default come _rosso_.
L'inserimento del nodo può provocare un errore nell'RB-albero, ad esempio il nodo inserito può essere figlio di un altro nodo rosso ([[#Descrizione|proprietà 3.]]), dunque è necessario risolvere tali anomalie.

````c
void resolve_anomaly(Node son){
	// Ripeto l'algoritmo finchè non porto
	// l'anomalia alla radice o il padre ha colore BLACK
	while(son != ROOT && son.parent.color == RED){
		Node dad = son.parent;
		Node g_father = son.parent.parent;
		
		// Considero il caso in cui il padre è figlio sx del nonno.
		// Se è il figlio dx devo fare le stesse operazioni
		if(dad == g_father.left){
			Node uncle = g_father.right;
			
			// Se lo zio è RED come il padre, allora per forza
			// il nonno è BLACK (altrimenti non era un RB-albero valido)
			// quindi sposto l'anomalia verso l'alto.
			if(uncle.color == RED){
				dad.color = BLACK;
				uncle.color = BLACK;
				g_father.color = RED;
				son = g_father;
			}
			
			// Lo zio è BLACK
			// Entro nei casi terminali
			else{
				// Se il figlio è figlio dx del padre
				if(son == dad.right){
					son = dad;
					left_rotate(son);
				}
				
				// Il figlio è sx
				else{
					dad.color = BLACK;
					g_father.color = RED;
					right_rotate(g_father);
					x = ROOT;
				}
			}
		}
		
		// Il padre è figlio destro del nonno
		// Fa le stesse operazioni dell'if precedente, ma speculare
		else{
			...
		}
	}
}
````