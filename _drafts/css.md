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