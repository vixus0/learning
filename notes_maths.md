Lecture 1: Intro & Proofs
===

Mathematical proofs need:

  - Proposition: a statement that is either T or F.
  - Axioms: a proposition that is "assumed" true.
  
p => q (implies) if p is F or q is T.
p <=> q (if and only if) requires an implication in both directions

    p | q | p => q | q => p | p <=> q
    --|---|--------|--------|---------
    T | T | T      | T      | T
    T | F | F      | T      | F
    F | T | T      | F      | F
    F | F | T      | T      | T
