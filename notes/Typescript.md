---
title: Typescript
created: '2020-08-28T16:27:57.387Z'
modified: '2020-09-06T18:35:19.628Z'
---

# Typescript

* Typescript is super script of javascript
* Will be compiled to the javascript to be able to run in the browser
* Does the type checking during compile time

## Why typescript ?

What happens if we pass two strings to this the below add function ?

```js
function add(a, b) {
  return a + b;
}
```

```js
function add(a:number, b:number) {
    return a + b;
}
```
* Support for types
* Next-gen javascript features
* Features like Interfaces and generics
* Meta programming features like decorators

## Running

```bash
tsc <filename>.ts
```

## Code setup

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Understanding typescript</title>
    <script src="app.js"defer></script>
</head>
<body>
    
</body>
</html>
```

`app.ts`

```js
console.log("Hello world");
```

`package.json`

```json
{
  "name": "typescript-learn",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "lite-server": "^2.5.4"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start" : "lite-server"
  },
  "author": "",
  "license": "ISC"
}
```

### Run

```bash
tsc app.ts
npm start
```

## Types

### Core types

* number
* string
* bool
* object
* array

  ```ts
  let arr: string[]
  ```

* tuples : order and length of array is fixed

  ```ts
  let role: [number, string] = [2, 'hello']
  ```
* enum

  ```ts
  enum state { COMPLETE='complete', PENDING='pending' }
  ```

* any

### Union types

* Where input can be one or more types

```ts
let v: number | string = 12;
```

### Literal types

```ts
let v: 'abc' | 'xyz' = "abc";
```

### Type alias

```ts
type combinable = number | string
```

### Function return types, void type and call backs

```ts
// Function return types
function add(a: number, b: number): number {
    return a + b;
}

function addPrint(a: number, b:number): void {
    console.log(a + b);
}

// Function type
const fun:  (x: number, y: number) => number = add;

function add(a: number, b: number): number {
    return a + b;
}

// Callbacks
function add(a: number, b: number, cb: (number) => void) {
    cb(a + b)
}

add(10, 20, (res) => {console.log(res)})
```

### Unknown and never type

```ts
// Unknown type
let user: unknown;

// Never type
function generatError(): never{
    throw new Error("Error message");
}
```

## Type script project and compiler

### Typescript project

Creates a tsconfig.json

```bash
tsc --init
```

### tsconfig.json

```json
"exclude": [
    "*.dev.js"
]
```

```json
"sourceMap" : true, // Generate source maps
"outDir" : "./dist",
"rootDir" : "./src",
"noEmitOnError" : true, // Do not generate js files on compilation error
```

### Watch mode

```bash
tsc -w
```

## Classes

```ts
class Department {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    describe(this: Department) {
        console.log("Description: " + this.name);
    }
}

const dep = new Department("Dep");
dep.describe();
```

### Public, private and protected

```ts
private employees: string[] = [];

// Short hand notation
constructor(public n: string, private id: string) {
}
```

### Readonly

```ts
// Read only
constructor(public n: string, private readOnly id: string) {
}
```

### Inheritance

```ts
class ITDepartment extends Department {

}
```

### Getters and setters

```ts
get id() {
  return this.GUID;
}
set id(name: string) {
  this.GUID = btoa(name);
}
```

### Static properties and methods

```ts
static fiscalYear = 2020;
static createEmployee(name: string) {
  return { name: name};
}
```

### Abstract classes and methods

```ts
abstract class Department {
  abstract describe(this: Department): void;
}
```

### Singleton class

```ts
class SingletonClass {
    private static instance;

    static getInstance() {
        if (SingletonClass.instance)
            return this.instance;
        this.instance = new SingletonClass();
        return this.instance;
        
    }

    private constructor() {}
}
```

### Interface

```ts
interface Greetable {
    greet(phrase: string): void;
}

class Person implements Greetable {
    greet(phrase: string): void {
        console.log(phrase);
    }
}
```

#### Interface as function types

```ts
interface AddFn {
    (a: number, b: number): number;
}

let add: AddFn;
add = (a: number, b: number) => {
    return a + b;
}
```

## Advanced Types

### Intersection types

```ts
type Admin = {
    name: string;
    privileges: string[];
}

type Employee = {
    name: string;
    startDate: Date;
}

type ElevatedEmployee = Admin & Employee;
```

### Type guards

```ts
if (typeof a === 'string') {
  //doSomething
}

if ('property' in someObject) {
  //doSomething
}

if (someObject instanceof someClass) {
  //doSomething
}
```

### Discrminated union

```ts
interface Bird  {
    type: 'bird';
    flyingSpeed: number;
}

interface Horse  {
    type: 'horse';
    runningSpeed: number;
}

type Animal = Bird | Horse;

function printSpeed(animal: Animal) {
    switch (animal.type) {
        case 'bird':
            console.log(animal.flyingSpeed);
            break;
        case 'horse':
            console.log(animal.runningSpeed);
            break;
    }
}
```

### Type casting

```ts
const inputElement = <HTMLInputElement>document.getElementId('user-input');
const inputElement = document.getElementId('user-input') as HTMLInputElement;

```

### Index properties

```ts
interface ErrorLogs {
    [prop: string]: string;
}
```

### Function overloads

```ts
type NumString = number | string;

function add(a: number, b:number): number;
function add(a: NumString, b: NumString) {
    if (typeof a === 'string' || typeof b === 'string') {
        return a.toString() + b.toString();
    }
    return a + b;
}
```

### Optional chaining

```ts
someKey?.someKey?.someKey
```

### Nullish coalescing

```ts
 notNull ?? 'default'
```

## Generics

They are template types in cpp.

```ts
// T and U can be anything
function mergeObjects<T, U>(a: T, b: U) {
}

mergeObjects<string, number>('a', 1)

// With Constraints
function mergeObjects<T extends Object, U extends Object>(a: T, b: U) {

}

// keyOf
function getValue<T extends object, U extends keyof T>(obj: T, key: U) {
    return obj[key]
}
```

### Generic classes

```ts
class DataStorage<T> {
    private data: T[] = [];

    addItem(item: T) {
        this.data.push(item);
    }
}

const textStorage = new DataStorage<string>();
textStorage.addItem('Nick');

```

## Utility types

### Partial

```ts
type Person = {
    name: string;
    age: number;
}

function createPerson(name:string) {
    let person: Partial<Person> = {};
    person.name = 'Nick';
    person.age = 23;
    return person;
}
```

### ReadOnly

```ts
const fruits: Readonly<string[]> = ['Apple'];
```

## Decorators

* A Decorator is a special kind of declaration that can be attached to a class declaration, method, accessor, property, or parameter. Decorators use the form @expression, where expression must evaluate to a function that will be called at runtime with information about the decorated declaration.
* Meta programming
* Runs when class is defined

### Class decorator

```ts
function Logger(constructor: Function) {
    console.log("Logging...");
    console.log(constructor);
}

@Logger
class Person {
    name:string;

    constructor(name: string) {
        this.name = name;
        console.log(name);
    }
}

const p = new Person('Nick')
```

### Decorator factory

```ts
function Logger(logString: string) {
    console.log(logString);
    return (constructor: Function) => {
        console.log("Logging...");
        console.log(constructor);
    }
}

@Logger('Class decorator')
class Person {
    name:string;

    constructor(name: string) {
        this.name = name;
        console.log("Constructor called...");
    }
}

const p = new Person('Nick')
```

### Property decorators

```ts
function Log(target: any, propertyName: string) {
    console.log(target);
    console.log(propertyName);
}
class Product {
    @Log
    private _price: number = 0;

    set price(price: number) {
        if (price > 0) {
            this._price = price;
        }
    }

    get price() {
        return this._price;
    }
}

```

### Access decorators

```ts
function Log(target: any, name: string, descriptor: PropertyDescriptor) {
    console.log(target);
    console.log(name);
    console.log(descriptor);
}
class Product {
    private _price: number = 0;

    @Log
    set price(price: number) {
        if (price > 0) {
            this._price = price;
        }
    }

    get price() {
        return this._price;
    }
}

```

### Method Decorator

```ts
function Log(target: any, name: string | Symbol, descriptor: PropertyDescriptor) {
    console.log(target);
    console.log(name);
    console.log(descriptor);
}
class Product {
    private _price: number = 0;

    set price(price: number) {
        if (price > 0) {
            this._price = price;
        }
    }

    get price() {
        return this._price;
    }
    @Log
    getPrice() {
        return this._price;
    }
}

```

### Parameter decorator

```ts
function Log(target: any, methodName: string | Symbol, position: Number) {
    console.log(target);
    console.log(methodName);
    console.log(position);
}
class Product {
    private _price: number = 0;

    set price(price: number) {
        if (price > 0) {
            this._price = price;
        }
    }

    get price() {
        return this._price;
    }

    getPriceWithTax( @Log tax: number) {
        return tax + this._price;
    }
}

```

