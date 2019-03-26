---
layout: post
title:  "Teorema CAP"
subtitle: "Consistência, disponibilidade e tolerância a particionamento"
date:	2016-12-10 18:55:09 -0300
comments: true
categories: "computation, database, distributed systems"
---

## CAP Theorem

Na ciência da computação o teorema CAP diz que é impossível para um sistema de computação distribuída prover as três garantias: **Consistência**, **disponibilidade** e **tolerância a particionamento** (funcionamento mesmo que haja interrupção de comunicação entre um ou alguns nós do sistema). O que é diferente da garantia **ACID**.

Banco de dados tradicionais como os *RDBMS* com apenas um nó (Master) possui consistência e disponibilidade, porém nessa disposição não são considerados um sistema distribuído por não ter uma comunicação pela rede.

Bancos de dados que cuidam de dados sensíveis ou que podem causar prejuízos caso o dado não seja o mais atual possível escolhem abrir mão da disponibilidade (CP) o que faz com que eles possam retornar timeout em algumas tentativas de escritas dos clientes. Porém o banco sempre vai retornar o valor correto do saldo dos clientes.

Uma outra configuração dos bancos é escolher abrir mão da consistência (AP), ou seja nem sempre o banco vai retornar o valor mais atualizado dos registros, pois o banco pode retornar respostas no meio de um sync com suas réplicas. Esse tipo de banco é utilizado preferencialmente para guardar logs ou métricas de negócio.