---
layout: post
title:  "HTML5 Imports"
date:   2016-09-06 19:19:34 -0300
comments: true
categories: html javascript ecmascript
---

### Problema
<ul>
<li>O carregamento dos scripts no HTML estão bloqueando a renderização</li>
<li>A execução do script acontece antes mas deveria ser após a renderização</li>
</ul>

A importação de 'scripts' no HTML acontece atraves da tag `script` ([Mais informações][mdn-script]) Porém a importação de multiplos scripts causa o problema de renderização bloqueante ou 'render blocking'

{% highlight html %}
<script src="exemplo1.js"></script>
<script src="exemplo2.js"></script>
<script src="exemplo3.js"></script>
{% endhighlight %}

### Solução
Com o HTML5 é possivel resolver este problema através dos atributos `async` e `defer` onde o `async` faz com que o script seja carregado em pararelo com os demais e o `defer` faz com que o script seja executado apena após a renderização do documento.

{% highlight html %}
<script async defer src="exemplo1.js"></script>
<script async defer src="exemplo2.js"></script>
<script async defer src="exemplo3.js"></script>
{% endhighlight %}

### Relacionados

Importar libs essenciais de renderização (como jQuery) de forma asincrona [link][async-advanced]
Introdução a `Web Components` [link][web-components]

[mdn-script]: https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/script
[async-advanced]: https://varvy.com/pagespeed/critical-render-path.html
[web-components]: http://webcomponents.org/articles/introduction-to-html-imports/

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