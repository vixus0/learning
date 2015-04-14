Lecture 8: Graph Theory II
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


