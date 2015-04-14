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


