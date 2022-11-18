---
{"dg-publish":true,"permalink":"/fleeting-notes/game-theory-the-shapley-value/"}
---


# The Shapley Value -- Game Theory

LIoyd Shapley's idea: members should receive payments or share proportional to their marginal contributions.

Axiom
- Symmetry: For any v, if i and j are interchangeable then $\psi_i(N, v) = \psi_j(N, v)$
- Dummy players: if i is a dummy player then $\psi_i(N,v) = 0$
- Additivity: if we can separate a game into two parts v = v1 + v2, then we should be able to decompose the payments

Given a coalitional game(N, v), there is a unique payoff division $x(v) = \Phi(N, v)$ that divides the full payoff of the grand coalition and that satisfies the Symmetry, Dummy player and additivity axioms: the Shapley Value
$$\Phi_i(N, v) = \frac{1}{N!}\sum_{S\subseteq N/\{i\}} |S|!(|N|-|S|-1)![v(S\cup\{i\})-v(S)]$$
- |S|! ways the set S could be formed prior $i$'s addition, |S| the number of S set
- (|N|-|S|-1)! ways the remaining players could be added
- Sum over all possible sets S and average by dividing by |N|!: the number of possible orderings of all the agents

example: 
![](https://s2.loli.net/2022/07/13/FwPZvu1WVI2DoGd.png)
## Summary
- The Shapley Value allocates the value of a group according to marginal contribution calculations
- Captured by some simple axioms and logic
- Other axioms and approaches lead to other allocations of value
	- [ ] for example the 'Core' 



[GTO-7-03: The Shapley Value - YouTube](https://www.youtube.com/watch?v=qcLZMYPdpH4)