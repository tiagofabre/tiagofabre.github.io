---
layout: post
title:  "Vetores e matrizes"
date:	2018-12-03 08:50:00 -0300
subtitle: "Revisão de vetores e matrizes"
comments: true
categories: "machine-learning, data-science, math"
---


<script src="https://tikzwolke.com/v1/tikzwolke.js"></script>

# Dot Product

$$
\vec{V} .\vec{W} \ =\sum ^{n}_{i=1} v_{i} w_{i}
$$

Angulo entre os vetores

$$
 \begin{array}{l}
\vec{V} .\vec{W} \ =\ \parallel \vec{V} \parallel \parallel \vec{W} \parallel \cos \theta \ \\
\\
\cos \theta \ =\ \frac{\vec{V}\vec{W}}{\parallel \vec{V} \parallel \parallel \vec{W} \parallel }\\
\end{array}
$$

<center>
    <img src="/assets/img/vetores-matrizes/angulo-vetores.svg" alt="/assets/img/vetores-matrizes/angulo-vetores.svg" style="width: 860px;">
</center>

$$
\vec{V} .\vec{W} \ =0
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-prop1.svg" alt="/assets/img/vetores-matrizes/vec-prop1.svg" style="width: 860px;">
</center>

$$
\vec{V} .\vec{W} \  >0
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-prop2.svg" alt="/assets/img/vetores-matrizes/vec-prop2.svg" style="width: 860px;">
</center>

$$
\vec{V} .\vec{W} \ < 0
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-prop3.svg" alt="/assets/img/vetores-matrizes/vec-prop3.svg" style="width: 860px;">
</center>

$$
\vec{V} .\vec{W} \  >C
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-prop4.svg" alt="/assets/img/vetores-matrizes/vec-prop4.svg" style="width: 860px;">
</center>


## Mulriplicação de matriz

### Propriedades

* Distributive property 👍

$$
A( B+C) =AB+AC
$$

* Associative property 👍

$$
A( BC) =( AB) C
$$

* Commutative property 👎

$$
 \begin{array}{l}
AB\neq BA\\
AB=\begin{bmatrix}
1\\
1
\end{bmatrix}\begin{bmatrix}
1 & 1
\end{bmatrix} \ =\begin{bmatrix}
1*1 & 1*1\\
1*1 & 1*1
\end{bmatrix} \ =\ \begin{bmatrix}
1 & 1\\
1 & 1
\end{bmatrix}\\
BA=\begin{bmatrix}
1 & 1
\end{bmatrix}\begin{bmatrix}
1\\
1
\end{bmatrix} =\begin{bmatrix}
1*1+1*1
\end{bmatrix} =2
\end{array}
$$

## Operação

$$
\begin{bmatrix}
1 & 0 & 1\\
2 & 0 & -1\\
0 & 1 & 1
\end{bmatrix}\begin{bmatrix}
4\\
-1\\
5
\end{bmatrix} \ =\ \begin{bmatrix}
1*4 & 0*( -1) & 1*5\\
2*4 & 0*( -1) & -1*5\\
0*4 & 1*( -1) & 1*5
\end{bmatrix} \ =\begin{bmatrix}
9\\
3\\
4
\end{bmatrix}
$$

$$
\begin{bmatrix}
1 & 2\\
-1 & 1
\end{bmatrix}\begin{bmatrix}
1 & 1 & 0\\
0 & 1 & 2
\end{bmatrix} \ =\ \begin{bmatrix}
1*1+2*0 & 1*1+2*1 & 1*0+2*2\\
-1*1+1*0 & -1*1+1*1 & -1*0+1*2
\end{bmatrix} \ =\begin{bmatrix}
1 & 3 & 4\\
-1 & 0 & 2
\end{bmatrix}
$$

$$
\underbrace{\begin{bmatrix}
1 & 0\\
2 & 3\\
4 & 5
\end{bmatrix}}_{3x2}\underbrace{\begin{bmatrix}
2 & 1\\
8 & 7\\
1 & 4
\end{bmatrix}}_{3x2}
$$

A matrizes acima não são multiplicáveis pois o numero de linhas da segunda não é igual ao numero de colunas da primeira assim como o exempli abaixo:

$$
\underbrace{\begin{bmatrix}
2 & 1 & 3\\
4 & 5 & 6
\end{bmatrix}}_{2x3}\underbrace{\begin{bmatrix}
2 & 1\\
8 & 7\\
1 & 4
\end{bmatrix}}_{3x2}
$$


## Hadamard product

$$
\underbrace{\begin{bmatrix}
1 & 0\\
2 & 3\\
4 & 5
\end{bmatrix}}_{3x2}\underbrace{\begin{bmatrix}
2 & 1\\
8 & 7\\
1 & 4
\end{bmatrix}}_{3x2} =\ \begin{bmatrix}
1*2 & 0*1\\
2*8 & 3*7\\
4*1 & 5*4
\end{bmatrix} =\begin{bmatrix}
2 & 0\\
16 & 21\\
4 & 20
\end{bmatrix}
$$

$$
[ A\circ B]_{ij} =a_{ij} b_{ij}
$$

### Propriedades

* Distributive property 👍

$$
A\circ ( B+C) =A\circ B+A\circ C
$$

* Associative property 👍

$$
A\circ ( B\circ C) =( A\circ B) \circ C
$$

* Commutative property 👍

$$
A\circ B=B\circ A
$$


## Geometria das operações

$$
V=\begin{bmatrix}
2\\
1
\end{bmatrix} \ =\ 2\underbrace{\begin{bmatrix}
1\\
0
\end{bmatrix}}_{c_{1}} +1\underbrace{\begin{bmatrix}
0\\
1
\end{bmatrix}}_{c_{2}}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-sum.svg" alt="/assets/img/vetores-matrizes/vec-sum.svg" style="width: 860px;">
</center>

$$
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}\begin{bmatrix}
2 & 1\\
1 & 1
\end{bmatrix} \ =\ \begin{bmatrix}
2 & 1\\
1 & 1
\end{bmatrix}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-dot.svg" alt="/assets/img/vetores-matrizes/vec-dot.svg" style="width: 860px;">
</center>


$$
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}\begin{bmatrix}
1 & 0\\
0 & 0
\end{bmatrix} \ =\ \begin{bmatrix}
1 & 0\\
0 & 0
\end{bmatrix}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-dot2.svg" alt="/assets/img/vetores-matrizes/vec-dot2.svg" style="width: 860px;">
</center>

$$
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}( -1) \ =\ \begin{bmatrix}
-1 & 0\\
0 & -1
\end{bmatrix}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-dot3.svg" alt="/assets/img/vetores-matrizes/vec-dot3.svg" style="width: 860px;">
</center>

## Inversão de matriz

$$
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}\begin{bmatrix}
2 & 1\\
1 & 1
\end{bmatrix} \ =\ \begin{bmatrix}
2 & 1\\
1 & 1
\end{bmatrix}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-dot4.svg" alt="/assets/img/vetores-matrizes/vec-dot4.svg" style="width: 860px;">
</center>

$$
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}\begin{bmatrix}
1 & 0\\
0 & 0
\end{bmatrix} \ =\ \begin{bmatrix}
1 & 0\\
0 & 0
\end{bmatrix}
$$

<center>
    <img src="/assets/img/vetores-matrizes/vec-dot5.svg" alt="/assets/img/vetores-matrizes/vec-dot5.svg" style="width: 860px;">
</center>

$$
 \begin{array}{l}
AA^{-1} =I\\
\\
\begin{bmatrix}
e & f\\
g & h
\end{bmatrix}\begin{bmatrix}
a & b\\
c & d
\end{bmatrix} =\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}\\
\\
\left\{\begin{matrix}
ea+fc\ =1\\
eb+fa=0\\
ga+hc=1\\
gb+hd=0
\end{matrix}\right.
\end{array}
$$

## Conteúdo relacionado

* Cameras de jogos e visualização de jogos ortogonais
* Pseudo inversa de uma matriz