Lecture 9: Communication Networks
===

Complete Binary Tree
---

                  🞆     🞆 switch          Diameter: 2(logN+1) [6]
                ↙↗ ↖↘   🞐 terminal        Switch size: 3x3
           3x3 🞆     …                    #switches: 2N-1 [7]
             ↙↗ ↖↘
        2x2 🞆     🞆
           ↗ ↘    ↗ ↘      
          🞐   🞐  🞐   🞐   🞐   🞐  🞐   🞐 
          I0  O0 I1  O1  I2  O2 I3  O3 

_Switches_ direct packets through the network. _Terminals_ are the sources and 
destinations of data. We want to route packets efficiently between terminals.

*Define* The _latency_ is the time required for a packet to travel from an input to an
output.

*Define* The _diameter_ of a network is the length of the shortest path between the
input and output that are furthest apart. The furthest terminals need to send data
to each other through the root.

    D = 2(log N + 1) 

For N inputs and N outputs. Note log = log₂ and N is power of 2.

*Define* The _size_ of a switch is UxV where U = #inputs and V = #outputs. In a
binary tree, all the intermediate nodes (half the total nodes) are 3x3 switches.

Increasing the size of intermediate switches will reduce the diameter but this isn't
really feasible in reality.

*Define* The _switch count_ is:

    Since logN is the number of levels in the BT.
    ∑[i=0,logN] 2^i = ∑ 1 + 2 + 4 + … + N = 2N - 1

*Define* A _permutation_ is a function π(i) {0 … N-1} → {0 … N-1} such that no two
numbers are mapped to the same value.

    π(i) = π(j) iff i=j

*Example*

    π(i) = N-1-i
    π(i) = i

**Permutation routing problem for π** 

For each i, direct the packet at In i to Out π(i). The path taken is denoted by
P[i,π(i)].

*Define* The _congestion_ of the paths P[0,π(0)] … P[N-1,π(N-1)] is equal to the
largest number of paths that pass through a single switch.

    π(i) = i ← congestion 1, eg. In 1 → Out 1
    π(i) = N-1-i ← congestion 4, eg. In 1 → Out 2

The _max congestion_ (worst case scenario) = maximum over all possible π (min
congestion P[0,π(0)] … P[N-1,π(N-1)]).

So the maximum congestion for the binary tree is N.

2D Array
---

      I0 🞐 →🞆 →🞆 →🞆 →🞆      Diameter: 2N [8]
            ↓  ↓  ↓  ↓      #switches: N² [16]
      I1 🞐 →🞆 →🞆 →🞆 →🞆      Switch size: 2x2
            ↓  ↓  ↓  ↓
      I2 🞐 →🞆 →🞆 →🞆 →🞆 
            ↓  ↓  ↓  ↓
      I3 🞐 →🞆 →🞆 →🞆 →🞆 
            ↓  ↓  ↓  ↓
            🞐  🞐  🞐  🞐
            O0 O1 O2 O3

**Theorem** The congestion for an N-input array is 2.

*Proof* 

    Let π be any permutation.
    P[i,π(i)] = path from Ii rightward to column π(i) then down to Oπ(i).

    Switch in row i and column π(i) transmits ≤ 2 packets.
    If π(0)=0, then π(N-1)=N-1 ⇒ congestion 2

Butterfly
---

    -- See Butterfly_multitree.svg --

Each switch uniquely identified by column (bitfield) and level (integer). To go from
an input in one col (say 011) to an output in another col (say 101), you cross at
each level IF the bits are different.

    011 → 101, cross at level 0 and 1.

The _diameter_ is then 2+logN.

Switch size is 2x2.

The #switches is N(1+logN).

The _congestion_ is √N or √(N/2) depending on odd or even N, respectively.

Benes
---

    -- See Benesnetwork.png --

Basically two butterfly networks back to back. Has _congestion_ of 1. _Diameter_ is
1+2logN, switch size 2x2 and #switches 2NlogN.
