Is a programming language for web development and browser can run it directly. 
Browser will need a javascript engine to intepret and excute JS

# Javascript engines
1. Google Chrome: V8
2. Firefox: SpiderMonkey
3. Safari: JavaScriptCore
4. IE: Chakra

![[img/javascript-engine.jpeg]]

> Any JavaScript engine typically contains a call stack and a heap. The call stack is where the code is executed. The heap is an unstructured memory pool that stores all the objects needed for the application.


# Transpilers

> A transpiler takes ES2015+ source code and generates ES5 code that can run in every browser. 

Also generates source map files for debuggin ES2015+ source code.
=> In short term, transpilers transfer ES6 code to ES5 code so that every browser can run it.

Some notable tranpilers:
1. [Babel.js](https://babeljs.io/docs/)
2. [Typescript](https://code.visualstudio.com/docs)
3. [Traceur](https://github.com/google/traceur-compiler) (end of life)

# Variables
- **`var`:**
    - **Scope:** Function-scoped. A variable declared with `var` is accessible anywhere within the function it's defined in.
    - **Hoisting:** `var` declarations are "hoisted" to the top of their scope, but their assignment is not.
    - **Modern Usage:** Largely replaced by `let` and `const` to avoid common bugs related to its scoping rules.
- **`let`:**
    - **Scope:** Block-scoped.
    - **Hoisting:** `let` declarations are hoisted but are not initialized. Accessing them before the declaration results in a `ReferenceError`. This is known as the Temporal Dead Zone (TDZ).
    - **Reassignment:** You can reassign a value to a `let` variable.
- **`const`:**
	- Same as `let` in `scope` and `hoisting`
    - Difference from `let` is `const` can't be resassigned. However, `object` and arrays can have its content modified.

# Closures
## Scope
Javascript use **Lexical scoping**. Which mean, functions or variables of the inner scope can access functions & variables of parent scope.
```javascript
function utilityFunc() {
	let name = 'Vscode';
	function print() {
		console.log(name); // Print out "Vscode"
	}
}
utilityFunc().print();
```

## Closures
Combine function usage with lexical scope, we have closures. Closures can run even if the parent function returned.
```javascript
function countWithState() {
  let count = 0;
  return function() {
    console.log(++count);
  }
}

const counter = countWithState();
counter();// 1
counter();// 2
```
### Examples
1. [Debounce | JavaScript Interview Questions with Solutions](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/debounce)
2. 
### ### Common Uses of Closures
1. **Data Privacy/Encapsulation:** Closures let you emulate private variables.
2. **Function Factories:** You can use closures to create customized functions.
3. **Event Handlers/Callbacks:** They help maintain access to variables when dealing with asynchronous code.
4. **Functional programming**
5. **Memoization:** Closures can cache previous results.

More info: [How do JavaScript closures work? - Stack Overflow](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work?rq=2)
# Event loop
JavaScript is single-threaded. The Event Loop is the mechanism that allows JavaScript to handle asynchronous tasks (like fetching data or timers) without blocking the main thread.
- **Web APIs:** Where the browser handles background tasks like `setTimeout` or `fetch` asynchronously.
- **Callback Queue (TaskQueue):** After browser have finished the async operations, those callbacks will be moved here and waiting for the Call Stack to be empty.
- **Micro task Queue:** Callbacks from `promise`, `queueMicrotask()`, or `MutationObserver` will be moved here after browser finished the async operations. **Micro task queue** also waiting for the Call Stack to be empty to dequeue to Call Stack. But EventLoop will prioritize **Micro task Queue** more than **Callback Queue**
- **Call Stack:** Where function calls are executed (LIFO - Last-In, First-Out). Which is, most inner function is executed first.
![[img/Event loop.png]]

1. Js runtime will pop the call stack, execute one by one.
2. If there are tasks that use browser API, it will be moved to Web APIs list so it can be run asynchronously.
3. Tasks in Web APIs done running will be moved to the Callback queue or Micro task queue respectively depends on what type of callback comes from.
4. Event loop will move tasks from Callback queue to Call stack if stack is empty.