Radial basis function

$$
f( x) =\sum ^{P}_{p=1} a_{p} .R_{p} +b
$$


Resoluação de sistemas pelo metodo da matriz inversa

$$
fx=\begin{cases}
    2a1+1a2=4\\
    1a1+1a2=3
\end{cases}
$$

Reescrevendo em forma de matriz:

$$
\begin{bmatrix}
    2 & 1\\
    1 & 1
\end{bmatrix} \ .
\begin{bmatrix}
    a1\\
    a2
\end{bmatrix} =
\begin{bmatrix}
    4\\
    3
\end{bmatrix}
$$
 
 Podemos utilizar a equação:

$$
\begin{bmatrix}
    R
\end{bmatrix} .
\begin{bmatrix}
    a
\end{bmatrix} =
\begin{bmatrix}
    A
\end{bmatrix}
$$

Isolando a matriz *a*

$$
\begin{bmatrix}
    a
\end{bmatrix} =
\begin{bmatrix}
    R
\end{bmatrix}^{-1}\ .
\begin{bmatrix}
    A
\end{bmatrix}
$$

Obtemos

$$
\begin{bmatrix}
    a1\\
    a2
\end{bmatrix} =
\begin{bmatrix}
    1 & -1\\
    -1 & 2
\end{bmatrix}.
\begin{bmatrix}
    4\\
    3
\end{bmatrix}
$$

Que resulta em

$$
\begin{bmatrix}
    a1\\
    a2
\end{bmatrix} =
\begin{bmatrix}
    1\\
    2
\end{bmatrix}
$$

Porém so conseguimos encontrar a matriz inversa à partir de uma matriz quadrada.
Uma forma de resolver o sistema  não quadrado e utilizando a [matriz pseudo-inversa](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse)
descoberta por [Moore](https://en.wikipedia.org/wiki/E._H._Moore)

Que deduz:


$$
\begin{bmatrix}
R
\end{bmatrix} .\begin{bmatrix}
a
\end{bmatrix} =\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\begin{bmatrix}
I
\end{bmatrix} .\begin{bmatrix}
R
\end{bmatrix} .\begin{bmatrix}
a
\end{bmatrix} =\begin{bmatrix}
I
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\begin{bmatrix}
R
\end{bmatrix} .\begin{bmatrix}
a
\end{bmatrix} =\begin{bmatrix}
R^{t}
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\begin{bmatrix}
R
\end{bmatrix}^{-1} .\begin{bmatrix}
R
\end{bmatrix} .\begin{bmatrix}
a
\end{bmatrix} =\begin{bmatrix}
R
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\begin{bmatrix}
a
\end{bmatrix} =\begin{bmatrix}
R
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\left(\begin{bmatrix}
B
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}\right)^{-1} =\begin{bmatrix}
B
\end{bmatrix}^{-1} .\begin{bmatrix}
A
\end{bmatrix}^{-1}
$$

$$
\left(\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
R
\end{bmatrix}\right)^{-1} =\begin{bmatrix}
R
\end{bmatrix}^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix}^{-1}
$$


$$
\begin{bmatrix}
a
\end{bmatrix} =\left(\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
R
\end{bmatrix}\right)^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
A
\end{bmatrix}
$$

$$
\begin{bmatrix}
a
\end{bmatrix} =\frac{1}{[ R]} \ \begin{bmatrix}
A
\end{bmatrix}
$$

$$
\frac{1}{[ R]} \ =\left(\begin{bmatrix}
R^{t}
\end{bmatrix} .\begin{bmatrix}
R
\end{bmatrix}\right)^{-1} .\begin{bmatrix}
R^{t}
\end{bmatrix}
$$

***

$$
\begin{cases}
1a1\ +\ 2a2\ +\ 1a3\ =4\\
2a1\ +\ 3a2\ +\ 1a3\ =6\\
4a1\ +\ 1a2\ +\ 2a2\ =7\\
1a1\ +\ 5a2\ +\ 2a3\ =8
\end{cases}
$$


$$
\begin{bmatrix}
    a
\end{bmatrix} =
\frac{1}{[ R]} \ 
\begin{bmatrix}
    A
\end{bmatrix}
$$  

onde 

$$\frac{1}{[ R]} =\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t}$$


$$
\begin{bmatrix}
    1 & 2 & 1\\
    2 & 3 & 1\\
    4 & 1 & 2\\
    1 & 5 & 2
\end{bmatrix} .\begin{bmatrix}
    a1\\
    a2\\
    a3
\end{bmatrix} =\begin{bmatrix}
    4\\
    6\\
    8\\
    7
\end{bmatrix}
$$

Encontrando 1/[R]:

$$
\begin{pmatrix}
\begin{bmatrix}
    1 & 2 & 4 & 1\\
    2 & 3 & 1 & 5\\
    1 & 1 & 2 & 2
\end{bmatrix} .\begin{bmatrix}
    1 & 2 & 1\\
    2 & 3 & 1\\
    4 & 1 & 2\\
    1 & 5 & 1
\end{bmatrix}
\end{pmatrix}^{-1} .\begin{bmatrix}
    1 & 2 & 4 & 1\\
    2 & 3 & 1 & 5\\
    1 & 1 & 2 & 2
\end{bmatrix}
$$


$$
\begin{pmatrix}
\begin{bmatrix}
    22 & 17 & 13\\
    17 & 39 & 17\\
    13 & 17 & 10
\end{bmatrix}
\end{pmatrix}^{-1} .\begin{bmatrix}
    1 & 2 & 4 & 1\\
    2 & 3 & 1 & 5\\
    1 & 1 & 2 & 2
\end{bmatrix}
$$


$$
\begin{bmatrix}
    0.3960 & 0.2000 & -0.8549\\
    0.2000 & 0.2000 & -0.6000\\
    -0.8549 & -0.6000 & 2.2313
\end{bmatrix} .\begin{bmatrix}
    1 & 2 & 4 & 1\\
    2 & 3 & 1 & 5\\
    1 & 1 & 2 & 2
\end{bmatrix}
$$


$$
\begin{bmatrix}
    -0.058 & 0.537 & 0.074 & -0.313\\
    0.000 & 0.400 & -0.200 & 0.000\\
    0.176 & -1.278 & 0.443 & 0.607
\end{bmatrix}
$$

Voltando para a equação


$$
\begin{bmatrix}
    a
\end{bmatrix} =
\frac{1}{[ R]} \ 
\begin{bmatrix}
    A
\end{bmatrix}
$$  

$$
[a] =\begin{bmatrix}
    -0.058 & 0.537 & 0.074 & -0.313\\
    0.000 & 0.400 & -0.200 & 0.000\\
    0.176 & -1.278 & 0.443 & 0.607
\end{bmatrix} .\begin{bmatrix}
    4\\
    6\\
    7\\
    8
\end{bmatrix}
$$

$$
[ a] =\begin{bmatrix}
    1\\
    1\\
    1\\
    1
\end{bmatrix}
$$

$$
f( x) =\sum ^{P}_{p=1} a_{p} .R_{p} +b
$$


$$
\begin{array}{ c c }
x & f( x)\\
2 & 3\\
3 & 6\\
4 & 5
\end{array}
$$

Utilizando dois polos:

$$
\begin{array}{l}
C1=2\\
C2=4
\end{array}
$$

$$
\sigma ^{2} =1
$$

$$
R_{p} = e^{-\frac{1}{2\sigma ^{2}} .\parallel ( X_{i}) -( X_{p}) \parallel ^{2}}
$$

$$
\begin{array}{l}
\begin{cases}
e^{-0.5\parallel ( 2) -( 2) \parallel ^{2}} a_{1} +e^{-0.5\parallel ( 2) -( 2) \parallel ^{2}} a_{2} +b=3\\
e^{-0.5\parallel ( 3) -( 2) \parallel ^{2}} a_{1} +e^{-0.5\parallel ( 3) -( 4) \parallel ^{2}} a_{2} +b=6\\
e^{-0.5\parallel ( 4) -( 2) \parallel ^{2}} a_{1} +e^{-0.5\parallel ( 4) -( 4) \parallel ^{2}} a_{2} +b=5
\end{cases}\\
\\
\begin{cases}
e^{-0.0} a_{1} +e^{-2.0} a_{2} +b=3\\
e^{-0.5} a_{1} +e^{-0.5} a_{2} +b=6\\
e^{-2.0} a_{1} +e^{-0.0} a_{2} +b=5
\end{cases}\\
_{\ }\\
\begin{cases}
1.0000a_{1} +0.1353 a_{2} +b1.0000=3\\
0.6065a_{1} +0.6065 a_{2} +b1.0000=3\\
0.1353a_{1} +1.0000 a_{2} +b1.0000=3
\end{cases}
\end{array}
$$
$$
 \begin{array}{l}
\begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.6065 & 0.6065 & 1.0000\\
0.1353 & 1.0000 & 1.0000
\end{bmatrix} .\begin{bmatrix}
a1\\
a2\\
a3
\end{bmatrix} =\begin{bmatrix}
3\\
6\\
5
\end{bmatrix}\\
\\
\begin{bmatrix}
R
\end{bmatrix}_{3x3} .\begin{bmatrix}
a
\end{bmatrix}_{3x1} =\begin{bmatrix}
A
\end{bmatrix}_{3x1}\\
\\
\begin{bmatrix}
R
\end{bmatrix} =\begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.6065 & 0.6065 & 1.0000\\
0.1353 & 1.0000 & 1.0000
\end{bmatrix}_{3x3}\\
\\
\frac{1}{[ R]} =\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t}\\
\\
[ R]^{t} .[ R] =\begin{bmatrix}
1.0000 & 0.6065 & 0.1353\\
0.1353 & 0.6065 & 1.0000\\
1.0000 & 1.0000 & 1.0000
\end{bmatrix}_{3x3} .\ \begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.6065 & 0.6065 & 1.0000\\
0.1353 & 1.0000 & 1.0000
\end{bmatrix}_{3x3}\\
\\
[ R]^{t} .[ R] =\begin{bmatrix}
1.3862 & 0.6386 & 1.7419\\
0.6386 & 1.3262 & 1.7419\\
1.7419 & 1.7419 & 3.0000
\end{bmatrix}_{3x3}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} =\begin{bmatrix}
248.9582 & 247.6207 & -288.3246\\
247.6207 & 248.9582 & -288.3246\\
-288.3246 & -288.3246 & 335.1485
\end{bmatrix}_{3x3}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t} \ =\begin{bmatrix}
248.9582 & 247.6207 & -288.3246\\
247.6207 & 248.9582 & -288.3246\\
-288.3246 & -288.3246 & 335.1485
\end{bmatrix}_{3x3} .\ \begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.6065 & 0.6065 & 1.0000\\
0.1353 & 1.0000 & 1.0000
\end{bmatrix}_{3x3}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t} \ =\begin{bmatrix}
-5.8546 & 12.8657 & -7.0111\\
-7.0111 & 12.8657 & -5.8546\\
7.8034 & -146069 & 7.8034
\end{bmatrix}_{3x3} =\frac{1}{[ R]}\\
\\
\begin{bmatrix}
a
\end{bmatrix} =\frac{1}{[ R]} \ \begin{bmatrix}
A
\end{bmatrix}\\
\\
\begin{bmatrix}
+24.5749\\
+26.8879\\
-25.2138
\end{bmatrix}_{3x1} =\begin{bmatrix}
-5.8546 & 12.8657 & -7.0111\\
-7.0111 & 12.8657 & -5.8546\\
7.8034 & -146069 & 7.8034
\end{bmatrix}_{3x3} .\begin{bmatrix}
3\\
6\\
5
\end{bmatrix}_{3x1}\\
\\
f( x) =\sum ^{2}_{p=1} a_{p} .R_{p} +b\\
\\
f\ ( x) \ =a_{1} e^{-0.5\parallel ( X) -( 2) \parallel ^{2}} +a_{2} e^{-0.5\parallel ( X) -( 4) \parallel ^{2}} +b\\
\\
f\ ( x) \ =24.5749e^{-0.5\parallel ( X) -( 2) \parallel ^{2}} +26.8879e^{-0.5\parallel ( X) -( 4) \parallel ^{2}} -25.2138\\
\\
X=( 2) \Longrightarrow 24.5749e^{0.0} +26.8879e^{-2.0} -25.2138\ =3\\
\\
X=( 3) \Longrightarrow 24.5749e^{-0.5} +26.8879e^{-0.5} -25.2138\ =6\\
\\
X=( 4) \Longrightarrow 24.5749e^{-2.0} +26.8879e^{0.0} -25.2138\ =5\\
\\
f( 1.5) =-2.3451\\
\\
f( 2.5) =+5.2027\\
\\
f( 3.5) =+6.4930\\
\\
f( 4.5) =-0.4055\\
\end{array}
$$


## XOR input

$$
\begin{array}{l}
\begin{matrix}
x & f( x)\\
1,1 & 0\\
0,1 & 1\\
0,0 & 0\\
1,0 & 1
\end{matrix}\\
\\
\\  
 \begin{array}{l}
Polos\\
C1=( 1,1)\\
C2\ =( 0,0)
\end{array}\\
\\
\begin{cases}
e^{-1\parallel ( 1,1) -( 1,1) \parallel ^{2}} a_{1} +e^{-1\parallel ( 1,1) -( 0,0) \parallel ^{2}} a_{2} +b=0\\
e^{-1\parallel ( 0,1) -( 1,1) \parallel ^{2}} a_{1} +e^{-1\parallel ( 0,1) -( 0,0) \parallel ^{2}} a_{2} +b=1\\
e^{-1\parallel ( 0,0) -( 1,1) \parallel ^{2}} a_{1} +e^{-1\parallel ( 0,0) -( 0,0) \parallel ^{2}} a_{2} +b=0\\
e^{-1\parallel ( 1,0) -( 1,1) \parallel ^{2}} a_{1} +e^{-1\parallel ( 1,0) -( 0,0) \parallel ^{2}} a_{2} +b=1
\end{cases}\\
\\
\begin{cases}
e^{-0} a_{1} +e^{-2} a_{2} +b=0\\
e^{-1} a_{1} +e^{-1} a_{2} +b=1\\
e^{-2} a_{1} +e^{-0} a_{2} +b=0\\
e^{-1} a_{1} +e^{-1} a_{2} +b=1
\end{cases}\\
\\
\begin{cases}
1.0000a_{1} +0.1353 a_{2} +b1.0000=0\\
0.3678a_{1} +0.3678 a_{2} +b1.0000=1\\
0.1353a_{1} +1.0000 a_{2} +b1.0000=0\\
0.3678a_{1} +0.3678 a_{2} +b1.0000=1
\end{cases}\\
\\
\begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.3678 & 0.3678 & 1.0000\\
0.1353 & 1.0000 & 1.0000\\
0.3678 & 0.3678 & 1.0000
\end{bmatrix} .\begin{bmatrix}
a1\\
a2\\
b
\end{bmatrix} =\begin{bmatrix}
0\\
1\\
0\\
1
\end{bmatrix}\\
\\
\begin{bmatrix}
R
\end{bmatrix}_{4x3} .\begin{bmatrix}
a
\end{bmatrix}_{3x1} =\begin{bmatrix}
A
\end{bmatrix}_{4x1}\\
\\
\begin{bmatrix}
R
\end{bmatrix} =\begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.3678 & 0.3678 & 1.0000\\
0.1353 & 1.0000 & 1.0000\\
0.3678 & 0.3678 & 1.0000
\end{bmatrix}_{4x3}\\
\\
\frac{1}{[ R]} =\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t}\\
\\
[ R]^{t} .[ R] =\begin{bmatrix}
1.0000 & 0.3678 & 0.1353 & 0.3678\\
0.1353 & 0.3678 & 1.0000 & 0.3678\\
1.0000 & 1.0000 & 1.0000 & 1.0000
\end{bmatrix}_{3x4} .\begin{bmatrix}
1.0000 & 0.1353 & 1.0000\\
0.3678 & 0.3678 & 1.0000\\
0.1353 & 1.0000 & 1.0000\\
0.3678 & 0.3678 & 1.0000
\end{bmatrix}_{4x3}\\
\\
[ R]^{t} .[ R] =\begin{bmatrix}
1.2889 & 0.5413 & 1.8711\\
0.5413 & 1.2890 & 1.8711\\
1.8711 & 1.8711 & 4.0000
\end{bmatrix}_{3x3}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} =\begin{bmatrix}
6.9320 & 5.5945 & -5.8596\\
5.5945 & 6.9320 & -5.8596\\
-5.8596 & -5.8596 & 5.7319
\end{bmatrix}_{3x3}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t} =\begin{bmatrix}
6.9320 & 5.5945 & -5.8596\\
5.5945 & 6.9320 & -5.8596\\
-5.8596 & -5.8596 & 5.7319
\end{bmatrix}_{3x3} .\begin{bmatrix}
1.0000 & 0.3678 & 0.1353 & 0.3678\\
0.1353 & 0.3678 & 1.0000 & 0.3678\\
1.0000 & 1.0000 & 1.0000 & 1.0000
\end{bmatrix}_{3x4}\\
\\
\left([ R]^{t} .[ R]\right)^{-1} .[ R]^{t} =\begin{bmatrix}
1.8296 & -1.2513 & 0.6731 & -1.2513\\
0.6731 & -1.2513 & 1.8295 & -1.2513\\
-0.9207 & 1.4207 & -0.9207 & 1.4207
\end{bmatrix}_{3x4} =\frac{1}{[ R]}\\
\\
\begin{bmatrix}
a
\end{bmatrix} =\frac{1}{[ R]} \ \begin{bmatrix}
A
\end{bmatrix}\\
\\
\begin{bmatrix}
-2.5027\\
-2.5027\\
2.8413
\end{bmatrix}_{3x1} .\begin{bmatrix}
1.8296 & -1.2513 & 0.6731 & -1.2513\\
0.6731 & -1.2513 & 1.8295 & -1.2513\\
-0.9207 & 1.4207 & -0.9207 & 1.4207
\end{bmatrix}_{3x4} =\begin{bmatrix}
0\\
1\\
0\\
1
\end{bmatrix}_{4x1}\\
\\
f( x) =\sum ^{2}_{p=1} a_{p} .R_{p} +b\\
\\
f\ ( x) \ =a_{1} e^{-1\parallel ( X) -( 1,1) \parallel ^{2}} +a_{2} e^{-1\parallel ( X) -( 0,0) \parallel ^{2}} +b\\
\\
f\ ( x) \ =-2.5027e^{-1\parallel ( X) -( 1,1) \parallel ^{2}} -2.5027e^{-1\parallel ( X) -( 0,0) \parallel ^{2}} +2.8413\\
\\
X=( 1,1) \Longrightarrow -2.5027e^{0} -2.5027e^{-2} +2.8413=0\\
\\
X=( 0,1) \Longrightarrow -2.5027e^{-1} -2.5027e^{-1} +2.8413=1\\
\\
X=( 0,0) \Longrightarrow -2.5027e^{-2} -2.5027e^{0} +2.8413=0\\
\\
X=( 1,0) \Longrightarrow -2.5027e^{-1} -2.5027e^{-1} +2.8413=1
\end{array}
$$
