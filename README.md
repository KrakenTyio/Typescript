# Typescript

## What is Typescript and why use it

### JS Pros.
- Dynamic typing
- Lack of modularity

### JS Cons.
- It`s everywhere
- Huge amount of libs
- Flexible

### TS
- Scalable
- Modular
- Easy learn
- Non-invasive (existing libs, broser support)
+ Superset for JavaScript
+ JS + Types = Typescript
+ Types are optinal
+ Compilation to native JS

### Types
- Object 				-> any
- void 				-> void
- boolean 				-> boolean
- integer, ling, short … 	-> number
- string, char 			-> string
- Type[] 				-> type[]

### Other
- Alliases
- Enum
- String literal
- typeof, instanceof, nullable

## Configuration and first run
require node.js
```sh
> npm install -g typescript
```
IDE:  	
- Visual Studio 2015 or newer, 
- Jetbrain Tools (WebStorm, PhpStorm, IntelliJ)
- Eclipse with plugin

define tsconfig.json
```sh
> mv burger.js burger.ts
> tsc burger.ts
```
## How Typescript extends JS and ES6
- Static types
- Live Error Check (Lint, Hint)
- Auto-completition
- Code Navigation
- Typed existed libs
- OOP
- Compilation to defined ECMAScript version
- Code readable
- Discovers the impact of change
- Productivity booster

## Basic for everyone
```js
// anybody can guess the value of 'msg'?
var msg = "The inning is: " + inning;
```
```js
var inning = {
    label: "Fifth",
    count: 5
}
```
```js
// still acceptable
var msg = "The inning is: " + inning;
```
```
"The inning is: [object Object]"
```

### Types
```js
// JavaScript
var isBatting = false;
var inning = 6;
var teamName = "Red Sox";
var runsRecord = [1,6,3];
```
```ts
// TypeScript
let isBatting: boolean = false;
var inning: number = 6;
const teamName: string = "Red Sox";
let runsRecord: number[] = [1,6,3];

let anotherArray: Array<number> = [1,2,3];
const value: string = <string>inning; 		// Type assertions
const value: string = inning as string;	// JSX as operator 
```
### Functions
```js
var pitch = function(effect) {
    if(effect == "fastball")
        return 170.5;
    else
        return 123.9; 
}
```
```ts
let pitch = function(effect: string) : number {
    if(effect == "fastball")
        return 170.5;
    else
        return 123.9; 
}
```
```ts
// Like a Boss:
const pitch: number = (effect: string) => effect == "fastball" ? 170.5 : 123.9; 
```
## Expert work with TS 
### Interface
```js
// looks strange...
function printLabel(labelledObj: {label: string}) {
  console.log(labelledObj.label);
}
var myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
```ts
// much better
interface LabelledValue {
  label: string;
}
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}
var myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
```ts
interface Shape {
    color: string;
}
interface Square extends Shape {
    sideLength: number;
}
```
### Module
```ts
export interface StringValidator {
    isAcceptable(s: string): boolean;
}


export const numberRegexp = /^[0-9]+$/;


export class ZipCodeValidator implements StringValidator {
    isAcceptable(s: string) {
        return s.length === 5 && numberRegexp.test(s);
    }
}


export { ZipCodeValidator as mainValidator };
```
```ts
import { ZipCodeValidator } from "./ZipCodeValidator";

let myValidator = new ZipCodeValidator();

export {mainValidator as Validator} from "./ZipCodeValidator";
```
### Generics
```ts
interface Burger {
	cheese: boolean;
}
interface ChickenBurger extends Burger {
	chinken: boolean;
}
```
```ts
function getBurger(type: any): any {
	return type;
}
```
```ts
function getBurger<T extends Burger>(type: T): T {
	return type;
}
```
```ts

// aioli: Object;
getBurger(aioli);	/// ??? ehm
// grange: Burger
getBurger(grange);	// OK
// chicken: ChickenBurger
getBurger<ChuckenBurger>(chicken);	// OK
```
### Decorators
Can be attached to a class declaration, method, accessor, property, or parameter.
```ts
function Params(param1: number) {
    return function(
        target: Function // The class the decorator
    ) {
        console.log(param1 + " called on: ", target);
 }
 ```
 ```ts
function Property(
    target: Object, // The prototype of the class
    propertyKey: string | symbol // The name of the property
    ) {
    console.log("called on: ", target, propertyKey);
}
```
```ts
@Params(1)
class ClassExample {
    @Property
    name: string;
...
```
#### Method Decorator
```ts
function MethodDecorator(
    target: Object, // The prototype of the class
    propertyKey: string, // The name of the method
    descriptor: TypedPropertyDescriptor<any>
    ) {
    console.log("called on: ", target, propertyKey, descriptor);
}
class MethodDecoratorExample {
    @MethodDecorator
    method() { }
}
```
```
called on:  { method: [Function] } method { value: [Function],
  writable: true,
  enumerable: true,
  configurable: true }
```
## Async-Await, RxJS what more?
### Async-Await
```ts
function delay(milliseconds: number, count: number): Promise<number> {
    return new Promise<number>(resolve => setTimeout(() => resolve(count), milliseconds));
}

async function dramaticWelcome(): Promise<void> { // async function always return a Promise
    console.log("Hello");
    for (let i = 0; i < 5; i++) {
        const count:number = await delay(500, i); // await is converting Promise<number> into number
        console.log(count);
    }
    console.log("World!");
}

dramaticWelcome();
```
### RxJS
```ts
var count = 0;
var rate = 1000;
var lastClick = Date.now() - rate;
var button = document.querySelector('button');
button.addEventListener('click', (event) => {
  if (Date.now() - lastClick >= rate) {
    count += event.clientX;
    console.log(count)
    lastClick = Date.now();
  }
});
```
```ts
var button = document.querySelector('button');
Rx.Observable.fromEvent(button, 'click')
  .throttleTime(1000)
  .map(event => event.clientX)
  .scan((count, clientX) => count + clientX, 0)
  .subscribe(count => console.log(count));
```
## @Types and externals JS Libs.
get from NuGet
or node.js
```sh
> npm install tsd -g
```
or with DefinitelyTyped
```sh
> npm install @types/{LIB}
```
```ts
// jquery.d.ts
interface JQuery {
	appendTo(..): …
	...
}
```
## TS vs Coffee vs Dart
### CoffeScript
- Also a compile-to-JS lang
- More syntactic sugar, 
- still dynamically typed
- JS is not valid CoffeeScript
- No spec
- Future: CS doesn`t track ES 6
### Dart
- Dart VM + stdlib (also compile-to-JS)
- Optinally typed
- Completely different syntax than JS
- JS interrop throught dart:js library
- ECMA Dart spec

## TS future...
### Cons.
- still need to know some JS how to and tips
- current compiler slower
- external module syntax not ES6-compatible

### Pros.
- hight value, low cost improvement over JavaScript
- Safer and more modular
- Solid path to ES6

