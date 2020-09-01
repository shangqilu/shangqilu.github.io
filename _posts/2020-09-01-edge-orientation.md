---
layout: post
title: Dynamic graph orientation with bounded out-degree
---

In graph orientations, we want to orient every edge of a simple graph to obtain a directed graph with low out-degree. How to get a graph orientation and how to maintain a graph orientation under edge updates?



Suppose that the maximum out-degree is $$\delta$$.  There are many applications. One application is to support adjancency query with $$O(\delta)$$ answer time and linear space.  Another one is to list all the triangles in $$O(m\delta)$$ time where $$m$$ is the number of edges.



## Static graph





## Dynamic graph orientation





### An off-line strategy



$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$








