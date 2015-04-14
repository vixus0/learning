Lecture 6: Graph Theory & Colouring
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


