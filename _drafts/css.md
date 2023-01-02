---
layout: post
title: "CSS selectors"
subtitle: ""
comments: true
categories: "web-dev english"
---

# Definition

# Usage

# Use cases

## Only with multiple classes/<token>

```html
<div class="key1">Only key 1</div>
<div class="key2">Only key 2</div>
<div class="key1 key2"> Key 1 and Key 2</div>

<style>
.key1 .key2 {
    background-color: white;
}

.key1.key2 {
    background-color: gray;
}
</style>
```
## first-child
```html
<ul>
@  <li></li>
  <li></li>
  <li></li>
</ul>

```
```css
li:first-child
```

## Not

```html
<div>
@  <p></p>
  <p class="foo"></p>
@  <p></p>
@  <p></p>
</div>

```
```css
p:not(.foo)
```

## nth-child

```html
<ul>
  <li></li>
  <li></li>
@  <li></li>
  <li></li>
@  <li></li>
  <li></li>
@  <li></li>
</ul>

```
```css
li:nth-child(2n+3)
```
## all children of a div

```html
<div>
@  <span></span>
@  <p>
    <a></a>
    <span></span>
  </p>
</div>
```
```css
div > *
```

## sibling

```html
<div>
  <span></span>
@  <p>
    <a></a>
    <span></span>
  </p>
</div>
```
```css
span ~ p
```
## by atribute

```html
<div data-item="abc">
<div data-item="cde">
```

```css
[data-item]

[data-item~="abc"]
```