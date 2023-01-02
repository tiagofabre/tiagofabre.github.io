---
layout: post
title:  "Guardando sessões http no redis"
subtitle:  "Integrando a sessão do Express.js ao redis para escalar horizontalmente o backend"
date:	2016-12-09 21:49:09 -0300
comments: true
categories: "database web-dev portuguese"
---

## Session

Sessão é um mecanismo que guarda determinadas informações no cliente através de cookies, os quais podem ser acessados pelo servidor no corpo das requisições. Um dos usos mais utilizados é para autorização de usuários, onde o cliente autentica com o servidor e o servidor cria uma sessão com a informação dizendo que aquele usuário ja está autenticado.

A criação da sessão cria um objeto no servidor e envia para o usuário uma chave de acesso (através de cookies) a esse objeto. Por existir esse objeto no servidor chamamos essa operação de operação stateful, o que dificulta a utilização dessa aplicação em múltiplas maquinas por estarem isoladas.

## Redis

Uma forma de fazer com que outro servidor tenha acesso a esse objeto da sessão é utilizando um banco de dados em memória o qual tem uma velocidade de escrita e leitura muito superior a de banco de dados convencionais. Onde o servidor que vai criar a sessão guarda a informação no redis e caso o load-balancer da aplicação direcione o cliente para outro servidor o mesmo consegue saber se o cliente está logado acessando o objeto da sessão no redis.


## Express session

O Express através do express-session faz todo esse processo de forma simples apenas adicionando um 'RedisStore' no field 'store' da configuração do express-session

```javascript
var session = require('express-session');
var RedisStore = require('connect-redis')(session);

var sessionMiddleware = session({
  secret: secret,
  store: new RedisStore({client: clientRedis}),
  resave: false,
  saveUninitialized: true
})

app.use(sessionMiddleware)
```

## Referências
[express-session](https://github.com/expressjs/session)

[connect-redis](https://www.npmjs.com/package/connect-redis)

[How does session work](http://machinesaredigging.com/2013/10/29/how-does-a-web-session-work/)
