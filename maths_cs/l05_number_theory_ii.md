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


