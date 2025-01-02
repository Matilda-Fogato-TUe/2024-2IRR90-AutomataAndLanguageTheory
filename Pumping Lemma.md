`Homework assignment 2`
`Matilda Fogato`
`1656376`
`13/12/2024`

The language $L \subseteq \{ 0,1,\# \} ^*$ is given by $$L= \{ u \# w \; | \; u,w \in \{0,1 \}^* \text{and } u \text{ is a substring of } w \} $$
Prove, by application of the Pumping Lemma for context-free languages, considering no more than five subcases, that $L$ is _not_ a context-free language. 
# Proof
Suppose that $L$ is a context-free language. Pick a pumping length $p > 0$, which exists by the pumping lemma, and consider the word $s=0^p1^p\#0^p1^p$. Clearly, $|s| \geq p$, and $s \in L$. Consider an arbitrary 5-split $s=uvxyz$ such that $|vxy| \leq p$ and $|vy| > 0$. By the pumping lemma, $uv^i xy^i z \in L$ for all $i \in \mathbb{N}$.
We obtain a contradiction by showing that we can always find $i$ such that $uv^i xy^i z \notin L$. 
## Case 1: $vxy$ only includes symbols before the $\#$
Since $|vxy| \leq p$, the string obtained by pumping up, i.e. $s_2 = uv^2 x y^2 z$,  will not be in $L$.
By adding symbols to the $u$ part of the word, $u$ can no longer be a substring of $w$ (and $w$ would not necessarily be a substring of $u$ either).
## Case 2: $vxy$ only includes symbols after the $\#$
Since $|vxy| \leq p$, the string obtained by pumping down, i.e. $s_0 = u v^0 x y^0 z$, will not be in $L$.
By removing symbols from the $w$ part of the word, $u$ will no longer be a substring of $w$.
## Case 3: the substring $vxy$ straddles the $\#$, and includes symbols from both part $u$ and $w$ of the word
Because $|vxy| \leq p$, the substring $vxy$ will be of the form $1^n \# 0^m$, with either  $n \leq \frac{p}{2}$ and $m < \frac{p}{2}$,  or $n < \frac{p}{2}$ and $m \leq \frac{p}{2}$, with $n,m \in \mathbb{N}$.
If $vy$ contains $\#$, the string obtained by pumping down, i.e. $s_0 = u v^0 x y^0 z$, will not be in $L$.
Trivially, the word will no longer be in the shape $u \# w$, since it will no longer contain the symbol $\#$. 
If $vy$ does not contain $\#$, we can distinguish two sub-cases. 
* If there are more 1s than 0s, the string obtained by pumping up, i.e. $s_2 = uv^2 x y^2 z$,  will not be in $L$. By adding symbols (appending more ones) to the $u$ part of the word, $u$ can no longer be a substring of $w$.
* If there are more 0s than 1s, the string obtained by pumping down, i.e. $s_0 = u v^0 x y^0 z$, will not be in $L$. By removing symbols (deleting the initial zeroes) from the $w$ part of the word, $u$ will no longer be a substring of $w$.

In each case, a counterexample could be found, so we can conclude that the language $L$ is not context-free.