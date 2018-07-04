---
layout: post
title:  "Algoritimo genético"
date:	2016-11-30 20:35:09 -0300
comments: true
categories: Machine-learning data-science
---

Tendo um dataset hipotético com 3 features podemos representa-los atraves de:

Sexo | Idade    | Sintoma      | Daginostico
 0;1 | 0;1;0;0  | 0;1;0;1;0;0  | 1
 0;1 | 0;1;0;0  | 0;1;0;0;0;0  | 0
 1;0 | 0;1;0;0  | 0;1;0;0;0;0  | 0
 1;0 | 0;1;0;0  | 1;0;0;1;0;0  | 1

Sendo no sexo respectivamente masculino e feminino
na idade respectivamente de 0 a 20,de 20 a 40, 40 a 60, 60 +
e o sintoma sendo sendo tosse seca, febre, diarreia, manchas no corpo, dor de garganta, X, Y e Z
O diagnostico é o resultado diganosticado por um especialista dizendo se o paciente tem a doenca X ou não

Para criar uma solucao é preciso criar alguns individuos que suporte todas essas features, ou seja será preciso individuos com no minimo 12 cromossomos

para fazaer isso sorteamos 12 numeros aleatórios para cada individuos


individuo1 = [0.4446926  0.59343858 0.70837683 0.66555158 0.13439199 0.94390958 0.06488285 0.01318221 0.83431067 0.46803834 0.30197153 0.94194467]
individuo2 = [0.14751403 0.98293243 0.39077686 0.25116452 0.13573441 0.23722197 0.39239264 0.1596161  0.48951393 0.8997783  0.64295595 0.61457108]
individuo3 = [0.43224167 0.22627665 0.66722017 0.06624968 0.13514032 0.79314953 0.40153436 0.5953709  0.31984319 0.25358895 0.52797932 0.85551707]
individuo4 = [0.06631595 0.23386993 0.95740376 0.67177216 0.27449152 0.81743309 0.28891403 0.96618539 0.41207696 0.3943861  0.7023933  0.22065646]
individuo5 = [0.83722251 0.26851182 0.48519195 0.34374418 0.86785779 0.34057811 0.33036101 0.89066606 0.27335567 0.65566881 0.01440101 0.78016194]
individuo6 = [0.61869326 0.36646116 0.23473808 0.17886999 0.39160891 0.70844053 0.24346035 0.1907936  0.47029346 0.53354231 0.35229775 0.58972727]

com isso podemos verificar a eficiencia dos individuos atraves de

b0+ s0 + s1 + I1 + I2 + I3 + I4 + s1 + s2 + s3 + s4 + s5 + s6


