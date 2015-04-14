Lecture 7: Matching Problems
===

Given a graph G(V,E), a _matching_ is a subgraph (collection of edges) of G where
every node has degree 1.

*Example*

    V = 1 … 8
    E = {(1,2) (1,6) (1,7) (1,8) (2,5) (2,6) (3,5) (4,5) (5,6)}

    {(1,6) (2,5)} is a matching of size 2.
    {(1,7) (2,6) (3,5)} is a matching of size 3.

*Define* A matching is _perfect_ if it has size |V|/2 (ie. every node involved).

Some matchings might be more desirable than others (weighted graph). Usually you
want the minimum weight.

*Define* The _weight_ of a matching M is the sum of the weights of the edges in M.

*Define* A _min-weight matching_ for G is a perfect matching for G with the minimum
weight.

*Example*

    V = B, T, J, A
    E = {(B,J)=10 (B,A)=5 (T,J)=16 (T,A)=10}

    Min-weight matching: {(B,J) (T,A)} ≡ 20

Algorithms exist for finding the min-weight matching for a graph and usually run in
quadratic to cubic time.

Alternative problem: preferences instead of weights

    V = B, T, J, A
    E = {(B,A)=1 (B,J)=2 (T,A)=1 (T,J)=2 (J,B)=1 (J,T)=2 (A,B)=1 (A,T)=2}

*Define* Given a matching M, x & y form a _rogue couple_ if they prefer each other
over their mates in M. eg. {(B,J) (T,A)}, then (B,A) are a rogue couple.

*Define* A matching is _stable_ if there are no rogue couples.

So the goal is to find a perfect matching that is stable. In the above case
{(B,A) (T,J)} is the stable matching. People may not get their preference but no one
prefers someone else over their mate.

Stable matches can always be found if the graph is composed of two groups. If the
nodes are homogeneous then it's impossible to avoid rogue couples.

**Theorem** There is no stable matching in the following graph:

    V = A, R, B, M
    E = {(A,R)=2 (A,B)=1 (R,A)=1 (R,B)=2 (B,A)=2 (B,R)=1 (A,M)=(R,M)=(B,M)=3}

*Proof by contradiction*

    Assume there exists a stable matching S. Then M matched w/ someone in S.
    WLOG (by symmetry) assume M matched with A. So {(A,M) (R,B)} but then (A,R) are
    a rogue couple so S not stable.

Stable Marriage Problem
---

* N boys & N girls.
* Each boy has his own ranked list of the girls.
* Each girl has her own list.

Goal is to find a perfect matching with no rogue couples.

    N = 5

    B1: C B E A D     GA: 3 5 2 1 4
    B2: A B E C D     GB: 5 2 1 4 3
    B3: D C B A E     GC: 4 3 5 1 2
    B4: A C D B E     GD: 1 2 3 4 5
    B5: A B D E C     GE: 2 3 4 1 5

*Greedy algorithm*

    1 → C got their top pref, so no rogue coupling
    2 → A "
    3 → D "
    4 → B but rogue couple (4,C)
    5 → E but rogue couple (5,B)

So this doesn't work…

Instead use the *The Mating Algorithm* (TMA). Iterates as follows:

  1. Every boy serenades the top girl still on his list.
  2. Girls who have ≥ 1 suitor pick their favourite and tell them to return.
  3. Everyone else is rejected.
  4. Boys that have been rejected remove that girl from their list.
  5. If *every* girl has ≤ 1 suitor then stop.

*Example*

    Serenaders
    Girls     Day 1     Day 2     Day 3     Day 4
    -------------------------------------------------
    A         2 4 5     5         5         5
    B         -         2         2 1       2
    C         1         1 4       4         4
    D         3         3         3         3
    E         -         -         -         1

    Cross-outs
    Boys
    -------------------------------------------------
    1                   C         B
    2         A
    3
    4         A
    5

Need to show:

  * The algorithm terminates (quickly).
  * Everyone gets mated.
  * No rogue couples.
  * Fairness.

**Theorem 1** TMA terminates in ≤ N²+1 iterations.

*Proof by contradiction* Suppose TMA does not terminate in N²+1 days.

    Claim: if we don't terminate on an iter, then at least one boy crosses at least
    one girl off their list.

    N lists w/ N names ⇒ ≤ N² crossouts. So > N²+1 crossouts aren't possible.
    Contradiction. The algorithm has to terminate within N²+1 iterations max.

Let P: "If a girl G ever rejected a boy B then G has a suitor who she prefers to B."

**Lemma 1** P is an invariant for TMA.

*Proof by induction* on # iters.

    Base case: Iter 0 - no one rejected yet ⇒ vacuously true.
    Induction step: Assume P holds at the end of iteration i.
      Case 1: G rejects B on iteration i+1, then better suitor ⇒ P true at i+1
      Case 2: G rejected B before iteration i+1, P ⇒ G had a better suitor at i

    ⇒ G has same or better suitor at i+1
    ⇒ P true on i+1. QED

**Theorem 2** Everyone is mated in TMA.

*Proof by contradiction* Assume that some boy B is not mated ⇒ B was rejected by
every girl ⇒ every girl has a better suitor (lemma 1) ⇒ every girl mated ⇒ every
boy mated. Contradiction.

**Theorem 3** TMA produces a stable matching.

*Proof* Let (B,G) be _any_ pair that are not mated. 

Case 1: G rejected B ⇒ G marries someone better than B (lemma 1) ⇒ (B,G) not a rogue
couple.

Case 2: G did not reject B ⇒ B never serenaded G ⇒ B prefers his mate to G ⇒ (B,G)
not a rogue couple.

So there can be no rogue couples. TMA always gives a unique answer (deterministic)
but there may be other stable matchings.

Let S: set of all stable matchings. S is non-empty. For each person P, we define the
_realm of possibility_ for P to be {given Q, there exists a matching M in S, with
(P,Q) in M}.

*Define* A person's _optimal mate_ is their favourite from the realm of possibility.

*Define* A person's _pessimal mate_ is their least favourite " " ".

**Theorem 4** TMA mates every boy with his optimal mate. (Assume true).

**Theorem 5** TMA mates every girl with her pessimal mate.

*Proof by contradiction*

    Suppose that there exists a stable matching M where some girl G who fares worse
    than in TMA.

    B' ---- M ---- G ---- TMA ---- B ---- M ---- G'

    Girl prefers B to B'.
    (B,G) are a rogue couple in M so M not stable. Contradiction.

TMA is used in many applications. For example matching MDs (girl) to residency 
programs at hospitals (boy). Load balancing - servers are boys, girls are requests.


