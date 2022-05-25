# Tabelle hash
## Caratteristiche
Costo di accesso ad un elemento: $\boldsymbol{\Theta(1)}$

## Definizione
E' una struttura dati che associa ad una chiave un certo valore.
Non possono esistere oggetti uguali nella tabella.
Viene usata per l'associazione una funzione $H$ chiamata **funzione di hash**.

// immagine

Nelle tabelle hash una chiave viene trasformata nell'indice di un array, che contiene i valori da memorizzare.
Dato che il numero di chiavi possibili è maggiore del numero di celle dell'array, è possibile che ci siano dei conflitti, ovvero più chiavi diverse che puntano alla stessa cella dell'array.

Per diminuire i conflitti solitamente viene incrementata la dimensione dell'array, ma esistono anche altre tecniche.

## Tecniche di gestione dei conflitti
#### Tramite liste
Ogni cella dell'array diventa la testa di una lista ed un elemento viene quindi aggiunto in coda alla lista.

Se, per un elemento $x$, la funzione $H(x)$ restituisce l'indice di una cella già occupata, allora viene esplorata la lista, e:
- Se viene trovato un elemento $x'$ tale che $x=x'$, termina senza aggiungere $x$;
- Se non viene trovato un elemento uguale a $x$, $x$ viene aggiunto in coda.

// immagine

Nel caso peggiore, la tabella hash degenera in una lista, con tempo di accesso $O(n)$, ma in media è $\Theta(1 + \alpha)$, dove $\alpha$ è il numero di nodi nella coda, ovvero **costante**.

#### Indirizzamento aperto
Nell'inserimento dell'elemento $x$, se $H(x)$ punta a una cella dell'array già usata, scorre l'array finchè non trova una cella libera e mette il contenuto di $x$ in tale cella.

Può crearsi un fenomeno di aggregazione su alcune celle dell'array, ovvero alcune celle possono essere puntate molte volte dalla funzione $H$, mentre altre non lo sono mai.

Per risolvere questo problema è possibile usare due distinte funzioni hash e combinarle creando una nuova funzione hash (**hashing doppio**) $H(k, i) = (H_1(k) + iH_2(k)) \mod m$, dove $i$ è il numero di tentativi effettuati.
Viene calcolato l'hash dei tentativi con una funzione hash ($H_2$) diversa da quella usata normalmente per la chiave ($H_1$).

## Funzione hash
#### Metodo di divisione
Funzione: $\boldsymbol{H(k)\triangleq k\mod m}$, dove $m$ è la lunghezza dell'array.

Il parametro $m$ deve essere diverso da una potenza di 2 (altrimenti $H(k) = H(k + m)$), l'ideale è avere un $m$ primo e distante da una potenza di 2.

#### Metodo di moltiplicazione
Funzione: $\boldsymbol{H(k) \triangleq m(kA \mod 1)}$, dove $A$ è un numero reale fissato e $m$ è la lunghezza dell'array.
(Il risultato viene infine approssimato)

$(kA \mod 1)$ ritorna un valore $x$, dove $0 \le x \lt 1$, che moltiplicato per $m$ ritorna un $i$ tale che $0 \le i \lt m$.