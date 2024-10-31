Is a programming language for web development and browser can run it directly. 
Browser will need a javascript engine to intepret and excute JS

# Javascript engines
1. Google Chrome: V8
2. Firefox: SpiderMonkey
3. Safari: JavaScriptCore
4. IE: Chakra

![[javascript-engine.jpeg]]

> Any JavaScript engine typically contains a call stack and a heap. The call stack is where the code is executed. The heap is an unstructured memory pool that stores all the objects needed for the application.


# Transpilers

> A transpiler takes ES2015+ source code and generates ES5 code that can run in every browser. 

Also generates source map files for debuggin ES2015+ source code.
=> In short term, transpilers transfer ES6 code to ES5 code so that every browser can run it.

Some notable tranpilers:
1. [Babel.js](https://babeljs.io/docs/)
2. [Typescript](https://code.visualstudio.com/docs)
3. [Traceur](https://github.com/google/traceur-compiler) (end of life)