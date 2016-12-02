---
layout: post
title:  "EventEmitter Pattern Node.js"
date:	2016-12-01 20:35:09 -0300
comments: true
categories: node.js
---

É um padrão muito utilizado no Node.js que nos permite emitir eventos para múltiplos listeners. Pode ser utilizado em momento em que apenas um callback de um evento asincrono não é suficiente.


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

    {% highlight javascript %}
    var fs = require('fs');
    var io = require('socket.io')(3000);
    require('socket.io-stream')(io);
    
    io.on('connection', function(socket){
      io.emit(fs.createReadStream('file.jpg'));
    });
    {% endhighlight %}

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

Por padrão o event emiter não tem um evento 'error' e quando um evento deste tipo é emitido o node apenas lança uma exceção com throw.

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

{% if page.comments %}

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//https-tiagofabre-github-io.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                                


{% endif %}