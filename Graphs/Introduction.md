# Introduzione ai grafi
## Definizione
Un grafo è un insieme di nodi collegati da archi.
L'insieme degli archi è chiamato $E$, mentre l'insieme dei nodi è chiamato $V$.

// immagine

## Termini usati
- Un arco può essere *pesato*, ovvero contenere un certo valore;
- Gli archi possono essere *orientati*, ovvero essere percorsi in una sola direzione, oppure *non orientati*;
- Due nodi connessi direttamente da un arco vengono chiamati *adiacenti*;
- Un **cammino** è una sequenza di nodi che sono uniti da archi, possono esistere diversi tipi di cammini:
	- Cammino semplice, dove un cammino può passare da ogni nodo più volte;
	- Cammino hamiltoniano, è un cammino che passa da ogni nodo esattamente una volta.
- I cammini possono essere infiniti, ovvero non avere nè inizio nè fine;
- Il costo di un cammino è la somma dei costi degli archi attraversati;
- Un grafo è *connesso* se è possibile raggiungere qualsiasi nodo da qualsiasi altro nodo (anche indirettamente);
- Un grafo è chiamato *ciclico* se contiene dei cammini infiniti, altrimenti viene chiamato *aciclico*;
- Un **DAG** (Directed Acyclic Graph) è un grafo orientato aciclico;
- Il *grado* di un nodo è il numero di archi in entrata e uscita, in particolare:
	- Il grado *entrante* è il numero di archi in entrata di tale nodo;
	- Il grado *uscente* è il numero di archi in uscita di tale nodo.
- Un grafo è *completo* se ogni nodo è adiacente a qualsiasi altro nodo (in questo caso, $|E| = |V^2|$).

## Rappresentazione di un grafo
Un grafo può essere rappresentato (in un algoritmo) in due modi:

#### Tramite liste di adiacenza
Viene usato un array in cui ogni cella rappresenta un nodo del grafo ed è la testa di una lista concatenata che contiene i nodi raggiungibili da tale nodo.
E' la tecnica solitamente usata.

// immagine

###### Complessità operazioni
- Calcolo del grado uscente di un nodo: $\Theta(V)$;
- Calcolo della somma dei gradi uscenti: $\Theta(V+E)$, perchè esploro tutta la lista (se il grafo è completo, $\Theta(V^2)$);
- Calcolo del grado entrante di un nodo: $\Theta(V+E)$.

#### Tramite matrici di adiacenza
Viene usata una matrice, dove le righe sono i nodi sorgenti degli archi e le colonne i nodi destinazione.
Dato un cammino $(i, j)$ metto $1$ in ```matrix[i][j]``` se il cammino esiste ($\in E$), altrimenti $0$.
Occupa sempre $|V^2|$ memoria.

###### Complessità operazioni
- Calcolo del grado uscente di un nodo: $\Theta(V)$;
- Calcolo della somma dei gradi uscenti: $\Theta(V^2)$;
- Calcolo del grado entrante di un nodo: $\Theta(V)$, pechè basta guardare la colonna del nodo.