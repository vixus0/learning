Lecture 10: Graph Theory III
===

*Define* An _Euler tour_ is a walk that traverses every edge exactly once and
starts/finishes at the same node.

**Theorem** A connected graph has an Euler tour iff every node of the graph has
even degree.

*Proof* Assume G(V,E) has an Euler tour:

    v₀ - v₁ - … - vk-1 - vk - v₀

Since every edge in E is traversed once, each node must have an entering edge
and a leaving edge. Even if a node is re-entered, the entering and leaving edges
must be a different pair from the previous ones. Since every edge is traversed
exactly once, there must be an even number of edges. So

    degree(u) = 2 * #times u appears in walk
