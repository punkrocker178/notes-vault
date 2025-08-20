# Regular function
> Regular functions create their own `this` context, which can change depending on how the function is called

## 1. Free function invocation (call function directly)
`this` in this case is default to global object (`window` in browser, `global` in Nodejs)
- non strict mode: `this` refers to `window`
- strict mode: `this` is `undefined` to prevent defaulting to global object
```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

greet(); // this is refers to window.name or undefined
```

## 2. Object function call
`this` is the same object that invokes the function.
In this case, `this` is `person`
```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

let person = {
	name: 'Hieu',
	sayHi: greet
}

person.sayHi(); // Hello, Hieu
```

## 3. Constructor function
When a function is instatiated by a `new` keyword, we have a new object that has `this` bound to it.
The context is same as [[#2. Object function call]]
```javascript
function Person(name) {
	this.name = name;
	this.sayHi = function () {
	  console.log(`Hello, ${this.name}`);
	}
}

const p = new Person('Hieu');
p.sayHi(); // Hello, Hieu
```
# Arrow function
Lexical scope. Inherit `this` context from surrounding scope.
Which means, arrow function will get the context from where it is created.
So it is not suitable to be defined as object methods.
=> Suitable as callback

```javascript
// ✔️ Valid use case
function greeting() {
  setTimeout(() => {
    console.log("Hello, " + this.name);
  }, 1000);
}

const person = {
  name: "Hieu",
  greet: greeting
};
person.greet() // Delayed 1s then "Hello, Hieu"

/*---------------------------------------------*/

// ❌ Invalid use case
const greeting = () => {
  console.log("Hello, " + this.name);
}

const person = {
  name: "Hieu",
  greet: greeting
};
person.greet() // greeting() is created in parent context. So it will inherit this from parent context. Which is undefined
```

# bind(), apply(), call()
These 3 prototype methods will set `this` explicitly

## 1. `bind()`
Create a new function that binds the context of the provided value to the new function.
### 1.1 Syntax
```javascript
bind(thisArg)
bind(thisArg, arg1, arg2, /* …, */ argN)
```

## 2. `apply()`
Call this function with a given `this` value, and `arguments` provided as an array
### 2.1 Syntax
```javascript
apply(thisArg)
apply(thisArg, argsArray)
```

## 3. `call()`
Same as `apply()` but pass arguments separately
### 3.1 Syntax
```javascript
call(thisArg) 
call(thisArg, arg1) 
call(thisArg, arg1, arg2, /* …, */ argN)
```

# Examples
1. [Debounce | JavaScript Interview Questions with Solutions](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/debounce)
2. [Throttle | JavaScript Interview Questions with Solutions](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/throttle)