---
layout: post
title:  "Neuronio artificial"
subtitle:  "Iniciando uma rede neural"
date:   2016-11-27 19:19:34 -0300
comments: true
categories: "data-science fundamentals"
tags: "portuguese"
---
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=AM_HTMLorMML"></script>

Já no começo do século XX <i><b>Alan Turing e John Von Newman(MCCULLOCH; PITTS,1943)</b></i> asseguraram que a inteligência podia ser representada por matemática booleana. Segundo <i><b> MCCULLOCH&PITTS (1943)</b></i> este modelo de neurônio é formado por um conjunto de `entradas` (<i>X0, X1, …, Xn</i>) e as sinapses são representadas por `pesos` numéricos(<i>wj0, wj1, …, wjn</i>), que podem tanto assumir valor positivo quanto negativo, fazendo com que o neurônio seja excitado ou inibido. Após a multiplicação das `entradas` pelos `pesos`,esses resultantes são somados pelo `somador` (Σ) ou combinador linear e o valor é submetido a uma `função de ativação` ou função de transferência (T), que gera uma `saída`.


Neurônios artificiais são estruturas compostas de `Entradas`, `Pesos`, `Somador`, `Bias`, `Função de ativação` e `Saída`.

<img src="https://raw.githubusercontent.com/tiagofabre/tiagofabre.github.io/master/images/neuron/neuron-diagram.png">

Matematicamente o combinador linear (Σ) deste neurônio (uk) da é representado pela equação:

<img src="https://raw.githubusercontent.com/tiagofabre/tiagofabre.github.io/master/images/neuron/neuron-equation.png">

A `função de ativação` F(a) serve como um limitador da `saída` restringindo os valores para intervalos previamente definidos. Além de agir sobre os valores de `saída` do neurônio, a `função de ativação` também tem a função de aumentar ou diminuir a entrada liquida de um neurônio, tendo geralmente um valor fixo iguala 1 ou -1. Dessa forma, a representação do valor de `saída` do neurônio seria dada por

<img src="https://raw.githubusercontent.com/tiagofabre/tiagofabre.github.io/master/images/neuron/activation-function.png">

A `função de ativação` ou `função de transferência` determina o momento em que o neurônio será ativado, com base no valor que é recebido do somador. Existem diversas funções de ativação, que podem ser binárias ou com uma `saída` mais abrangente (LISA, 2005) como:

<ul>
	<li>Função degrau</li>
	<li>Função linear</li>
	<li>Função logística</li>
	<li>Função tangente hiperbólica</li>
</ul>

### Referências

<ul>
	
	<li>
		LISA, Sammer.Merkmalbasierte Zeichenerkennung mittels neuronaler Netze.2005. 124 f. Tese (Doutorado) -Curso de Matemática, Universitat Bayreuth Mathematisches Institut, Bayreuth, 2005. Disponível em: <http://num.math.uni-bayreuth.de/de/thesis/2005/Sammer_Lisa/Sammer_Lisa.pdf>. Acesso em: 29 jun. 2015.
	</li>

	<li>
		MCCULLOCH, Warren; PITTS, Walter.A Logical Calculus of the Ideas Immanent in Nervous Activity.1943. Disponível em: http://www.cse.chalmers.se/~coquand/AUTOMATA/mcp.pdf. Acesso em: 14/06/2015
	</li>

</ul>
