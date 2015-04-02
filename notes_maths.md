**MIT 6.042J: Maths for CS**

Lecture 1: Intro & Proofs
===

Mathematical proofs need:

  - Proposition: a statement that is either T or F.
  - Axioms: a proposition that is "assumed" true.
  - Logical deductions
  
p ⇒ q (implies) if p is F or q is T.
p <⇒ q (if and only if) requires an implication in both directions

    p | q | p ⇒ q | q ⇒ p | p <⇒ q
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


Lec 3: Strong Induction
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



Lecture 4: Number Theory I
===

Study of the integers.

Define: m|a (m divides a) iff there exists an integer k such that
a = km

Suppose a-gallon jug and b-gallon jug. (a=3, b=5), a ≤ b

Theorem: m|a & m|b, then m|(any result of pouring/filling jugs)

*State machine*

  * States: pairs (x,y) where x = amt in a-jug, y = amt in b-jug
  * Start-state: (0,0)
  * Transitions:
    - emptying: (x,y) → (0,y) or (x,y) → (x,0)
    - filling: (x,y) → (a,y) or (x,y) → (x,b)
    - pouring: …
 
    (x,y) → (0,x+y)      if x+y < b
    (x,y) → (x-(b-y), b) if x+y ≥ b
    (x,y) → (x+y, 0)     if x+y < a
    (x,y) → (a, y-(a-x)) if x+y ≥ a

    a=3, b=5 (0,0) → (3,0) → (0,3) → (3,3) → (1,5) → (1,0) → (0,1) → (3,1) → (0,4)
          or (0,0) → (0,5) → (3,2) → (0,2) → (2,0) → (2,5) → (3,4)

Proof by induction:

    Assume m|a, m|b
    Invariant: P(n) = "If (x,y) is the state after n transitions, 
    then m|x, m|y"

    Base case: (0,0), m|0 ⇒ P(0) … true

    Inductive step: Assume P(n)
    
    Suppose that (x,y) is the state after n transitions, then by P(n) 
    m|x and m|y.

    After another transition, each of the jugs are filled with
    0, a, b, x, y, x+y, x+y-a, x+y-b

    We know m|0, m|a, m|b and by P(n) m|x, m|y
    So m|(any linear combination of x,y,a,b,0)

    Done. 

Define: gcd(a,b) = greatest common denominator of a and b, eg. gcd(52,44) = 4

Theorem: Any linear combination, L = sa + tb with 0 ≤ L ≤ b can be reached

    4 = (-2)·3 + 2·5
           5·3 - 3·5   (ba - ab)
           ---------
           3·3 - 1·5 … is a multiple of 4
           s'    t'

Proof: 

    Notice L = sa+tb = (s+mb)a + (t-ma)b
                         s'        t'

Basically rewrite the linear relation so that we have a positive
coefficient s'. Even if s < 0, m can be large enough to make s' positive.
So there exists some s', t' such that L = s'a + t'b with s' > 0

Assume 0 < L < b

*Algorithm* To obtain L gallons, repeat s' times the following:

    - Fill the a-jug
    - Pour into b-jug
    - When full, empty b-jug
    - Repeat until a-jug empty

With a=3, b=5, s'=3:

    1st loop: (0,0) - (3,0) - (0,3)
    2nd loop: (0,3) - (3,3) - (1,5) - (1,0) - (0,1)
    3rd loop: (0,1) - (3,1) - (0,4)

Filled the a-jug s' times.
Suppose b-jug is emptied u times.
Let r be the remainder in the b-jug

    r = s'a - ub    L = s'a + t'b

Need to show r = L

    r = s'a + (t'b - t'b) - ub = L - (t'+u)b

But 0 ≤ r ≤ b and 0 < L < b, so 

    (t'+u) ≠ 0 ⇒ [r<0 or r>b]
    (t'+u) = 0 ⇒ u=-t' ⇒ r = L … true

Euclid's algorithm (the pulveriser)
---

Algorithm for finding gcd of two numbers.
There exists a unique quotient q and remainder r such that

    b = qa + r

with the property that 0 ≤ r < a. r = rem(b,a)

*Lemma* gcd(a, b) = gcd(rem(b,a), a)

*Example* 

    gcd(105, 224) = gcd(rem(224,105), 105)
                  since 224 = 2·105 + 14
                  = gcd(14, 105) 
                  = gcd(rem(105, 14), 14)
                  since 105 = 7·14 + 7
                  = gcd(7, 14)
                  = gcd(rem(14, 7), 7)
                  = gcd(0, 7)
                  = 7

Proof of *lemma*:

    Want to show if gcd can divide a and b, then it can also divide the
    rem(b,a).

    [m|a & m|b] ⇒ [m|b-qa = rem(b,a) & m|a]

    if rem(b,a) ≠ 0 then [m|b-qa & m|a] ⇒ [m|a & m|b]
    because if m divides b-qa and m divides a then it also divides any
    linear combination of those, such as (b-qa) + qa = b. So m also
    divides b.

    if rem(b,a) = 0 then b-qa = 0 ⇒ b = qa
    so m|a ⇒ m|b

*Theorem* gcd(a,b) is a linear combination of a and b.

Proof by induction:

    Invariant: 
    P(n) = "If Euclid's alg reaches a gcd(x,y) after n steps then both x
    and y are linear combinations of a and b. gcd(a,b) = gcd(x,y)

    Base case: n=0 gcd(a,b) = gcd(a,b) so P(0) true
    
    Inductive step: Assume P(n), prove P(n+1)
    Notice there exists a q such that rem(y,x) = y-qx → lin comb of a, b
    since y and x are both linear combinations of a and b.
    ⇒ P(n+1) … true

In the last step of the algorithm, gcd(0,y) = y

*Theorem* gcd(a,b) is the smallest positive lin comb of a and b.


Lecture 5: Number Theory II
===

Encryption
---

Beforehand: keys are exchanged between a receiver and a sender. To avoid
message being read by an interceptor, need to encrypt it.

* Encryption: m' = E(keys, m)
* Decryption: m = D(keys, m')

The MITM shouldn't be able to get any knowledge of m without some knowledge
of keys.

Turing's code V1
---

          "victory" v=22, i=09, etc.
    m = 2209032015182513 ← 13 appended to make m a prime

Beforehand: exchange a secret prime k.

* E: m' = mk
* D: m = m'/k

Hard to factor a product of two large primes, so seemingly good encryption.

But what if two messages are intercepted?

    m₁' = m₁k
    m₂' = m₂k

So find gcd(m₁', m₂') to get k. D-D-D-DECRYPTED.

Turing's code V2
---


Beforehand: exchange *secret* prime k and a *public* prime p.

Encryption: 

  * Message represented as a number m in range {0, 1, …, p-1}.
  * compute m' = rem(mk, p)

Decryption: ?

*Define* a,b are relatively prime iff gcd(a,b) = 1 iff there exist integers
s and t such that:

    sa + tb = 1

*Define* x is congruent to y modulo n: x ≡ y (mod n) iff n|(x-y)

*Example* 31 = 16 (mod 5), 5|31-16 ⇒ 5|15

*Define* The multiplicative inverse of x mod n is a number x¯¹ in the range
{0, 1, …, n-1} such that x·x¯¹ ≡ 1 (mod n)

*Example* 

    2·3 = 1 (mod 5), 5|6-1
    2 ≡ 3¯¹ (mod 5)
    3 ≡ 2¯¹ (mod 5)

    5·5 = 1 (mod 6), 6|25-1
    5 ≡ 5¯¹ (mod 6)

Back to the decryption: rem(mk, p) ≡ mk (mod p) ⇒ p|(rem(mk,p) - mk)

If k·k¯¹ ≡ 1 (mod p), then m'k¯¹ ≡ mk·k¯¹ ≡ m (mod p)

So m = rem(m'k¯¹, p)

Known-plaintext attack
---

Assume known message m and encryption m' = rem(mk, p)

    m' ≡ mk (mod p)

    Since p is a prime, gcd(m,p) = 1
    Since m and p are relatively prime, there is a linear combination of
    them that = 1.

    Compute m¯¹ such that m·m¯¹ ≡ 1 (mod p)

    Compute m'm¯¹ ≡ k·m·m¯¹ ≡ k (mod p)

    Compute k¯¹ (mod p)

    D-D-D-Decrypted

Euler's theorem
---

**Theorem** If the gcd(n,k) = 1 then k^ϕ(n) ≡ 1 (mod n)

*Define* (Euler's Totient Function) ϕ(n) denotes the number of integers in
{1, 2, 3, …, n-1} that are relatively prime to n.

*Example*

    n = 12: 1 2 3 4 5 6 7 8 9 10 11 12
            *       *   *        *
    ϕ(12) = 4

    n = 15: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
            * *   *     * *      *     *  *
    ϕ(15) = 8

*Define* gcd(n,k) = 1 iff k has a multiplicative inverse

*Proof*

    gcd(n,k) = 1 iff there exists a lin comb ns + kt = 1, n|(kt-1)
    so kt ≡ 1 (mod n) ⇒  k·k¯¹ ≡ 1 (mod n)

*Lemma* if gcd(n,k) = 1, then

    ak ≡ bk (mod n) ⇒ a ≡ b (mod n)

*Lemma* Suppose gcd(n,k) = 1. 

    Let k₁, …, k_r in {1, 2, …, n-1} denote the integers relatively prime 
    to n (r = ϕ(n)).

    Then, {rem(k₁·k, n), …, rem(k_r·k, n)} = {k₁, …, k_r}
                      ① # = r            ② equal     

*Proof ① :*

    rem(k_i·k, n) = rem(k_j·k, n)
    difference between the two is a multiple of n
    ⇒ k_i k ≡ k_j k (mod n)
    since ak ≡ bk (mod n) ⇒ a ≡ b (mod n)
    ⇒ k_i ≡ k_j (mod n)
    since n|(k_i - k_j) ???
    ⇒ k_i = k_j

*Proof ② :*

    gcd(n, rem(k_i k, n)) = gcd (n, k_i k) = 1
    because gcd(n,k) = 1 and gcd(n, k_i) = 1

    So the subset of all the remainders is equal to the subset of all k.

*Proof Euler's Theorem:*

    k₁ · k₂ · … · k_r = rem(k₁k, n) · … · rem(k_r k, n)
                      ≡ k₁·k · k₂·k · … · k_r k (mod n)
                      ≡ k₁·k₂·…·k_r·k^r (mod n)

    cancel on both sides
                    1 ≡ k^r (mod n) and remember r = ϕ(n)

Fermat's little theorem
---

**Theorem** Suppose p is a prime and k in range {1, 2, …, p-1} then
k^(p-1) ≡ 1 (mod p)

*Proof*

    1, 2, …, p-1 are relatively prime to p.

    k^ϕ(p) ≡ 1 (mod p)
    k^(p-1) ≡ 1 (mod p)
    k·k^(p-2) = k^(p-1) ≡ 1 (mod p)
    k¯¹ ≡ k^(p-2) (mod p)

RSA
---

Beforehand: Receiver creates a public key and a secret key.

  1. Generate two distinct primes p and q
  2. Let n = pq
  3. Select e such that gcd(e, (p-1)(q-)) = 1 ⇒ *public key* is pair (e,n)
  4. Compute d such that d·e ≡ 1 (mod (p-1)(q-1)) ⇒ *secret key* is pair (d,n)

Encryption: m' = rem(m^e, n)

Decryption: m = rem(m'^d, n)

*Proof*

    m' = rem(m^e, n) ≡ m^e (mod n) ⇒ (m')^d ≡ m^(ed) (mod n)

    ed = 1 + r(p-1)(q-1)

    So, m'^d ≡ m^(ed) ≡ m·m^(r(p-1)(q-1)) (mod n) ①

    If m ≠ 0 (mod p) then m^(p-1) ≡ 1 (mod p) by Fermat's little theorem
    If m ≠ 0 (mod q) then m^(q-1) ≡ 1 (mod q)

    since n = pq

    m'^d ≡ m·m^(r(p-1)(q-1)) (mod p) ①
           m·m^(r(p-1)(q-1)) (mod q)

    So m'^d ≡ m (mod p) [ p|(m'^d - m) ] - p·q|(m'^d - m)
            ≡ m (mod q) [ q|(m'^d - m) ] /

    m'^d ≡ m (mod n)

    So m = rem(m'^d, n) … DONE 
