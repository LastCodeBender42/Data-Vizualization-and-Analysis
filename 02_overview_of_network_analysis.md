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


## $$P_s(v_i,v_j) = \min_{ij} p_{ij} \in P_{ij}</font>,$$


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
```

![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/2993883a-0923-45fe-a6f8-6a6b789b0d3c)

# Betweenness Centrality:
---

Betweenness Centrality ($BC$) utilizes concept of shortest path to assign significance to vertices. In descriptive terms, the $BC$ of a vertex $v_i$ is the ratio of the number of shortest paths incident on vi to the total number of shortest path lengths in the network. Therefore, the $BC$ evaluated for any vertex $v_i$ is equal to the proportion

## $$B(v_i) = \frac{\sum s_i}{S(G)}$$

where $s_i$ denotes the set of shortest paths that include vi and $S(G)$ denotes the complete set of shortest paths for a random graph $G$. Vertices with the large BC are understood to be important for maintaining the global connectivity of the graph. Vertices with larger $BC$ also decrease the overall average path length and diameter of the graph. $BC$ also contributes to the rate of diffusion on graphs. Vertices with large $BC$ increase the rate of diffusion across the graph due to smaller average path lengths.

Betweenness centrality is a crucial metric in network analysis that measures the extent to which a node lies on the shortest paths between other nodes. This centrality highlights nodes that act as bridges or critical intermediaries within the network. Nodes with high betweenness centrality are influential because they control the flow of information or resources across the network, making them key players in maintaining network connectivity and coherence. In social networks, individuals with high betweenness centrality often serve as gatekeepers or brokers, facilitating communication and interactions between different groups or communities. In transportation or logistical networks, nodes with high betweenness centrality can represent major hubs or transfer points essential for efficient flow. By identifying nodes with high betweenness centrality, analysts can pinpoint strategic points for monitoring, control, or reinforcement, making it a valuable tool for optimizing network performance, enhancing robustness, and mitigating vulnerabilities.

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Compute betweenness centrality
betweenness_centrality = nx.betweenness_centrality(G)

# Normalize node sizes based on betweenness centrality
min_size = 400
max_size = 4000
betweenness_weight = [min_size + (max_size - min_size) * betweenness_centrality[node] for node in G.nodes()]

# Normalize sizes for color mapping
normalized_sizes = [float(i - min(sizes)) / (max(sizes) - min(sizes)) for i in sizes]

# Get a color map
cmap = plt.get_cmap('bwr')
colors = [cmap(norm_size) for norm_size in normalized_sizes]

# Draw the graph with fixed positions and colored nodes
plt.figure(figsize=(8, 6))
nx.draw(G, pos, with_labels=True, node_color='orange', node_size=betweenness_weight, edge_color='grey', font_size=16, edgecolors='black', linewidths=2)
plt.title('Network with Node Sizes and Colors Based on Betweenness Centrality',fontsize=16)
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/6ddd3a0f-4802-473f-90ee-402f739019a3)

## Comparing the simple unweighted network to a network weighted by betweenness centrality.
---

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Create subplots
fig, axs = plt.subplots(1, 2, figsize=(12, 8))

# Plot simple random network
nx.draw(G, pos, ax=axs[0], node_color='orange', node_size=1000, with_labels=True,edgecolors='black', linewidths=2)
axs[0].set_title('Unscaled Node Size', fontsize=16)

# Plot betweenness centrality
nx.draw(G, pos, ax=axs[1], node_color='orange', node_size=betweenness_weight, with_labels=True, edgecolors='black', linewidths=2)
axs[1].set_title('Betweenness Centrality', fontsize=16)

plt.tight_layout()
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/bf90e37b-9aa9-4644-a141-95b5ed15d160)

# Closeness Centrality:
---
Closeness Centrality ($CC$) is a measure that identifies vertices that have the shortest
paths to all other nodes. In other words, these are the vertices that are at the geodesic
“center” of the graph. $CC$ is defined as

## $$C(v_i) = 1/\sum_j^N d(v_iv_j),$$


where $d(v_i, v_j)$ is the distance between $v_i$ and all other vertices $j$ in $G$. This definition of $CC$
implies that the largest possible $CC$ for $v_i$ in $G$ is $C(v_i) = 1/N$ and $C(v_i) → 0$ for vertices at
the graph periphery. Note: A vertex that is close to the center of a graph will have a $CC$ approximately equal to the radius of the graph. Given the definition of $CC$, the question arises as to whether $BC$ and $CC$ are somewhat redundant. It can be the case that nodes that are ‘close’ are also ’between’, but that is not necessarily the case. But, the principle difference between $CC$ and $BC$ are at the end points of the distances measured. $BC$ evaluates the shortest path from $v_h$ through $v_i$ to $v_j$ and $CC$ begins at $v_i$ and evaluates the distanceto every other vertex $v_j$.

Closeness centrality is a crucial metric in network analysis that measures the average shortest path length from a given node to all other nodes in the network. This metric is significant because it provides insight into how quickly information or resources can be disseminated from one node to the entire network. Nodes with high closeness centrality are typically more central and have better access to the rest of the network, making them critical for efficient communication and information spread. In social networks, these nodes often represent influential individuals who can reach others more quickly. In infrastructure networks, such nodes are key to ensuring rapid distribution and connectivity. By identifying nodes with high closeness centrality, network analysts can pinpoint strategic positions for optimizing the flow of information, enhancing robustness, and improving overall network efficiency.

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Compute closeness centrality
closeness_centrality = nx.closeness_centrality(G)

# Normalize node sizes based on closeness centrality
min_size = 400
max_size = 4000
closeness_weight = [min_size + (max_size - min_size) * closeness_centrality[node] for node in G.nodes()]


# Get a color map
# cmap = plt.get_cmap('bwr')
# colors = [cmap(norm_size) for norm_size in sizes]

# Draw the graph with fixed positions
plt.figure(figsize=(8, 6))
nx.draw(G, pos, with_labels=True, node_color='orange', node_size=closeness_weight, edge_color='grey', font_size=16, edgecolors='black', linewidths=2)
plt.title('Network with Node Sizes Weighted by Closeness Centrality',fontsize=16)
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/24c437e6-f326-4725-aa4f-db806f95948c)

## Comparing the simple unweighted network to a network weighted by closeness centrality.
---

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Calculate centralities
closeness_centrality = nx.closeness_centrality(G)

# Create subplots
fig, axs = plt.subplots(1, 2, figsize=(12, 8))

# Plot simple random network
nx.draw(G, pos, ax=axs[0], node_color='orange', node_size=1000, with_labels=True,edgecolors='black', linewidths=2)
axs[0].set_title('Unscaled Node Size', fontsize=16)

# Plot closeness centrality
nx.draw(G, pos, ax=axs[1], node_color='orange', node_size=closeness_weight, with_labels=True, edgecolors='black', linewidths=2)
axs[1].set_title('Closeness Centrality', fontsize=16)

plt.tight_layout()
plt.show()
```

![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/44fd8ddc-73d2-4451-9ea3-6671680b70d3)

# Degree Centrality:
---

Degree Centrality ($DC$) is simplest of the centrality measures to understand intuitively. $DC$ is just the count of all the nodes adjacent to vi or alternatively a count of the edgesincident on $v_i$. Using the definition of counting incident edges, we have

## $$D(v_i) = \sum_j^N e_{ij}$$


It does not require much imagination to rationalize the logic of degree centrality: Things that are important tend to be well-connected. Whether it’s social groups, interstate traffic, or biological pathways, things that are important exert a lot of influence over the system of interest. So, whereas $BC$ and $CC$ communicate influence, vertices with high $DC$ exert influence. Additionally, the topology of graphs with with scale-free degree distribution cohere through the existence of a small number of highly connected nodes. Targeted removal of these vertices can dramatically effect network connectivity resulting in the decomposition of large components smaller components or even bifurcation of the network.


Degree centrality is a fundamental metric in network analysis that measures the number of direct connections a node has to other nodes in the network. This metric is significant because it highlights the most connected or influential nodes within the network, often referred to as hubs. Nodes with high degree centrality have extensive ties and are crucial for maintaining the network's structural integrity and facilitating communication. In social networks, these nodes represent individuals with many social ties, playing pivotal roles in spreading information and influence. In biological networks, such as protein interaction networks, nodes with high degree centrality often correspond to essential proteins involved in multiple biological processes. By identifying nodes with high degree centrality, analysts can understand key points of connectivity and influence, which can be vital for network optimization, targeted interventions, and understanding the network's resilience to disruptions.

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Compute degree centrality
degree_centrality = nx.degree_centrality(G)

# Normalize node sizes based on degree centrality
min_size = 40
max_size = 8000
degree_weight = [min_size + (max_size - min_size) * degree_centrality[node] for node in G.nodes()]

# Normalize sizes for color mapping
normalized_sizes = [float(i - min(sizes)) / (max(sizes) - min(sizes)) for i in sizes]

# Get a color map
# cmap = plt.get_cmap('bwr')
# colors = [cmap(norm_size) for norm_size in normalized_sizes]

# Draw the graph with fixed positions and colored nodes
plt.figure(figsize=(8, 6))
nx.draw(G, pos, with_labels=True, node_color='orange', node_size=degree_weight, edge_color='grey', font_size=16, edgecolors='black', linewidths=2)
plt.title('Network with Node Sizes and Colors Based on Degree Centrality',fontsize=16)
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/acaad9e7-65d9-4ea6-8bf2-80ebf83dd4a8)

## Comparing the simple unweighted network to a network weighted by degree centrality.
---

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Create subplots
fig, axs = plt.subplots(1, 2, figsize=(12, 8))

# Plot simple random network
nx.draw(G, pos, ax=axs[0], node_color='orange', node_size=1000, with_labels=True,edgecolors='black', linewidths=2)
axs[0].set_title('Unscaled Node Size', fontsize=16)

# Plot degree centrality
nx.draw(G, pos, ax=axs[1], node_color='orange', node_size=degree_weight, with_labels=True, edgecolors='black', linewidths=2)
axs[1].set_title('Degree Centrality', fontsize=16)

plt.tight_layout()
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/6ce76fe5-3dc0-433f-b57d-b7ac5efd8a0f)

# Eigenvector Centrality:
---
Eigenvector Centrality ($EC$) builds on the concept of DC. If the vertices that are the most well-connected (highest ranked by degree centrality) exert the most influence on the network, then vertices immediately adjacent to these are likely vertices that are also ”influential”. $EC$ is a concept akin to guilt-by-association. The $EC$ of a vertex $v_i$ is proportional to

## $$E(v_i) = \frac{1}{\lambda} \sum_{j=1}^N A_{ij}v_i$$

which satisfies $Av = \lambda v$. The “significance” of node $v_i$ is defined by the eigenvector of the adjacency matrix A and scaled by the inverse of the associated eigenvalue $\lambda$. The entries of $v$ are $EC$ values. The eigenvalue $\lambda$ is the largest eigenvalue of the adjacency matrix $A$. One of the consequences of this centrality measure is that in scale-free networks $EC$ ’drives’ the centrality value of vertices that are not adjacent to high degree vertices to zero. In other words, $EC$ for a vertex may be high because it has many neighbors or because it is adjacent to an influential neighbor. For this reason, in scale-free networks, $EC$ tends to result in ’clusters’ of many vertices of high $EC$ centered on high-degree vertices with large swaths of vertices in the network characterized $EC$ values near zero.

Eigenvector centrality is a significant measure in network analysis that assesses a node's influence based not only on its direct connections but also on the importance of its neighbors. This centrality considers the principle that connections to highly connected nodes contribute more to a node's centrality than connections to less connected nodes. Consequently, eigenvector centrality identifies nodes that are central to the most influential sub-networks, making it particularly useful in identifying key players in social networks, hubs in transportation networks, and influential nodes in biological networks. It captures the recursive nature of influence, where a node's importance is derived from the importance of the nodes it is connected to. This makes eigenvector centrality an invaluable tool for uncovering the underlying power structures and key influencers within a network, enabling more effective strategies for information dissemination, targeted interventions, and understanding the dynamics of complex systems.

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Compute eigenvector centrality
eigenvector_centrality = nx.eigenvector_centrality(G)

# Normalize node sizes based on eigenvector centrality
min_size = 400
max_size = 8000
eigenvector_weight = [min_size + (max_size - min_size) * eigenvector_centrality[node] for node in G.nodes()]

# Normalize sizes for color mapping
normalized_sizes = [float(i - min(sizes)) / (max(sizes) - min(sizes)) for i in sizes]

# Get a color map
cmap = plt.get_cmap('bwr')
colors = [cmap(norm_size) for norm_size in normalized_sizes]

# Draw the graph with fixed positions and colored nodes
plt.figure(figsize=(8, 6))
nx.draw(G, pos, with_labels=True, node_color='orange', node_size=eigenvector_weight, edge_color='grey', font_size=16, edgecolors='black', linewidths=2)
plt.title('Network with Node Sizes and Colors Based on Eigenvector Centrality',fontsize=16)
plt.show()
```
![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/5416dea7-89c2-4ce6-89a5-073914386f20)

## Comparing the simple unweighted network to a network weighted by eigenvector centrality.
---

```python
# Compute the fixed positions for the nodes
pos = nx.spring_layout(G, seed=42)  # Use a fixed seed for reproducibility

# Create subplots
fig, axs = plt.subplots(1, 2, figsize=(12, 8))

# Plot betweenness centrality
nx.draw(G, pos, ax=axs[0], node_color='orange', node_size=1000, with_labels=True,edgecolors='black', linewidths=2)
axs[0].set_title('Unscaled Node Size', fontsize=16)

# Plot closeness centrality
nx.draw(G, pos, ax=axs[1], node_color='orange', node_size=eigenvector_weight, with_labels=True, edgecolors='black', linewidths=2)
axs[1].set_title('Eigenvector Centrality', fontsize=16)

plt.tight_layout()
plt.show()
```

![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/8a5a58b7-19fc-4d88-ac78-45289c244ba1)

# Side-by-side Comparison of Four Centrality Metrics:
---

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

# Calculate centralities
betweenness_centrality = nx.betweenness_centrality(G)
closeness_centrality = nx.closeness_centrality(G)
degree_centrality = nx.degree_centrality(G)
eigenvector_centrality = nx.eigenvector_centrality(G)

# Create subplots
fig, axs = plt.subplots(2, 2, figsize=(12, 8))

# Plot betweenness centrality
nx.draw(G, pos, ax=axs[0, 0], node_color='orange', node_size=[v * 5000 for v in betweenness_centrality.values()], with_labels=True,edgecolors='black', linewidths=2)
axs[0, 0].set_title('Betweenness Centrality', fontsize=14)

# Plot closeness centrality
nx.draw(G, pos, ax=axs[0, 1], node_color='orange', node_size=[v * 5000 for v in closeness_centrality.values()], with_labels=True, edgecolors='black', linewidths=2)
axs[0, 1].set_title('Closeness Centrality', fontsize=14)

# Plot degree centrality
nx.draw(G, pos, ax=axs[1, 0], node_color='orange', node_size=[v * 5000 for v in degree_centrality.values()], with_labels=True, edgecolors='black', linewidths=2)
axs[1, 0].set_title('Degree Centrality', fontsize=14)

# Plot eigenvector centrality
nx.draw(G, pos, ax=axs[1, 1], node_color='orange', node_size=[v * 5000 for v in eigenvector_centrality.values()], with_labels=True, edgecolors='black', linewidths=2)
axs[1, 1].set_title('Eigenvector Centrality', fontsize=14)

# # Add border around the entire 2x2 plot
# for ax in axs.flatten():
#     ax.spines['top'].set_visible(True)
#     ax.spines['right'].set_visible(True)
#     ax.spines['bottom'].set_visible(True)
#     ax.spines['left'].set_visible(True)

# Create a rectangle patch around the subplot grid
# rect = plt.Rectangle((0, 0), 1, 1, transform=fig.transFigure, edgecolor='black', linewidth=2, fill=False)
# fig.patches.append(rect)
# fig.patch.set_facecolor('ivory')

# Add a title to the entire figure
fig.suptitle('Comparing Metrics of Network Centrality', fontsize=24)

plt.tight_layout()
plt.show()
```

![image](https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/dbda4743-91e6-4e88-8711-822da2b7c4cd)
















