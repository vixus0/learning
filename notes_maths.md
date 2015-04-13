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

*Define*: A pair of letters L1, L2 is an inversion (inverted pair) if
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

    So m'^d ≡ m (mod p) [ p|(m'^d - m) ] }→ p·q|(m'^d - m)
            ≡ m (mod q) [ q|(m'^d - m) ] }

    m'^d ≡ m (mod n)

    So m = rem(m'^d, n) … DONE 


Lecture 6: Graph Theory and Colouring
===

Graphs
---

*Define* A graph G is a pair of sets (V,E) where V is a non-empty
set of items called vertices/nodes and E is a set of 2-item subsets of V, called
edges.

*Example*

    V = {X₁, X₂, …, X₇}
    E = {{X₁,X₂}, {X₁,X₃}, …, {X₅,X₇}}

*Define* Two nodes Xi and Xj are _adjacent_ if {Xi,Xj} is in E.

*Define* An edge e = {Xi,Xj} is _incident_ to Xi and Xj.

*Define* The number of edges incident to a node is called its _degree_.

*Define* A graph is _simple_ if it has no loops or multiple edges. A loop
is an edge that connects a node to itself. Multi-edges connect already-joined
nodes.

*Example*

Use graph theory to determine whether males or females have more opposite-gender
partners.

Claims:

  * U Chicago: on average, men have 74% more o-g partners than women.
  * ABC News: 233%

    Cardinalities (sizes):
    |V| = 300m, |Vm| = 147.6m, |Vw| = 152.4m, |E| = ??

    Am = average # of opposite-gender partners for men
    Aw =        "     "      "      "      "       women

    Am/Aw = 1.74 (U Chicago), 3.33 (ABCN)

    Am = (∑[x in Vm] deg(x)) / |Vm| = |E|/|Vm|
    Aw = (∑[x in Vw] def(x)) / |Vw| = |E|/|Vw|

    Am/Aw = (|E|/|Vm|) / (|E|/|Vw|) = |Vw|/|Vm| ≈ 1.0325
    so the studies are bullshit

Graph-colouring problems
---

Given a graph G and K colors, assign a color to each node so that adjacent nodes
get different colours.

*Define* Minimum # required colours K is the graph's _chromatic number_, $(s).

Easy to check if a colouring is valid but hard to work out the colouring in the
first place. This is an NP-complete problem.

Basic graph-colouring algorithm
---

For a graph G(V,E).

  1. Order the nodes V₁, V₂, …, Vn
  2. Order the colours C₁, C₂, …
  3. For i = 1, 2, …, n
    - Assign the lowest legal colour to Vi
    - But ordering of nodes affects number of colours required
    - Generally better to start with high degree nodes

This is a _greedy_ algorithm. 

**Theorem** If every node in G has degree ≤ d, then the Basic Alg uses at most d+1
colours for G.

*Proof* by induction:

    G has n nodes all with degree ≤ d.

    Base case: n=1 ⇒ 0 edges ⇒ d=0 ⇒ 1 color = d+1 … true
    
    Inductive step: Assume P(n) is true for induction. Let G(V,E) be any (n+1)-node
    graph. Let d be the maximum degree in G.

    Order the nodes V₁, V₂, …, Vn, Vn₊₁.
    Remove Vn₊₁ from G to create G'(V',E') with n nodes.
    Degree of any nodes must stay the same or decrease, so G' has max degree ≤ d.
    P(n) says Basic Alg uses ≤ d+1 colors for V₁, V₂, …, Vn.

    Call Vn₊₁'s neighbours U₁, U₂, …, Ud (since ≤ d neighbours).

    Vn₊₁'s colour must be different from any of its neighbours (d colours).
    So there is one more colour available in the set of d+1 colours that is unused
    by any neighbour that can be assigned to Vn₊₁.

    ⇒ Basic Alg uses ≤ d+1 colors on G ⇒ P(n+1) … QED

*Define* A graph G(V,E) is _bipartite_ if V can be split into Vl, Vr so that
all the edges connect a node in Vl to a node in Vr.

Lots of scheduling problems are actually graph colouring problems.


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


Lecture 8: Graph Theory II - Minimum-Weight Spanning Trees
===

Walks & Paths
---

*Define* A _walk_ is a sequence of nodes joined by edges.

    S             E
    v₀ - v₁ - … - vk  ← length k

*Define* A _path_ is a walk where all nodes are different, ie. no retracing nodes.

*Lemma 1* If there exists a walk from a vertex u to v, then there exists a path from
u to v.

*Proof by contradiction* By the well ordering principle (every non-empty set of integers has a least
element): there exists a walk of minimal length k:

    u = v₀ - v₁ - … - vk = v

If this is not a path then there are two nodes in the sequence that are the same.

    Case k = 0 … true
    Case k = 1 u - v … true
    Case k ≥ 2 suppose walk is not a path and two nodes vi and vj are the same

         u = v₀ - … - vi = vj - … - vk = v

         Construct a shorter walk by condensing any edges between vi/vj (the one node).
         So the walk from u to v can't be the shortest possible, violating the well ordering
         principle. QED

Connectivity
---

*Define* Nodes u and v are _connected_ if there is a path from u to v.

*Define* A graph is _connected_ when every pair of nodes in the graph is connected.

Cycles & Closed Walks
---

*Define* A _closed walk_ is a walk for which the start and end points are the same node.

*Define* If k ≥ 3 and v₀, v₁, …, vk-₁ are all different then we have a _cycle_.

Trees
---

*Define* A connected and acyclic graph is a _tree_. Nodes with degree one are called _leaves_.

*Lemma 2* Any connected subgraph of a tree is also a tree.

*Proof by contradiction* Suppose the connected subgraph isn't a tree and so has a cycle. The whole
graph must also have this cycle. But the whole graph is a tree, which is acyclic. QED.

*Lemma 3* A tree with n nodes must have n-1 edges.

*Proof by induction*

    P(n): There are n-1 edges in any n node tree.
    Base case: P(1), 0 edges … true
    Ind step: Suppose P(n) ⇒ P(n+1)

    Let T be a tree with n+1 nodes.
    Let v be a leaf of T.
    Delete v: this creates a connected subgraph with n nodes. By Lemma 2, this is also a tree.
    By P(n): this sub graph has n-1 edges. Since we removed a leaf, we also removed an edge.
    Putting these back in, we see T has n edges and n+1 nodes.

*Define* A _spanning tree_ (ST) of a connected graph is a subgraph that is a tree and incorporates
all the nodes in the graph.

**Theorem** Every connected graph has a spanning tree.

*Proof by contradiction* Assume we have a connected graph G that has no ST.

    Let T be a connected subgraph of G with the same nodes as G and with the smallest number
    of edges possible.

    T is not a ST, so it must have a cycle. Want to prove that removing an edge from the cycle
    still leaves us with a connected subgraph but breaks the cycle. No nodes would be removed
    so we'd still have all the nodes from G, but we'd have one fewer edges, contradicting our
    initial statement.

    Case 1: --•--- … ---•-- 
              x         y
            Does not contain the removed edge e.
            But since it was a cycle, x and y are still connected.

    Case 2: •---<==…==>---•
            x    cycle    y
            Still connected by if we remove an edge from the cycle.

    So all nodes in G are still connected if we remove an edge from T.
    Removing the edge makes T acyclic, so we have an ST. QED

If the edges in the graph have weights then you have a weighted ST. But how to calculate the
ST with minimum weight?

*Define* The _minimum spanning tree_ MST of an edge-weighted graph G is the ST of G with the
smallest possible sum of edge weights.

**Algorithm** Grow a subgraph one edge at a time, so at each step add the minimum weight edge 
that keeps the subgraph acyclic.

*Lemma 4* Let S consist of the first m edges selected by the algorithm. Then there exists a
MST T(V,E) for G such that S is a subset of E. 

**Theorem** For any connected, weighted graph G the algorithm produces a MST.

*Proof of Theorem* We have n nodes, |V| = n

  1. If chose < n-1 edges, then there exists an edge in E-S that can be added without creating a cycle.
    - since E has n-1 edges
    - since E can't have a cycle

  2. Once m = n-1 edges have been chosen, S = E, producing a MST. (By Lemma 4)

*Proof of Lemma 4*

    By induction.

    P(m): As in lemma.
    Base case: m=0, S (empty set) is subset of E. By previous theorem, every connected
      graph has a MST. … true
    Inductive step: Assume P(m) ⇒ P(m+1)

    Let e be the edge selected in the (m+1)st step.
    Let S denote the first m selected edges.

    By P(m): let T* = (V,E*) be a MST such that S is a subset of E*.

    Case: e in E*, then S+e already subset of E* → P(m+1) … true
    Case: e not in E*
      Algorithm ⇒ S+e has no cycle.
      T* is a tree ⇒ (V,E*+e) has a cycle (proof in notes?)
      ⇒ this cycle has an edge e' that is in E*-S

    Algorithm could have selected e or e' ⇒ weight(e) ≤ weight(e').

    Swap e and e' in T:
      Let T** = (V,E**), E** = E*-e'+e.
      T** is acyclic because removed e' from the only cycle in E*+e.
      T** is connected since e' was on a cycle.
      T** contains every node in G.
      ⇒ T** is a ST of G.

      Know that weight(T**) ≤ weight(T*). By P(m) T* is a MST.
      ⇒ T** is a MST of G.

    ⇒ P(m+1) holds. QEDWTFBBQ
