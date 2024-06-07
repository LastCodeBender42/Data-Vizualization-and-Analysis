# **Overview of Network Analysis Using Python and Networkx**
---

<div style="line-height: 1.8;">This notebook will provide the code for generating an example network containing 13 nodes and 17 edges. This network will be used for the purpose of visulaizing how network centrality values can be used to identify or select for specific features of the network structure. The network as shown below is simple. However, once a network centrality is evaluated the nodes of the network can be resized to create a weighted network where the weight is determined by the given centrality.</div> 

# Network Centrality Metrics

<div style="line-height: 1.8;">Network centrality metrics are crucial for quantifying the topology of biological systems, offering profound insights into the roles and significance of various components within these complex networks. These metrics, such as degree centrality, betweenness centrality, and closeness centrality, help identify key nodes that may represent critical proteins, genes, or metabolites in biological pathways. By evaluating the importance and influence of these nodes, researchers can pinpoint potential targets for therapeutic intervention and understand the underlying mechanisms of disease. Degree centrality highlights nodes with numerous direct connections, indicating their potential influence on network stability and function. Betweenness centrality identifies nodes that act as critical connectors or hubs, facilitating communication and interaction within the network. Closeness centrality measures how efficiently information spreads from a node to all other nodes, reflecting its overall accessibility within the network. By leveraging these centrality metrics, scientists can dissect the intricate architecture of biological systems, leading to more targeted and effective approaches in drug discovery, disease diagnosis, and treatment development.</div>div

## Contents:
- [Network Centrality as a Metric of Topology](#network-centrality-as-a-metric-of-topology)
- [Betweenness Centrality](#betweenness-centrality)
- [Closeness Centrality](#closeness-centrality)
- [Degree Centrality](#degree-centrality)
- [Eigenvector Centrality](#eigenvector-centrality)
- [Comparing Metrics of Network Centrality](#side-by-side-comparison)


# Network Centrality as a Metric of Topology

Before reviewing commonly utilized metrics of network centrality, it is probably best to review more basic concepts.

A graph $G$, or network, is composed of two sets of elements: A set of vertices and a set of edges. A standard formal definition of a graph is given as $G = (V, E)$. The set of vertices, or nodes. for a graph $G$ is denoted by $V(G)$. The set of edges is composed of unordered pairs of vertices and is denoted by $E(G)$. Vertices are commonly indicated using the notation $v_1, v_2, v_3,..., v_N$, where N is the size of the vertex set and we write that $(v_1, v_2, v_3,..., v_N) \subset V(G)$. Edges are given by similar notation. Where two vertices $v_i, v_j \in V(G)$ are connected by an edge, the edge is defined as $e_{ij} = (v_i,v_j) \in E(G)$. Vertices that are connected by an edge in a graph are said to be *adjacent* and the edge connecting two vertices is said to be *incident*. The total number of edges connected to a node $v_i$ is called the *node degree* and is denoted as $\delta(v_i)$. There are three coefficients that are used to describe networks: The number of nodes, the number of edges, and the average node degree, $<\delta>$. Another fundamental concept is that of *shortest paths*. A path represents a sequence of edges that can be traced between two nodes, e.g., $v_i \rightarrow v_j \rightarrow v_k$. A shortest path is a series edges that represents the shortest distance traversed between two nodes. The formal defintion of a shortest path is given by

```math
<font size='4'>P_s(v_i,v_j) = \min_{ij} p_{ij} \in P_{ij}</font>,
```

where $P_s(v_i,v_j)$ is the subset of minimum path length between $v_i$ and $v_j$ of the set of all possible paths $P_{ij}$. Path lengths are often used in the definition of other network metrics. 

Consider a very simple network. This network has 13 nodes that compose the vertex set $(v_1, v_2,...,v_{13}) \subset V(G)$ and 17 edges that make up the edge set $(e_{1,3}=(v_1,v_3), e_{2,3} = (v_2,v_3),...,e_{12,13} = (v_12,v_13)) \subset E(G)$. Simple inspection will show that this network has a structure, or *topology*. Network topology refers to the arrangement or distributiuon of edges among the nodes. Frequently the topology of a network can be quantified by looking at how network properties are distributed. For example, networks where the degree distribution follows a binomial pattern, then the network topology is likely *homogeneous*, i.e., the edges are uniformly distributed. Where the degree distribution follows a power-law, then the network topology is likely *inhomogeneous*, i.e., nonuniformly distributed, which is what we have with this simple network. Using this network as a baseline for comparison, four network centrality properties will be reviewed below and the nodes in the network will be scaled by the network centrality to visualize how that network centrality can be used to evaluate network topology.

```python
import networkx as nx
import matplotlib.pyplot as plt

# Create a new graph
G = nx.Graph()

# Add 13 nodes
nodes = range(1, 14)
G.add_nodes_from(nodes)

# Add some edges to connect the nodes
edges = [
    (1, 3), (2, 3), (3, 4), (4, 5),
    (4, 6), (4, 7), (7, 8), (8, 9),
    (8, 12), (8, 13), (9, 13), (9, 10),
    (10, 13), (10, 11), (11, 12), (11, 13), (12, 13)
]
G.add_edges_from(edges)

# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Draw the graph with fixed positions
plt.figure(figsize=(8, 6))
nx.draw(G, pos, with_labels=True, node_color='orange', node_size=1000, edge_color='grey', font_size=16, edgecolors='black', linewidths=2)
plt.title('Simple Random Network ',fontsize=16)
plt.show()

![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/2993883a-0923-45fe-a6f8-6a6b789b0d3c)

