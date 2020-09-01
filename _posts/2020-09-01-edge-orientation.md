---
layout: post
title: Dynamic graph orientation with bounded out-degree
---

In graph orientations, we want to orient every edge of a simple graph to obtain a directed graph with low out-degree. How to get a graph orientation and how to maintain a graph orientation under edge updates?



Suppose that the maximum out-degree is $\delta$ in the oriented graph.  There are many applications. One application is to support adjancency query with $O(\delta)$ answer time and $O(m)$ space where $m$ is the number of edges.  Another one is to list all the triangles in $O(m\delta)$ time.



## Basic Notations







## Static Graph Orientation

For static graph, there is a simple way to make the out-degree bounded by arboricity of $G$.



## Dynamic Graph Orientation





### An off-line strategy






