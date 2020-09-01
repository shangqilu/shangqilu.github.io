---
layout: post
title: Graph orientations with bounded out-degree
output: html_document
bibliography: ref.bib
---

In graph orientations, we want to orient every edge of a simple graph to obtain a directed graph with low out-degree. 

Graph orientations can serve a building block for some other algorithms. Suppose that the maximum out-degree is $\delta$ in the oriented graph.  One application is to support adjancency query with $O(\delta)$ answer time and $O(m)$ space where $m$ is the number of edges.  Another one is to list all the triangles in $O(m\delta)$ time. Specifically, for each vertex $u$, we only need to enumerate every two out-neighbors $v, w$ of $u$ and then check whether $u, v, w$ forms a triangle. 



## 1. Basic Notations

We use $G = (V, E)$ to denote a simple graph. Denote by $m$ the number of edges and $n$ the number of vertices in $G$.

In this note, $\{u,v\}$ represents an undirected edge between vertices $u$ and $v$, while a directed edge from $u$ to $v$ is represented as $(u,v)$. 

An *orientation* of a graph $G$ is a directed graph $G^+$ obtained by giving each edge in $G$ a direction.



## 2. Static Graph Orientation

There is a linear time algorithm to find an orientation of $G$ with max out-degree $O(\alpha)$, where $\alpha$ is the [arboricity](https://en.wikipedia.org/wiki/Arboricity) of $G$, which is the smallest number of edge-disjoint forests that cover all the edges in $G$; in general, $\alpha$ is between $1$ and $\lceil \sqrt{m}\rceil$.

Later



## 3. Dynamic Graph Orientation





### 3.1 An off-line strategy





# References






