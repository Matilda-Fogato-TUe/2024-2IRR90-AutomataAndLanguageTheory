```
Homework assignment 3
Matilda Fogato
1656376
07/01/2025
```

Consider the language $Double_{TM}$ given by $$Double_{TM} = \{ \langle M \rangle \; | \;\text{if TM } M \text{ halts on input } w \text{ then } M \text{ diverges on input } ww \}$$
Prove that the language $Double_{TM}$ is undecidable by a reduction from $\mathcal{A}_{TM}$.
# Proof
We assume that $Double_{TM}$ is decidable, and use that assumption to show that $\mathcal{A}_{TM}$ is decidable as well, reaching a contradiction.
Assume that we have a TM $R$ that decides $Double_{TM}$. We construct the TM $S$ to decide $\mathcal{A}_{TM}$, with $S$ operating as follows.
TM $S$ = "on input $\langle M,w \rangle$, the code of a TM $M$ and a string $w$:
* Transform $\langle M, w \rangle$ into $\langle M' \rangle$, where TM $M'$ = "on input $x$:
	* If $x = ww$:
		* Simulate $M$ on $w$
		* If $M$ accepts $w$, accept $x$
		* Otherwise, diverge on $x$
	* Else: accept $x$"
* Run $R$ on input $\langle M' \rangle$
	* If $R$ accepts, then __reject__ $\langle M, w \rangle$
	* If $R$ rejects, then __accept__ $\langle M, w \rangle$"

Since $R$ is a decider, $S$ is one as well. Furthermore, we have that 
$S$ accepts $\langle M, w \rangle$
$\iff R$ rejects $\langle M' \rangle$ (acceptance and rejection of $S$ and $R$ are swapped by construction)
$\iff$ if $M'$ halts on input $w$, it also halts on input $ww$ (by definition of $Double_{TM}$)
$\iff M'$ accepts both $w$ and $ww$ (by construction of $M'$)
$\iff M$ accepts input $w$ (by definition of $M'$)
$\iff \langle M, w \rangle \in \mathcal{A}_{TM}$ (by definition of $\mathcal{A}_{TM}$)

So, $S$ decides $\mathcal{A}_{TM}$, which contradicts the undecidability of $\mathcal{A}_{TM}$. 
Therefore, the assumption that a TM $R$ decides $Double_{TM}$ is false. We conclude that $Double_{TM}$ is undecidable.
