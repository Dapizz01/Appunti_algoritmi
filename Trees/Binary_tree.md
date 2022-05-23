# Binary tree
Usato in:
- [[Binary_search_tree|Alberi binari di ricerca]]
- [[Heap]]

## Descrizione
E' un albero in cui ogni nodo può avere al massimo due figli, uno destro e uno sinistro.

![Esempio di albero binario](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)
*Esempio di albero binario*

#### Termini usati
- Un nodo si dice **root** (o radice) il primo nodo in cima all'albero;
- Si chiama **sotto albero** un sottoinsieme di nodi di un albero che formano un albero valido;
- Si chiamano **nodi foglia** i nodi che non hanno figli;
- Si chiama **altezza dell'albero** il percorso massimo che ha sorgente dalla root verso uno qualsiasi dei suoi figli.

#### Visite
Esistono 3 possibili modi per esplorare un albero binario:

**Pre visit**
````c
void pre_visit(Node node){
	if(node != null){
		visit(node);
		pre_visit(node.left);
		pre_visit(node.right);	
	}
}
````

**In visit**
````c
void in_visit(Node node){
	if(node != null){
		in_visit(node.left);
		visit(node);
		in_visit(node.right);	
	}
}
````

**Post visit**
````c
void post_visit(Node node){
	if(node != null){
		post_visit(node.left);
		post_visit(node.right);
		visit(node);	
	}
}
````

Date due visite qualsiasi, è possibile ricostruire un albero binario.