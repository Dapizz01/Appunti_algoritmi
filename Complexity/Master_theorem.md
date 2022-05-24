# Master Theorem
Siano $a\ge1$, $b\gt1$ tali che **$$T(n) = aT(\dfrac{n}{b})+f(n)$$**
allora si hanno 3 casi:
1. Se $f(n) \in O(n^{\log_{b}(a)-\epsilon})$, con $\epsilon\gt0$, allora $$T(n) \in \Theta(n^{\log_{b}a})$$
2. Se $f(n) \in \Theta(n^{\log_{b}a})$, allora $$T(n) \in \Theta(f(n)\log n)$$ ^d0bdeb
3. Se $f(n) \in \omega(n^{\log_{b}a + \epsilon})$ , con $\epsilon \gt 0$, allora $$T(n) \in \Theta(f(n))$$ ma solo se $af(n) \le cf(n)$ per qualche $c \lt 1$, $n \gt \bar{n}$. ^bb725c

N.B. All'esame si possono presentare tutti i 3 i casi, ma del [[Master_theorem#^bb725c|terzo caso]] non è necessario gestire la condizione finale, dato che sicuramente il problema d'esame verte sul [[Master_theorem#|Master Theorem]].