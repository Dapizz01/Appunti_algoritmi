# Introduzione ai grafi
## Definizione
Un grafo è un insieme di nodi collegati da archi.
L'insieme degli archi è chiamato $E$, mentre l'insieme dei nodi è chiamato $V$.

![Esempio di grafo](Images/base_graph.png)
*Esempio di grafo*

## Termini usati
- Un arco può essere *pesato*, ovvero contenere un certo valore;
- Gli archi possono essere *orientati*, ovvero essere percorsi in una sola direzione, oppure *non orientati*;
- Due nodi connessi direttamente da un arco vengono chiamati *adiacenti*;
- Un **cammino** è una sequenza di nodi che sono uniti da archi, possono esistere diversi tipi di cammini:
	- Cammino semplice, dove un cammino può passare da ogni nodo più volte;
	- Cammino hamiltoniano, è un cammino che passa da ogni nodo esattamente una volta.
- I cammini possono essere infiniti, ovvero non avere nè inizio nè fine;
- Il costo di un cammino è la somma dei costi degli archi attraversati;
- Un **cammino** si dice **minimo** ($u$, $v$) se è il cammino con costo minore con sorgente $u$ e destinazione $v$.
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

![Esempio di grafo rappresentato con liste di adiacenza](Images/list_graph.png)
*Esempio di grafo rappresentato con liste di adiacenza*

###### Complessità operazioni
- Calcolo del grado uscente di un nodo: $\Theta(V)$;
- Calcolo della somma dei gradi uscenti: $\Theta(V+E)$, perchè esploro tutta la lista (se il grafo è completo, $\Theta(V^2)$);
- Calcolo del grado entrante di un nodo: $\Theta(V+E)$.

#### Tramite matrici di adiacenza
Viene usata una matrice, dove le righe sono i nodi sorgenti degli archi e le colonne i nodi destinazione.
Dato un cammino $(i, j)$ metto $1$ in ```matrix[i][j]``` se il cammino esiste ($\in E$), altrimenti $0$.
Occupa sempre $|V^2|$ memoria.

![Esempio di grafo rappresentato attraverso una matrice di adiacenza](Images/table_graph.png)
*Esempio di grafo rappresentato con una matrice di adiacenza*

###### Complessità operazioni
- Calcolo del grado uscente di un nodo: $\Theta(V)$;
- Calcolo della somma dei gradi uscenti: $\Theta(V^2)$;
- Calcolo del grado entrante di un nodo: $\Theta(V)$, pechè basta guardare la colonna del nodo.

## Grafi bipartiti
Un grafo bipartito è un grafo i cui nodi possono essere divisi in due regioni indipendenti, dove i nodi di ogni regione sono direttamente connessi con solo nodi dell'altra regione.

![Esempio di grafo bipartito](Images/bipartite.svg)
*Esempio di grafo bipartito*

Per verificare che un grafo è bipartito è sufficente eseguire un algoritmo di visita sul grafo ([[BFS]] o [[DFS]]) marcando ogni nodo come appartenente ad una regione e ogni vicino diretto come appartenente all'altra regione.
Se durante la visita viene rilevato un conflitto (ovvero, due nodi adiacenti appartengono alla stessa regione), significa che il grafo non è bipartito.

// esempio