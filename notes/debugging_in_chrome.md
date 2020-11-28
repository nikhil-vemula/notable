---
title: debugging_in_chrome
created: '2020-11-28T09:08:40.853Z'
modified: '2020-11-28T09:16:01.043Z'
---

# Debugging in chrome

## $ and $$

`$` - querySelector  
`$$` - querySelectorAll  

```js
$('button') // document.querySelector("button")
$$('button') // document.querySelectorAll("button");
```

## Inspect

Print the dom of element to the console.

```js
inspect($('button'));
```

## Monitor and unmonitor

Monitor a when a function is triggered.

```js
monitor("<function_name>");
unmonitor("<function_name>");
```

## Keys and values

Print keys or values of an object.

```js
keys(myObj);
values(myObj);
```

## Table

Print a object in table format

```js
table(myObj);
```
