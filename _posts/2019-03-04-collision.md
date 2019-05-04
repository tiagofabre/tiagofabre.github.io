---
layout: post
title:  "Detecção de colisão"
date:	2019-03-04 16:14:00 -0200
subtitle: "Simulação de detecção de colisão"
comments: true
categories: "gamedev, computation"
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

Number.prototype.clamp = function(min, max) {
  return Math.min(Math.max(this, min), max)
}

const width = 600
const height = 400
const canvas = document.querySelector("#collision_canvas")
const ctx = canvas.getContext("2d")
const rectWidth = 30
const rectHeight = 30
const lengthObstacles = 150
const collisionColor = "#d80559a1"
const pointerColor = "#773d92"

const palletColor = ["#FFF2F2","#FFBF59", "#E89951", "#FF9966", "#E86D51", "#FF6059", "#BF6060", "#F26B5E", "#F2913D"]

const obstacles = [... Array(lengthObstacles)].map(generateRandomRect)

canvas.addEventListener('touchmove', drawWorld)
canvas.addEventListener('mousemove', drawWorld)

fillBackground(palletColor[0])
drawObstacles(obstacles)


function clearCanvas() {
    ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height)
}

function getColorFromPallet(pallet) {
    const min=1; 
    const max=pallet.length-1;  
    const random =Math.floor(Math.random() * (+max - +min)) + +min;
    return pallet[random]
}

function generateRandomRect() {
    const elementWidth = (Math.random() * rectWidth * 3).clamp(rectWidth, rectWidth * 1.6)
    const elementHeight = (Math.random() * rectHeight * 3).clamp(rectHeight, rectHeight * 1.6)
    return {width:        elementWidth,
            height:       elementHeight,
            positionX:    (Math.random() * ctx.canvas.width).clamp(elementWidth/2, ctx.canvas.width - elementWidth/2),
            positionY:    (Math.random() * ctx.canvas.height).clamp(elementHeight/2, ctx.canvas.height - elementHeight/2),
            initialColor: getColorFromPallet(palletColor)}
}

function drawRect(x, y, w, h, color) {
    ctx.fillStyle = color;
    ctx.fillRect(x-(w/2), y-(h/2), w, h);
}

function chooseColor(collision, element) {
    return collision ? collisionColor : element.initialColor
}

function fillBackground(color) {
    ctx.rect(0, 0, ctx.canvas.width, ctx.canvas.height);
    ctx.fillStyle = color;
    ctx.fill();
}

function drawObstacles(obstacles) {
    obstacles.forEach(function(e) {
        drawRect(e.positionX, e.positionY, e.width, e.height, e.color ? e.color : e.initialColor)
    })
}

function checkCollision(event, obstacle) {
    const {offsetX, offsetY} = event

    box1 = {left: offsetX - obstacle.width/2,
            right: offsetX + obstacle.width/2,
            top: offsetY - obstacle.height/2,
            bottom: offsetY + obstacle.height/2}

    box2 = {left: obstacle.positionX - rectWidth/2,
            right: obstacle.positionX + rectWidth/2,
            top: obstacle.positionY - rectHeight/2,
            bottom: obstacle.positionY + rectHeight/2}

    if((box1.right >= box2.left) &&
       (box1.left <= box2.right) &&
       (box1.bottom >= box2.top) &&
       (box1.top <= box2.bottom)) {
        return true
    }
    return false
}

function drawWorld(event) {
    const {offsetX, offsetY} = event
    const colorByCollision = (event, e) => chooseColor(checkCollision(event, e), e)
    const obstaclesWithCollision = obstacles.map(e => Object.assign(e, {color: colorByCollision(event, e)}))

    clearCanvas()
    fillBackground(palletColor[0])
    drawObstacles(obstaclesWithCollision)
    drawRect(offsetX, offsetY, rectWidth, rectHeight, pointerColor)
}
</script>

É dada pela seguinte verificação:

``` javascript
function checkCollision(b1, b2)
{
    if((b1.right >= b2.left) &&
       (b1.left <= b2.right) &&
       (b1.bottom >= b2.top) &&
       (b1.top <= b2.bottom)) {
        return true
    }
    return false
}
```