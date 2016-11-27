---
layout: post
title:  "HTML5 Imports"
date:   2016-09-06 19:19:34 -0300
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
Com o HTML5 é possivel resolver este problema através dos atributos 'async' e 'defer' onde o 'async' faz com que o script seja carregado em pararelo com os demais e o 'defer' faz com que o script seja executado apena após a renderização do documento.

{% highlight html %}
<script async defer src="exemplo1.js"></script>
<script async defer src="exemplo2.js"></script>
<script async defer src="exemplo3.js"></script>
{% endhighlight %}

### Relacionados

Importar libs essenciais de renderização (como jQuery) de forma asincrona [link][async-advanced]
Introdução a 'Web Components' [link][web-components]

[mdn-script]: https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/script
[async-advanced]: https://varvy.com/pagespeed/critical-render-path.html
[web-components]: http://webcomponents.org/articles/introduction-to-html-imports/

