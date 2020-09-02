---
layout: post
title: Graph Orientation Under Edge Updates
---

In *graph orientation*, we want to orient every edge of a simple graph to obtain a directed graph with low out-degree. 

Graph orientation may serve a building block for some other algorithms. Suppose that the maximum out-degree is $\delta$ in the oriented graph.  We can construct adjacency lists to support adjacency query with $O(\delta)$ answer time and $O(m)$ space where $m$ is the number of edges.  Another example is to list all the triangles in $O(m\delta)$ time. Specifically, for each vertex $u$, we only need to enumerate every two out-neighbors $v, w$ of $u$ and then check whether $u, v, w$ form a triangle. When $\delta$ is small, the above algorithms would be very efficient. This usually happens in *sparse* graphs. 



## 1. Notations

We use $G = (V, E)$ to denote a simple graph. Denote by $m$ the number of edges and $n$ the number of vertices in $G$.

In this note, $\{u,v\}$ represents an undirected edge between vertices $u$ and $v$, while a directed edge from $u$ to $v$ is represented as $(u,v)$. 

An *orientation* of a graph $G$ is a directed graph $G^+$ obtained by giving each edge in $G$ a direction. Define $deg(G^+)$ as the maximum out-degree of $G^+$. We say $G^+$ is a $\delta$-orientation of $G$ if $deg(G^+)\le \delta$.

The [arboricity](https://en.wikipedia.org/wiki/Arboricity) \[CN85\], denoted by $\alpha$, is the smallest number of edge-disjoint forests that cover all the edges in $G$. In general, $\alpha$ is between $1$ and $\lceil \sqrt{m}\rceil$ and is a measure of the *sparsity* of $G$， while $\alpha=O(1)$  in planar graphs, or graphs with bounded degree or bounded tree-width. Existing works mainly focus on finding a $O(\alpha)$-orientation. 

## 2. Static Graph Orientation

There is a linear-time algorithm to find an $O(\alpha)$-orientation of $G$.

The algorithm repeatedly finds a vertex $u$ with a minimum degree in $G$, orients each edge of $u$ from $u$ to the other vertex, and then remove $u$ and the edge of $u$ from $G$.  In the end, the out-degree of the orientation is bounded by the *[degeneracy](https://en.wikipedia.org/wiki/Degeneracy_(graph_theory))* of $G$, which is a constant approximation of the arboricity of the graph.

On the other hand, it is rudimentary to verify that $G$ has an $O(\alpha)$-orientation only if the arboricity is $O(\alpha)$. 



## 3. Dynamic Graph Orientation

When there are edge insertions/deletions, the question is how to maintain an $O(\alpha)$-orientation with small update time. More specifically, after an edge update, the directions of some edges in $G^+$ may be flipped,  and we want to make the number of edges flipped as small as possible. 

In this setting, graph orientation becomes more challenging. If only $O(\log^c m)$ edge flips are allowed in each update where $c>0$ is a constant, existing results can only maintain an orientation with out-degree bounded by the largest arboricity in history (see the discussion in \[BB20\]).

Next, I will introduce some works in \[BB20\] and \[BF99\]. Given a sequence of updates where each update $i$ is either an edge insertion or an edge deletion, an online algorithm receives the sequence as a stream and upon receiving update $i$, it produces an orientation $G^+_i$ of the current graph. While an off-line strategy knows the sequence before it produces an orientation after each update. Therefore, finding an online algorithm is more difficult.

### 3.1 An off-line strategy

The off-line strategy given in \[BF99\] is as follows.

> Lemma 1. There is an off-line strategy to maintain a $O(\alpha_h)$-orientation with $O(\log n)$ flips in each update where $\alpha_h$ is the largest arboricity in history.

Note that the off-line strategy knows $\alpha_h$. The proof of Lemma 1 follows from the interesting lemma: 

> Lemma 2. Let $G$ be a graph with arboricity $\alpha$ and $G^+$ be an orientation of $G$. If $G^+$ has a vertex $u$ with out-degree at leaset $\delta = 2\alpha$, then there exists a vertex $v$ with out-degree less than $\delta$ and a directed $u$-to-$v$ path containing at most $\lceil log_2 n \rceil$ edges.

We can maintain a $\delta$-orientation with $O(\log n)$ flips at each update.  No edges are flipped in each deletion. After inserting an edge $\{u,v\}$ into $G$, without loss of generality, we orient it into $(u,v)$ If the out-degree of $u$ is larger than $\delta$, due to Lemma 2, we can find a $u$-to-$w$ path in $G^+$ with length $O(\log n)$ such that $w$ has a out-degree less than $\delta$. By reversing all the edges on this path, only the out-degree of $w$ increases by one.  

*Proof of Lemma 2*. Let $V_i$ be the set of vertices reachable from $u$ in $G^+$ by paths with length at most $i$. The claim is $|V_i|\ge 2^i$ if all vertices in $V_i$ has out-degree at least $\delta$. Becasue $|V_i|\le n$, then we have $i < \log_2 n$ and the lemma follows. We can prove this claim by induction and use the property that $|E'|/(|V'|-1) \le \alpha_h$ for any subgraph of $G$ (see more details in [BF99]).

### 3.2 An simple online strategy

\[BB20\] gives a simple online algorithm:

>  Lemma 3. There is an online algorithm maintains an $O(\alpha_h + \log n)$-orientation with $O(\log n)$ flips at each update.

The algorithm is very simple. Each vertex $v$ has a FIFO queue $Q_v$ which stores its out-neighbors. For each insertion, the algorithm orients the new edge arbitrarily. Then it does $k = \theta(\log n)$ times *max-flips*: in each max-flip, it picks a vertex $v$ with maximum out-degree and flips the first edge in $Q_v$. While for each deletion,  no edge flips are performed. 

The analysis is non-trivial, which shows that the algorithm is competitive to the off-line strategy in Lemma 1. Here I only give some basic ideas about the proof. The first interesting lemma is that after $k$ max-flips, the max out-degree increased by at most one. Hence, a max-flip is performed on a vertex with out-degree $O(\alpha_h)$, after the $k$ max-flips, $G^+$ is still an $O(\alpha_h)$-orientation. 

The most difficult part is to bound the maximum out-degree after we have performed a sequence of updates where each max-flip is performed on a vertex with out-degree at least $c \cdot \alpha_h$ for some constant $c$. Since each insertion makes the out-degree of a vertex increase by one, it is not easy to directly bound the maximum out-degree. The paper introduced a notion of potential for each vertex $v$ which is an approximation of the out-degree of $v$. Hence, we only need to bound the maximum potential of the vertices. An important property is the total potential of all the vertices is non-increasing when the above scenario happens.



## References

> \[BB20\] A Simple Greedy Algorithm for Dynamic Graph Orientation
>
> \[BF99\] Dynamic Representations of Sparse Graphs
>
> \[CN85\] Arboricity and Subgraph Listing Algorithms
