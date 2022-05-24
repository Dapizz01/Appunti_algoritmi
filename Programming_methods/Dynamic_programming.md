# Programmazione dinamica
## Descrizione
La programmazione dinamica prevede la suddivisione del problema in sotto problemi, da risolvere usando un approccio bottom-up o top-down. 

Si basa inoltre sulla **tecnica di memoizzazione**, ovvero:
risolvo i sotto problemi in modo ricorsivo, memoizzo i risultati ed ogni volta che incontro un problema cerco se il problema è già stato memoizzato. Se lo è restituisco il risultato, altrimenti lo calcolo.

## Passi da seguire
1. Prendere il problema e dargli una caratterizzazione ricorsiva con una sottostruttura ottimale;
2. Andare a contare il numero di istanze distinte (senza ripetizioni);
3. Ordino le istanze in modo crescente;
4. Costruisco l'algoritmo iterativo che risolve i problemi in modo crescente;
5. Scrivo l'algoritmo ricorsivo usando la tecnica di memoizzazione, con una complessità pari all'algoritmo iterativo.
