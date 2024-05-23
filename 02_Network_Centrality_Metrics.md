# Network Centrality Metics

Network centrality metrics are crucial for quantifying the topology of biological systems, offering profound insights into the roles and significance of various components within these complex networks. These metrics, such as degree centrality, betweenness centrality, and closeness centrality, help identify key nodes that may represent critical proteins, genes, or metabolites in biological pathways. By evaluating the importance and influence of these nodes, researchers can pinpoint potential targets for therapeutic intervention and understand the underlying mechanisms of disease. Degree centrality highlights nodes with numerous direct connections, indicating their potential influence on network stability and function. Betweenness centrality identifies nodes that act as critical connectors or hubs, facilitating communication and interaction within the network. Closeness centrality measures how efficiently information spreads from a node to all other nodes, reflecting its overall accessibility within the network. By leveraging these centrality metrics, scientists can dissect the intricate architecture of biological systems, leading to more targeted and effective approaches in drug discovery, disease diagnosis, and treatment development.

## Contents
- [Network Centrality as a Metric of Topology](#network-centrality-as-a-metric-of-topology)
- [Betweenness Centrality](#betweenness-centrality)
- [Closeness Centrality](#closeness-centrality)

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
C(v_i) = 1/\sum_j^N d(v_iv_j),
```

where $d(v_i, v_j)$ is the distance between $v_i$ and all other vertices $j$ in $G$. This definition of $CC$
implies that the largest possible $CC$ for $v_i$ in $G$ is $C(v_i) = 1/N$ and $C(v_i) → 0$ for vertices at
the graph periphery. Note: A vertex that is close to the center of a graph will have a $CC$ approximately equal to the radius of the graph. Given the definition of $CC$, the question arises as to whether $BC$ and $CC$ are somewhat redundant. It can be the case that nodes that are ‘close’ are also ’between’, but that is not necessarily the case. But, the principle difference between $CC$ and $BC$ are at the end points of the distances measured. $BC$ evaluates the shortest path from $v_h$ through $v_i$ to $v_j$ and $CC$ begins at $v_i$ and evaluates the distanceto every other vertex $v_j$.

## Degree Centrality 

Degree Centrality ($DC$) is simplest of the centrality measures to understand intuitively. $DC$ is just the count of all the nodes adjacent to vi or alternatively a count of the edgesincident on $v_i$. Using the definition of counting incident edges, we have

```math
D(v_i) = \sum_j^N e_{ij}
```

It does not require much imagination to rationalize the logic of degree centrality: Things that are important tend to be well-connected. Whether it’s social groups, interstate traffic, or biological pathways, things that are important exert a lot of influence over the system of interest. So, whereas $BC$ and $CC$ communicate influence, vertices with high $DC$ exert influence. Additionally, the topology of graphs with with scale-free degree distribution cohere through the existence of a small number of highly connected nodes. Targeted removal of these vertices can dramatically effect network connectivity resulting in the decomposition of large components smaller components or even bifurcation of the network.

## Eigenvector Centrality

Eigenvector Centrality ($EC$) builds on the concept of DC. If the vertices that are the most well-connected (highest ranked by degree centrality) exert the most influence on the network, then vertices immediately adjacent to these are likely vertices that are also ”influential”. $EC$ is a concept akin to guilt-by-association. The $EC$ of a vertex $v_i$ is proportional to

```math
E(v_i) = \frac{1}{\lambda} \sum_{j=1}^N A_{ij}v_i
```

which satisfies $Av = \lambda v$. The “significance” of node $v_i$ is defined by the eigenvector of the adjacency matrix A and scaled by the inverse of the associated eigenvalue $\lambda$. The entries of $v$ are $EC$ values. The eigenvalue $\lambda$ is the largest eigenvalue of the adjacency matrix $A$. One of the consequences of this centrality measure is that in scale-free networks $EC$ ’drives’ the centrality value of vertices that are not adjacent to high degree vertices to zero. In other words, $EC$ for a vertex may be high because it has many neighbors or because it is adjacent to an influential neighbor. For this reason, in scale-free networks, $EC$ tends to result in ’clusters’ of many vertices of high $EC$ centered on high-degree vertices with large swaths of vertices in the network characterized $EC$ values near zero.

---

<img width="665" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/6f4a3fbe-b1c8-47e1-af8d-77eadae07199">


---
