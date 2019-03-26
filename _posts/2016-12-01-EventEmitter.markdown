---
layout: post
title:  "EventEmitter Pattern Node.js"
subtitle:  "Aprendendo um novo padrão e entendendo melhor libs como socket.io"
date:	2016-12-01 20:35:09 -0300
comments: true
categories: "computation, node.js"
---

É um padrão muito utilizado no Node.js que nos permite emitir eventos para múltiplos listeners. Pode ser utilizado em momento em que apenas um callback de um evento assíncrono não é suficiente.


Exemplo de implementação de um EventEmitter:

    {% highlight javascript %}
    'use strict'
    const EventEmitter = require('events');
    
    class MyEmitter extends EventEmitter
    const myEmitter = new MyEmitter();
    
    myEmitter.on('event', () => {
      console.log('an event occurred!');
    });
    
    myEmitter.on('event', () => {
      console.log('same event occurred in another place!');;
    });
    
    myEmitter.emit('event');
    {% endhighlight %}

Um exemplo de utilização de `EventEmitter` é o `Socke.IO`:

    
``` javascript

var fs = require('fs');
var io = require('socket.io')(3000);
require('socket.io-stream')(io);

io.on('connection', function(socket){
  io.emit(fs.createReadStream('file.jpg'));
});

```

O EventListener chama os listeners conforme a ordem que eles se registraram.


Uma variação comportamental do `EventEmitter` é `once()` que acontece apenas uma vez e qualquer chamada pra que ele aconteça é ignorada.

    {% highlight javascript %}
    const myEmitter = new MyEmitter();
    var m = 0;
    myEmitter.once('event', () => {
      console.log(++m);
    });
    myEmitter.emit('event');
    // Prints: 1
    myEmitter.emit('event');
    // Ignored
    {% endhighlight %}

#### Tratamento de exceções

Por padrão o event emitter não tem um evento 'error' e quando um evento deste tipo é emitido o node apenas lança uma exceção com throw.

    {% highlight javascript %}
    const myEmitter = new MyEmitter();

    process.on('uncaughtException', (err) => {
      console.log('whoops! there was an error');
    });
   
    myEmitter.emit('error', new Error('whoops!'));
    // Prints: whoops! there was an error
    {% endhighlight %}

O código acima resolve o problema do erro mas como uma boa prática o Node.js recomenda que sempre se crie um evento de erro
 
    const myEmitter = new MyEmitter();
    myEmitter.on('error', (err) => {
      console.log('whoops! there was an error');
    });
    myEmitter.emit('error', new Error('whoops!'));
    // Prints: whoops! there was an error

## Referência

 - [Node.js 7.2 Documentation Events](https://nodejs.org/api/events.html)

 - [Joyenet design patterns](https://www.joyent.com/node-js/production/design)
