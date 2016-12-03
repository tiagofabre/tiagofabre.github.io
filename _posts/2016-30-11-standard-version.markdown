---
layout: post
title:  "Standard version"
date:	2016-11-30 20:35:09 -0300
comments: true
categories: webTooling
---

## Problema

- Especificar em cada versão de uma aplicação as features que foram desenvolvidas e o bugs que foram corrigidos


Desenvolver software pode virar uma tarefa complexa e quando não há organização. Um recurso que se utiliza é criar um arquivo de `changelog` 
que guarda todas as modificações que aconteceram em determinada aplicação entre uma versão e outra. Mas criar este arquivo de logs pode ficar
complicado pois os devs corrigem as tarefas e acabam esquecendo de alterar o `changelog`.

## Solução

Em aplicações `Node.js` é possível resolver este problema através de um package chamado `standard-version` que através das mensagens dos commits
gera o arquivo de `changelog` fazendo com que o desenvolvedor apenas tenha que adicionar um prefixo antes da mensagem do commit.


## Utilização

Instalar o standard version com dependência de desenvolvedor


    npm i --save-dev standard-version


Adicionar um `npm run script` no `package.json`


    {
      "scripts": {
        "release": "standard-version"
      }
    }
    
Para criar/atualizar o arquivo de `changelog` apenas precisamos executar o comando `npm run release`
que um arquivo `CHANGELOG.md` será criado na raiz do projeto.

Para que o `standard-version` identifique as features e correções de bugs as mensagens de commit precisam dos seguintes prefixos:

    fix(Usuários): Corrigido o bug ao entrar um novo usuário no momento X
    feat(Autenticação): Autenticação do usuário através da JWT
    
O plugin oferece o Badge [![Standard Version](https://img.shields.io/badge/release-standard%20version-brightgreen.svg)](https://github.com/conventional-changelog/standard-version)
 que pode ser utilizado atraves de:
 
 <pre class="editor editor-colors"><div class="line"><span class="source gfm"><span class="link"><span class="punctuation definition begin gfm"><span>[!</span><span>[</span></span><span class="entity gfm"><span>Standard&nbsp;Version</span></span><span class="punctuation definition end gfm"><span>]</span></span><span class="markup underline link gfm"><span class="punctuation definition begin gfm"><span>(</span></span><span>https://img.shields.io/badge/release-standard%20version-brightgreen.svg</span><span class="punctuation definition end gfm"><span>)</span></span></span><span class="punctuation definition end gfm"><span>]</span></span><span class="markup underline link gfm"><span class="punctuation definition begin gfm"><span>(</span></span><span>https://github.com/conventional-changelog/standard-version</span><span class="punctuation definition end gfm"><span>)</span></span></span></span></span></div></pre>
 
## Referência

[Standard-version NPM](https://www.npmjs.com/package/standard-version)

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