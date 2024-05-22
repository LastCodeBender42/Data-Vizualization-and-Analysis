# Network Centrality Metics

## 01 Network Centrality as a Metric of Topology

Betweenness Centrality (BC) is a measure that utilizes the definition of shortest path
to assign significance to vertices. In descriptive terms, the BC of a vertex vi
is the ratio of
the number of shortest paths incident on vi to the total number of shortest path lengths in
the network. Therefore, the BC evaluated for any vertex vi
is equal to the proportion
B(vi) =
Psi
S(G)
, (2.8)
10
where si denotes the set of shortest paths that include vi and S(G) denotes the complete set
of shortest paths for a random graph G. Vertices with the large BC are understood to be
important for maintaining the global connectivity of the graph. Vertices with larger BC also
decrease the overall average path length and diameter of the graph. BC also contributes to
the rate of diffusion on graphs. Vertices with large BC increase the rate of diffusion across
the graph due to reduced average path lengths.
