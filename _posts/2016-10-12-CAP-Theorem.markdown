---
layout: post
title:  "Teorema CAP"
subtitle: "Consistência, disponibilidade e tolerância a particionamento"
date:	2016-12-10 18:55:09 -0300
comments: true
categories: Big-Data, database, distributed systems
---

## CAP Theorem

Na ciência da computação o teorema CAP diz que é impossivel para um sistema de computação distribuida prover as três garantias: **Consistência**, **disponibilidade** e **tolerância a particionamento** (funcionamento mesmo que haja interrupção de comunicação entre um ou alguns nós do sistema). O que é diferente da garantia **ACID**.

Banco de dados tradicionais **ACID** como os **RDBMS** escolhem consistencia ao invés de disponibilidade (Possui uma estrutura solida na forma de guardar os dados, mas perde performance por e pode demorar a responder requisições devido à essa estrutura ser complexa). O exemplo inverso disso são os bancos de dados **NoSQL** que escolhem disponibilidade ao inves de consistência.

Em desenvolvimento...
