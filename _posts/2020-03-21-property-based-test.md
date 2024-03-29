---
layout: post
title:  "Property based test"
date:	2020-03-21 00:00:00 -0300
subtitle: "Melhorando a qualidade dos testes"
comments: true
categories: "computer-science test math"
tags: "portuguese"
---

<style>
.center {
    margin: 0 auto;
 }   

.example-bugs {
    width: 400px;
    height: 400px;
}
</style>

<script>


let sketch = function(p) {
    function randomPosition(max) {
        return Math.random() * max * 2;
    }
    
    p.setup = function(){
        
        // Global vars
        p.createCanvas(400, 400)
    }

    p.draw = function(){
        p.strokeWeight(5)

        // Testes points
        p.background(220)
        p.stroke(p.color(60, 60, 60))

        for (let i = 0; i < 200; i++) {
            p.point(randomPosition(i), randomPosition(i))
        }

        // Bug
        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))  
        p.point(25, 123)

        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))
        p.point(175, 83)

        p.frameRate(1)
    }
}

new p5(sketch, 'test-bugs');
</script>

<script>
let sketchExamples = function(p) {

    function randomPosition(max) {
    return Math.random() * max * 0.4;
    }

    p.setup = function(){
        
        // Global vars
        p.createCanvas(400, 400)
    }

    p.draw = function(){
        p.strokeWeight(5)

        // Testes points
        p.background(220)
        p.stroke(p.color(60, 60, 60))

        for (let i = 0; i < 1000; i++) {
            p.point(randomPosition(i), randomPosition(i))
        }

        // Bug
        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))  
        p.point(25, 123)

        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))
        p.point(175, 83)

        p.frameRate(1)
    }
}

new p5(sketchExamples, 'test-bugs-n-examples');
</script>

<script>
let sketchCustomResize = function(p) {

    function randomPosition(i, max) {
        return Math.random() * max * 0.4;
    }

    p.setup = function(){
        
        // Global vars
        p.createCanvas(400, 400)
    }

    p.draw = function(){
        p.strokeWeight(5)

        // Testes points
        p.background(220)
        p.stroke(p.color(60, 60, 60))

        let max = 1000
        for (let i = 0; i < max; i++) {
            p.point(randomPosition(i, max), randomPosition(i, max))
        }

        // Bug
        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))  
        p.point(25, 123)

        p.strokeWeight(30)
        p.stroke(p.color(240, 40, 40, 200))
        p.point(175, 83)

        p.frameRate(1)
    }
}

new p5(sketchCustomResize, 'test-bugs-custom-resize');
</script>

# Introdução a Testes baseados em propriedade

Mesmo com testes unitários, seu código ainda pode ter bugs. Então como encontrar os bugs do código que se escreve?

## Testar as propriedades do seu código:

Encontrar as propriedades de uma função faz com que você pense no problema de uma forma diferente, já que ao invés de pensar em exemplos de input você pensa em tipos de dados e intervalos de valores aceitáveis de deixa que uma ferramenta gere dados para você de uma forma aleatória, centenas ou milhares de vezes.

Imagine um mundo onde cada função que escrevemos possui um teste que valida todas os inputs possíveis. Exemplo: Se tenho uma função que recebe um valor inteiro. Para ele existiria um teste onde todos os inteiros existentes fossem passados para esta função, verificando que ela funciona com todos esses valores, inclusive valores `negativos`, `zero`, `+infinito`, `-infinito` e `NaN`.

## Problema

Seria o mundo ideal testar suas funções com todas as possibilidades possíveis, porém gerar todos os valores é algo muito demorado e quando feito para todas as propriedades de uma função e para centenas ou milhares de funções temos essa prática inviabilizada. Mas o que poderíamos fazer?

Daria para chegar próximo à isso se a utilizando valores aleatórios gerados centenas ou até milhares de vezes.


## Como fazer?

- Definir os valores aleatórios que devem ser gerados
- Definir uma expressão que valida o teste
- Definir o número de testes a serem gerados


Exemplo:

Serão gerados 200 valores entre 0 e 400 (pra facilitar a visualização)

<div >
    <div id="test-bugs" class="example-bugs center"></div>
    <center>
        <i>Exemplo de bugs em determinadas áreas e os testes cobrindo/encontrando os bugs</i>
    </center>
</div>

O exemplo acima é um possível exemplo de uma função que recebe dois valores numéricos e que em determinados valores a função não se comporta como o esperado (áreas em vermelho). Com isso é possível ver que jogando valores aleatórios é possível gerar valores que cobrem área e os bugs são encontrados.

Também é possível ver que em determinados momentos o bug não é encontrado (nenhum ponto preto intercepta a área vermelha). Uma forma de melhorar isso e fazer com que se encontre os bugs é aumentar a quantidades de valores que vão testar a função.

<div>
    <div id="test-bugs-n-examples" class="example-bugs center"></div>
    <center>
        <i class="center">Aumentando o numero de testes</i>
    </center>
</div>

Aumentando o número de testes podemos ver melhor uma concentração grande de valores no canto superior esquerdo. Isso acontece devido ao size dos valores aleatórios que em muitos frameworks sorteiam números com base no número de testes a serem gerados. Como na função abaixo:

``` clojure
(fn [index] (choose 0 index)) ; index quer dizer o numero de testes que ja forma gerados
```

Uma forma de resolver isso é mudando o size da função como ilustra o exemplo abaixo:

<div class="center">
    <div id="test-bugs-custom-resize" class="example-bugs center"></div>
    <center>
        <i>Exemplo de um size customizado</i>
    </center>
</div>

No Clojure `test.check` podemos fazer isso através da função [resize](https://github.com/clojure/test.check/blob/master/doc/growth-and-shrinking.md#genresize)
