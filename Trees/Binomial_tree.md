# Albero binomiale
## Descrizione
Un albero binomiale è un albero (non [[Binary_tree|binario]]), definito induttivamente come:
- Albero binomiale di base è costituito da un solo nodo;
- L'albero binomiale $k+1$ è l'unione di due alberi binomiali $K$, dove un albero binomiale $K$ diventa figlio "più sinistro" dell'altro albero.

![](https://static.packt-cdn.com/products/9781785888731/graphics/image_12_003.jpg)
*Esempi di alberi binari di rango differente. Notare come un albero binomiale di rango K ha come figlio sinistro un albero binomiale di dimensione K-1*

#### Proprietà
In un albero binomiale di rango $K$:
- Ci sono $2^K$ nodi;
- L'altezza è $K$;
- I figli della radice, da sinistra verso destra, sono alberi binomiali di rango $K-1 ... 0$;
- Uno heap binomiale di rango $K$ ha $2^K$ nodi.

![Esempio dell'ultima proprietà descritta](https://static.packt-cdn.com/products/9781785888731/graphics/image_12_006.jpg)
*Esempio dell'ultima proprietà descritta*