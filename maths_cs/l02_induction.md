Lecture 2: Induction
===

Proof by contradiction
---

Prove proposition P is true, assume P is false (ie. !P is true) and
then use that hypothesis to derive a falsehood or contradiction.

If !P ⇒ F is T, P is T

*Example* √(2) is irrational (can't be expressed as ratio of ints)

    Pf by cont. Assume for purpose of contradiction that √(2)
    is rational.
    ⇒ √(2) = a/b (fraction in lowest terms)
            2  = a²/b²
           2b² = a²
    ⇒ a² is even, so a is even (2|a)
    ⇒ 4|a² (if a is a multiple of 2, a² is a multiple of 4)
    ⇒ 4|2b²
    ⇒ 2|b²
    ⇒ b² is even, so b is even
    ⇒ a/b is NOT in lowest terms (both multiple of 2)
    ⇒ CONTRADICTION
    ⇒ √(2) is irrational

Proof by induction
---

*Induction axiom*
Let P(n) be a predicate. If P(0) is true and for all n P(n) ⇒ P(n+1) is
true then for all n P(n) is true.

If P(0), P(0) ⇒ P(1), P(1) ⇒ P(2), … are true
then P(0), P(1), P(2), … are true

*Example* For all n ≥ 0, 1+2+3+…+n = ∑(1,n) i = n(n+1) / 2

    If n = 1, ∑ i = 1
    If n ≤ 0, ∑ i = 0

    Pf by ind. Let P(n) be proposition ∑(1,n) i = n(n+1)/2
    Base case: check P(0) true (…it is)
    Inductive step: for n ≥ 0, show P(n) ⇒ P(n+1) is true

    Assume P(n) is true for purposes of induction.
    ie. assume 1+2+…+n = n(n+1)/2 is true
    need to show 1+2+…+(n+1) = (n+1)(n+2)/2

    1+2+…+(n+1)
    1+2+…+n+(n+1)
    n(n+1)/2 + n + 1 = (n² + n + 2n + 1)/2 = (n+1)(n+2)/2

    P(n) ⇒ P(n+1)

*Example* For all n, 3|(n³-n), eg. n=5, 3|(125-5) … is true

    Pf by ind.
    Let P(n) 3|(n³-n)

    Base case: P(0) n=0, 3|(0-0) … true
    Inductive step: for n ≥ 0, show P(n) ⇒ P(n+1) is true

    Assume P(n), ie. 3|(n³-n)
    Examine P(n+1): (n+1)³ - (n+1) = n³ + 3n² + 3n + 1 - (n+1)
                                   = n³ + 3n² + 2n
                                   = n³ - n + 3n² + 3n
    Since 3|(n³-n), 3|3n², 3|3n ⇒ 3|(n³ - n + 3n² + 3n)
    So P(n)⇒P(n+1)

*Example* For all n, there exists a way to tile a 2^n × 2^n region with a
centre square missing using 2×2 L shaped tiles.

    Pf by ind.
    Base case: P(0): 1×1 so just one square … true
    Inductive step: For n ≥ 0, assume P(n), so need to show P(n+1) true

    Consider a 2^(n+1) × 2^(n+1) courtyard.

    Changing the hypothesis to corner square works.
    Use this to prove centre square hypothesis for n ≥ 2.


