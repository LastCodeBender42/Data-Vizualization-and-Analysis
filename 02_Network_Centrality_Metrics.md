# Network Centrality Metics

## Network Centrality as a Metric of Topology

## Betweenness Centrality

Betweenness Centrality ($BC$) is a measure that utilizes the definition of shortest path to assign significance to vertices. In descriptive terms, the $BC$ of a vertex $v_i$ is the ratio of the number of shortest paths incident on vi to the total number of shortest path lengths in the network. Therefore, the $BC$ evaluated for any vertex $v_i$ is equal to the proportion

```math
B(v_i) = \frac{\sum s_i}{S(G)}
```

where $s_i$ denotes the set of shortest paths that include vi and $S(G)$ denotes the complete set
of shortest paths for a random graph $G$. Vertices with the large BC are understood to be
important for maintaining the global connectivity of the graph. Vertices with larger $BC$ also
decrease the overall average path length and diameter of the graph. $BC$ also contributes to
the rate of diffusion on graphs. Vertices with large $BC$ increase the rate of diffusion across
the graph due to reduced average path lengths.

## Closeness Centrality

Closeness Centrality ($CC$) is a measure that identifies vertices that have the shortest
paths to all other nodes. In other words, these are the vertices that are at the geodesic
“center” of the graph. $CC$ is defined as

```math
C(v_i) = 1/\sum_j^N d(v_i,v_j),
```

where $d(v_i, v_j)$ is the distance between $v_i$ and all other vertices $j$ in $G$. This definition of $CC$
implies that the largest possible $CC$ for $v_i$ in $G$ is $C(v_i) = 1/N$ and $C(v_i) → 0$ for vertices at
the graph periphery. Note: A vertex that is close to the center of a graph will have a $CC$ approximately equal to the radius of the graph. Given the definition of $CC$, the question arises as to whether $BC$ and $CC$ are somewhat redundant. It can be the case that nodes that are ‘close’ are also ’between’, but that is not necessarily the case. But, the principle difference between $CC$ and $BC$ are at the end points of the distances measured. $BC$ evaluates the shortest path from $v_h$ through $v_i$ to $v_j$ and $CC$ begins at $v_i$ and evaluates the distanceto every other vertex $v_j$.
