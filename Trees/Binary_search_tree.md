# Albero binario di ricerca
Usato in:
- [[RB_tree|RB-alberi]]

## Caratteristiche
Complessità ricerca nodo: $\boldsymbol{\Theta(\log(n))}$
Complessità aggiunta nodo: $\boldsymbol{O(n)}$
Complessità rimozione nodo: $\boldsymbol{O(n)}$

## Descrizione
Un albero binario di ricerca è un [[Binary_tree|albero binario]] in cui vige una relazione di ordinamento (similarmente ad uno [[Heap|heap]]), in particolare, per ogni nodo $x$:
- Tutti i nodi del sotto albero radicato nel figlio sinistro di $x$ hanno chiave < della chiave di x;
- Tutti i nodi del sotto albero radicato nel figlio destro di $x$ hanno chiave > della chiave di x;

Questa relazione permette di trovare un qualsiasi elemento all'interno dell'albero con complessità $\Theta(\log(n))$ ovvero pari all'altezza dell'albero.

Da notare inoltre che un albero binario di ricerca può degenerare in una lista (ovvero, ogni nodo ha un solo figlio) ed aumentare il tempo di ricerca a $O(n)$.