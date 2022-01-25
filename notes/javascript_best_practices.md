---
title: Javascript Best Practices
created: '2020-09-11T14:22:39.680Z'
modified: '2020-09-11T14:35:10.495Z'
---

# Javascript Best Practices

## Write Simple Code

### Instead of this

```js
var doubleList = list => {
  const newList = [];
  for (var i=0; i < list.length; i++) {
    newList[i] = list[i] * 2;
  }
  return newList;
}
```

### Write this

```js
const doubleList = list.map(x => x *2);
```

## Linear Code

### Instead of this

```js
if (title) {
  // doSomething with title
} else {
  return "Title is needed"
}
```

### Write this

```js
if (!title) return "Title is needed"
// doSomething with title
```

## Better naming conventions

### Instead of this

```js
let isNotActive;
let doesNotHaveAddress;
```

### Write this

```js
let isActive; // !isActive
let hasAddress; // !hasAddress
```

## Template

### Instead of this

```js
```

### Write this

```js
```
