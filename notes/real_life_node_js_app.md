---
title: Real life node.js app
created: '2020-10-03T09:32:26.188Z'
modified: '2020-10-03T09:51:48.184Z'
---

# Real life node.js app

Reference: https://medium.com/swlh/node-js-app-in-the-real-world-what-they-never-really-tell-you-a-5-part-series-24a3225d9d9a

* A `domain model` where the business logic lives and with zero dependencies (to other librairies as well as to Node.js modules).
* A `thin app layer` with zero hard dependencies (except of course on the domain) and Dependencies Injection (DI) mechanism.
* An `infrastructure layer` containing all the implementation-specific code, notably data access.
* A `presentation layer` with an HTTP interface for the API and a Command Line Interface (CLI) app.
* Extra thin controllers with `dependency inversion principle`.
* Overall `Separation of Concerns` (SoC).
* `Single Responsibilty Principle` (SRP) as much as possible.
* 100% unit test coverage,
* `Dont Repeat Yourself` (DRY) code as much as possible,
* Keep It Simple, Stupid (`KISS`) principle as much as possible,
* Aiming at `open/closed principle` for classes (I will use mostly classes, more on this later), and more generally getting as close as possible from SOLID code and Inversion of Control (IoC).

## Events 
Events are only really needed, as a rule of thumb, when you can’t foresee how many side effects involving other services there will be. Or if they are too many of them (use your best judgement here, but keep in mind the two magic words : decoupling and simplicity).
