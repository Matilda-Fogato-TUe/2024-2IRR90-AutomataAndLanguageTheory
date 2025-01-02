`Homework assignment 1`
`Matilda Fogato`
`1656376`
`27/11/2024`

For a language $L \subseteq \Sigma^\*$, for some alphabet $\Sigma$, the language $\text{MID}(L)$ is given by $$\text{MID}(L) = \{ w \in \Sigma^* \, | \, \exists x,y \in \Sigma^* \, : xwy \in L \}$$
Thus, $\text{MID}(L)$ consists of strings from $L$, with some (possibly empty) beginning and ending missing. Prove that $\text{MID}(L)$ is a regular language if $L$ is a regular language.
# Proof
Let $D=(Q, \Sigma, \delta, q_0, F)$ be a DFA that recognizes the language $L$. We can construct an NFA $N = (Q', \Sigma, \delta', q'_0, F')$ as follows:
* $Q'=Q \times \{1, 2\}$
* $q'_0 = \{ q_0, 1\}$
* $F' = F \times \{1\}$
The transition function $\delta': Q' \times \Sigma \rightarrow Q'$ is defined as:
* $\delta'(\langle q_0, 1 \rangle, \epsilon) =$ $\{ \langle q', 2 \rangle \}$ where $q' \in Q$ and $\exists x \in \Sigma^*$ such that $(q_0, x) \vdash_D^* (q', \epsilon)$
* $\delta'(\langle q, 1 \rangle, a) = \emptyset$ for any $q \in Q$
* $\delta'(\langle q, 2 \rangle, a) = \{ \langle \delta(q, a),2 \rangle \}$ for $q \in Q$ and $a \in \Sigma$
* $\delta'(\langle q, 2 \rangle, \epsilon) = \{\langle q_f, 1 \rangle \}$ where $q_f \in F$ and $\exists y \in \Sigma^*$ such that $(q, y) \vdash_D^* (q_f, \epsilon)$
---
We claim that $\mathcal{L}(N) = \text{MID}(L)$. This can be seen as follows:
$w \in \mathcal{L}(N)$
$\iff \exists q_f \in F: (\langle q_0, 1 \rangle, w) \vdash_N^* (\langle q_f, 1 \rangle, \epsilon)$ \[by definition of $\mathcal{L}(N)$]
$\iff \exists q_f \in F, q', q'' \in Q: (\langle q_0, 1 \rangle, w) \vdash_N (\langle q', 2 \rangle, w) \vdash_N^* (\langle q'', 2 \rangle, \epsilon) \vdash_N (\langle q_f, 1 \rangle, \epsilon)$ \[by definition of $N$]
$\iff \exists q_f \in F, q',q'' \in Q, x,y \in \Sigma^* : (q_0, x) \vdash_D^*(q',\epsilon) \land (q', w) \vdash_D^* (q'', \epsilon) \land (q'', y) \vdash_D^* (q_f, \epsilon)$ \[by definition of $N$]
$\iff \exists q_f \in F, q',q'' \in Q, x,y \in \Sigma^* : (q_0, xwy) \vdash_D^*(q',wy) \land (q', wy) \vdash_D^* (q'', y) \land (q'', y) \vdash_D^* (q_f, \epsilon)$ \[by property of $\vdash_D^*$]
$\iff \exists q_f \in F, x,y \in \Sigma^* : (q_0, xwy) \vdash_D^* (q_f, \epsilon)$ \[by property of $\vdash_D^*$]
$\iff \exists x,y \in \Sigma^*: xwy \in \mathcal{L}(D)$ \[by definition of $\mathcal{L}(D)$]
$\iff \exists x,y \in \Sigma^*: xwy \in L$ \[by choice of $D$]
$\iff w \in \text{MID}(L)$ \[by definition of $\text{MID}(L)$]
So, $\text{MID}(L) = \mathcal{L}(N)$ is the language accepted by the NFA $N$. From this, we can conclude that $\text{MID}(L)$ is a regular language. 
