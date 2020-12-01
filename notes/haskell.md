---
title: Haskell - By university of Glasgow
created: '2020-09-19T12:51:32.460Z'
modified: '2020-09-23T12:11:41.982Z'
---

# Haskell - By university of Glasgow

## Basics

* Expressions
  * Pure functional programming languages don’t have any statements — no assignments, no jumps.
  * Haskell has no statement, only expressions
  * `n = n + 1` is a equation, not assignment
* Functions
  ```hs
  hello name = "Hello, " ++ name
  ```
  * Lambda functions or anonymous functions

  ```hs
  f = \x y -> x*x + y*y
  ```

  * Function infix notation

  ```hs
    `92 `div` 10
  ````

* Types
  ```hs
  sq::Int->Int->Int
  sq x
  sq x y = x*x+y*y
  ```
* Lists
  ```hs
  l = ["apple", "banana"]
  ```

## Installing Haskell Compiler

### Installing Stack

```bash
curl -sSL https://get.haskellstack.org/ | sh
```

### Starting interacting session

```bash
stack ghci
```

```bash
:set prompt "ghci> "
```

### Load file in interactive session

```bash
:l baby-function.hs
:r
```

### Starting interacting session

```hs
:quit
```
