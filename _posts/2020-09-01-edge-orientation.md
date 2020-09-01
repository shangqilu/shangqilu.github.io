---
layout: post
title: Graph Orientation Under Edge Updates
---

In graph orientations, we want to orient every edge of a simple graph to obtain a directed graph with low out-degree. 

Graph orientations may serve a building block for some other algorithms and can be very useful in sparse graphs. Suppose that the maximum out-degree is $\delta$ in the oriented graph.  One example is to support adjancency query with $O(\delta)$ answer time and $O(m)$ space where $m$ is the number of edges.  Another one is to list all the triangles in $O(m\delta)$ time. Specifically, for each vertex $u$, we only need to enumerate every two out-neighbors $v, w$ of $u$ and then check whether $u, v, w$ form a triangle.



## 1. Basic Notations

We use $G = (V, E)$ to denote a simple graph. Denote by $m$ the number of edges and $n$ the number of vertices in $G$.

In this note, $\{u,v\}$ represents an undirected edge between vertices $u$ and $v$, while a directed edge from $u$ to $v$ is represented as $(u,v)$. 

An *orientation* of a graph $G$ is a directed graph $G^+$ obtained by giving each edge in $G$ a direction. Define $deg(G^+)$ as the maximum out-degree of $G^+$. We say $G^+$ is a $\delta$-orientation of $G$ if $deg(G^+)\le \delta$.



## 2. Static Graph Orientation

There is a linear time algorithm to find an $O(\alpha)$-orientation of $G$,  where $\alpha$ is the [arboricity](https://en.wikipedia.org/wiki/Arboricity) [CN85] of $G$, which is the smallest number of edge-disjoint forests that cover all the edges in $G$. In general, $\alpha$ is between $1$ and $\lceil \sqrt{m}\rceil$ and is a measure of the *sparcity* of $G$. On the other hand, $G$ has an $O(\alpha)$-orientation only if the arboricity of it is $O(\alpha)$.

The algorithm repeatedly finds a vertex $u$ with a minimum degree in $G$, orients the each edge of $u$ from $u$ to the other vertex and  then remove $u$ and the edge of $u$ from $G$.  At the end, the out-degree of the orientation is bounded by the *[degeneracy](https://en.wikipedia.org/wiki/Degeneracy_(graph_theory))* of $G$, which is a constant approximation of the arboricity of the graph.



## 3. Dynamic Graph Orientation

When there are edge insertions/deletions, the question is how to maintain an $O(\alpha)$-orientation with small update time? More specifically, after an edge update, the directions of some edges in $G^+$ may be flipped,  and we want to make the number of edge flipped as small as possible. 

In this setting, graph orientation becomes more challenging. If only $O(\log^c m)$ edge flips are allowed in each update where $c>0$ is a constant, existing results can only maintain a orientation with out-degree bounded by the largest arboricity in history (see the discussion in [BB20]).

Next, I will introduce some works in [BB20] and [BF99].

### 3.1 An off-line strategy in [BF99]





### 3.2 An simple online strategy in [BB20]







## References

> [BB20] A Simple Greedy Algorithm for Dynamic Graph Orientation
>
> [BF99] Dynamic Representations of Sparse Graphs
>
> [CN85] Arboricity and Subgraph Listing Algorithms










