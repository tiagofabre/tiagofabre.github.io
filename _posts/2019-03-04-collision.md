---
layout: post
title:  "Detecção de colisão"
date:	2019-03-04 16:14:00 -0200
subtitle: "Detecção de colisão entre retângulos"
comments: true
categories: Gamedev
---

## Sobreposição de objetos retangulares

<center>
    <canvas id="collision_canvas" width="600px" height="400px"></canvas>
</center>

<style>
#collision_canvas {
    border-style: solid;
    border-width: 1px;
    border-color: #e2e2e2;
}
</style>

<script>
let canvas = document.querySelector("#collision_canvas")
let ctx = null
let rectWidth = 30
let rectHeight = 30
let obstacles = []
let lengthObstacles = 25

ctx = canvas.getContext("2d")

for(let i=0; i < lengthObstacles; i++) {
    obstacles.push({positionX: (Math.random() * ctx.canvas.width - 30) + 30,
                    positionY: (Math.random() * ctx.canvas.height - 30) + 30})
}

drawObstacles(null, obstacles)

canvas.addEventListener('mousemove', event => {
    mousePositionX = event.offsetX
    mousePositionY = event.offsetY

    ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
    
    drawRect(mousePositionX, mousePositionY, rectWidth, rectHeight, "#773d92")
    drawObstacles(event, obstacles)
})

function drawObstacles(event, obstacles) {
    obstacles.forEach(function(e) {
        const collision = event ? checkCollision(event, e) : false
        drawRect(e.positionX, e.positionY, rectWidth, rectHeight, collision ? "#d80559a1" : "#16a284d9")
    })
}

function checkCollision(mouseEvent, obstacle) {
    mx = mouseEvent.offsetX
    my = mouseEvent.offsetY

    box1 = {left: mx - rectWidth/2,
            right: mx + rectWidth/2,
            top: my - rectHeight/2,
            bottom: my + rectHeight/2}

    box2 = {left: obstacle.positionX - rectWidth/2,
            right: obstacle.positionX + rectWidth/2,
            top: obstacle.positionY - rectHeight/2,
            bottom: obstacle.positionY + rectHeight/2}

    if(box1.right > box2.left) {
        if(box1.left < box2.right) {
            if(box1.bottom >= box2.top) {
                if(box1.top <= box2.bottom) {
                    return true
                }
            }
        }
    }
    return false
}

function drawRect(x, y, w, h, color) {
    ctx.fillStyle = color;
    ctx.fillRect(x-(w/2), y-(h/2), w, h);
}

</script>

É dada pela seguinte verificação:

``` javascript
function checkCollision(box1, box2)
{
    if(box1.right > box2.left) {
        if(box1.left < box2.right) {
            if(box1.bottom >= box2.top) {
                if(box1.top <= box2.bottom) {
                    return true
                }
            }
        }
    }
    return false
}
```