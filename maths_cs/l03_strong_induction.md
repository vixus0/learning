Lecture 3: Strong Induction
===

*Example* Rearrange following into alphabetical order using sliding moves:

    ABC       ABC
    DEF  -->  DEF
    HG        GH

It's impossible!

*Theorem*: No sequence of legal moves to invert G/H and return all other
letters to original position.

Use an invariant to prove. To show system can never reach a special
state it's sufficient to show there is some property (the invariant)
that holds in the initial state and across every step but not in the
special state.

Row move:

                          Natural order:
      ABC         ABC       123
      DG    -->   D G       456
      EFH         EFH       789

Lemma 1: A row move does not change the order of items.

Proof: In a row move we move an item from cell i to an adjacent cell
i ± 1. Nothing else moves, so the order of items is preserved.

Column move:

                          Natural order:
      ABC         ABC       123
      DF    -->   DFG       456
      HEG         HE        789

                          Natural order:
      ABC         A C       123
      D G   -->   DBG       456
      HEF         HEF       789

Lemma 2: A column move changes the relative order of precisely 2
pairs of items.

Proof: In a column move we move an item in cell i to a blank space in
cell i ± 3. So it changes relative order with (i±1, i±2).

*Define*: A pair of letters L1, L2 is an _inversion_ (inverted pair) if
L1 precedes L2 in the alphabet but L1 appears after L2 in the puzzle.

      ABC
      FDG
      EH

Inversions: (D,F) (E,F) (E,G)

Lemma 3: During a move, the # of inversions can only increase by 2,
decrease by 2 or stay the same.

Proof: 

  * Row move: doesn't change inversions (by Lemma 1)
  * Column move: 2 pairs change order (by Lemma 2)
    - A. Both pairs were in order ⇒ # inversions + 2
    - B. Both pairs were inverted ⇒ # inversions - 2
    - C. One pair inverted ⇒ # inversions stays same

Corollary 1: During a move, the parity (even/odd) of the # inversions
does not change.

Proof: Adding or subtracting 2 from a number doesn't change its parity.

Lemma 4: In every state reachable from the initial state

    ABC
    DEF
    HG

the parity of the # inversions is odd.

Proof: by induction

    P(n): after any sequence of n moves from the initial state,
    the parity of # inversions is odd.

    Base case: n=0 (no moves), # inversions = 1 ⇒ odd … true

    Inductive step: For any n ≥ 0, show P(n) ⇒ P(n+1)
    
    Consider any sequence of n+1 moves M1, M2, … , Mn+1
    By P(n), we know that parity after M1, … ¸ Mn is odd.
    By Cor1, we know parity does not change after Mn+1
    ⇒ the parity after M1, M2, … , Mn, Mn+1 is odd.
    ⇒ P(n+1)

    So P(n) ⇒ P(n+1)

Proof of *theorem*: The parity of # inversions in desired state is
even (#=0). By Lemma 4, the desired state can not be reached from the
initial state using legal moves because its parity is odd (#=1).

Strong Induction
---

Axiom: Let P(n) be any predicate. If P(0) is true and for all n
P(0)&P(1)&…&P(n) ⇒ P(n+1) is true, then for all n P(n) is true.

Theorem: all strategies for the n-block game produce the same score
S(n).

*Example* S(8) = 28

Proof: by strong induction

    P(n): see theorem

    Base case: n=1 S(1)=0
    
    Inductive step: Assume P(1), P(2), …, P(n) to prove P(n+1)
    Take n+1 blocks:

            n+1
            / \
           k   n+1-k      (for k < n)

    S(n+1) = k(n+1-k) + P(k) + P(n+1-k)

    Stuck - so make the predicate stronger. Get the formula for S(n).
    S(n) = n(n-1)/2

    S(n+1) = k(n+1-k) + k(k-1)/2 + (n+1-k)(n-k)/2
           = ( 2kn + 2k - 2k² + k² - + (n+1)n - kn - k - kn ) / 2
           = n(n+1)/2
             … true



