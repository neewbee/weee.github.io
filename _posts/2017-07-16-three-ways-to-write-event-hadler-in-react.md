---
layout:     post
title:      react 组件中this与参数传递
date:       2017-07-16 
summary:    六种写法及其优劣
categories: react this
---
{% gist 825fe97c5d65c495d0b495702c2a9737 %}

其中test6与test5经过babel编译后没有区别

```javascript

const test = () => {
    return this.method()
}

function(){
    console.log("take that")
}


```
