**MIT 6.042J: Maths for CS**

Lecture 1: Intro & Proofs
===

Mathematical proofs need:

  - Proposition: a statement that is either T or F.
  - Axioms: a proposition that is "assumed" true.
  - Logical deductions
  
p => q (implies) if p is F or q is T.
p <=> q (if and only if) requires an implication in both directions

    p | q | p => q | q => p | p <=> q
    --|---|--------|--------|---------
    T | T | T      | T      | T
    T | F | F      | T      | F
    F | T | T      | F      | F
    F | F | T      | T      | T


Lecture 2: Induction
===

Proof by contradiction
---

Prove proposition P is true, assume P is false (ie. !P is true) and
then use that hypothesis to derive a falsehood or contradiction.

If !P => F is T, P is T

Ex: sqrt(2) is irrational (can't be expressed as ratio of ints)

    Pf by cont. Assume for purpose of contradiction that sqrt(2)
    is rational.
    => sqrt(2) = a/b (fraction in lowest terms)
            2  = a²/b²
           2b² = a²
    => a² is even, so a is even (2|a)
    => 4|a² (if a is a multiple of 2, a² is a multiple of 4)
    => 4|2b²
    => 2|b²
    => b² is even, so b is even
    => a/b is NOT in lowest terms (both multiple of 2)
    => CONTRADICTION
    => sqrt(2) is irrational

Proof by induction
---

*Induction axiom*
Let P(n) be a predicate. If P(0) is true and for all n P(n) => P(n+1) is
true then for all n P(n) is true.

If P(0), P(0) => P(1), P(1) => P(2), … are true
then P(0), P(1), P(2), … are true

Ex: For all n ≥ 0, 1+2+3+…+n = ∑(1,n) i = n(n+1) / 2

    If n = 1, ∑ i = 1
    If n ≤ 0, ∑ i = 0

    Pf by ind. Let P(n) be proposition ∑(1,n) i = n(n+1)/2
    Base case: check P(0) true (…it is)
    Inductive step: for n ≥ 0, show P(n) => P(n+1) is true

    Assume P(n) is true for purposes of induction.
    ie. assume 1+2+…+n = n(n+1)/2 is true
    need to show 1+2+…+(n+1) = (n+1)(n+2)/2

    1+2+…+(n+1)
    1+2+…+n+(n+1)
    n(n+1)/2 + n + 1 = (n² + n + 2n + 1)/2 = (n+1)(n+2)/2

    P(n) => P(n+1)

Ex: For all n, 3|(n³-n), eg. n=5, 3|(125-5) … is true

    Pf by ind.
    Let P(n) 3|(n³-n)

    Base case: P(0) n=0, 3|(0-0) … true
    Inductive step: for n ≥ 0, show P(n) => P(n+1) is true

    Assume P(n), ie. 3|(n³-n)
    Examine P(n+1): (n+1)³ - (n+1) = n³ + 3n² + 3n + 1 - (n+1)
                                   = n³ + 3n² + 2n
                                   = n³ - n + 3n² + 3n
    Since 3|(n³-n), 3|3n², 3|3n => 3|(n³ - n + 3n² + 3n)
    So P(n)=>P(n+1)

Ex: For all n, there exists a way to tile a 2^n × 2^n region with a
centre square missing using 2×2 L shaped tiles.

    Pf by ind.
    Base case: P(0): 1×1 so just one square … true
    Inductive step: For n ≥ 0, assume P(n), so need to show P(n+1) true

    Consider a 2^(n+1) × 2^(n+1) courtyard.

    Changing the hypothesis to corner square works.
    Use this to prove centre square hypothesis for n ≥ 2.


Lec 3: Strong Induction
===

Ex: Rearrange following into alphabetical order using sliding moves:

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

Define: A pair of letters L1, L2 is an inversion (inverted pair) if
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
    - A. Both pairs were in order => # inversions + 2
    - B. Both pairs were inverted => # inversions - 2
    - C. One pair inverted => # inversions stays same

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

    Base case: n=0 (no moves), # inversions = 1 => odd … true

    Inductive step: For any n ≥ 0, show P(n) => P(n+1)
    
    Consider any sequence of n+1 moves M1, M2, … , Mn+1
    By P(n), we know that parity after M1, … ¸ Mn is odd.
    By Cor1, we know parity does not change after Mn+1
    => the parity after M1, M2, … , Mn, Mn+1 is odd.
    => P(n+1)

    So P(n) => P(n+1)

Proof of *theorem*: The parity of # inversions in desired state is
even (#=0). By Lemma 4, the desired state can not be reached from the
initial state using legal moves because its parity is odd (#=1).

Strong Induction
---

Axiom: Let P(n) be any predicate. If P(0) is true and for all n
P(0)&P(1)&…&P(n) => P(n+1) is true, then for all n P(n) is true.

Theorem: all strategies for the n-block game produce the same score
S(n).

Ex: S(8) = 28

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
