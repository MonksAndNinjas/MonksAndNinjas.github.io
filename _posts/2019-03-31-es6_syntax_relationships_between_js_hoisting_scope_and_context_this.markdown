---
layout: post
title:      "ES6 syntax relationships between JS hoisting, scope, and context ('this')"
date:       2019-03-31 20:47:53 +0000
permalink:  es6_syntax_relationships_between_js_hoisting_scope_and_context_this
---


This post is meant for someone who is just starting out with JavaScript and help clear up concepts such as hoisting, scope and this.

First some definitions:

**Hoisting:**   variable and function declarations are put into memory during the compile phase, but stay exactly where you typed them in the code. This allows you to use a function before you declare it in your code as shown in the example below.

```
catName("Chloe");

function catName(name) {
  console.log("My cat's name is " + name);
}
/*
The result of the code above is: "My cat's name is Chloe"
*/
```

Finally, JavaScript only hoists declarations, not initializations. If a variable is declared and initialized after using it, the value will be undefined as shown below.

```
console.log(num); // Returns undefined 
var num;
num = 6;
```

**Scope:**  In JavaScript there are two types of scope: Local scope and Global scope. JavaScript has function scope such that each function creates a new scope. Scope determines the accessibility of these variables. Variables defined inside a function are not accessible from outside the function.

Variables declared within a JavaScript function, become Local to the function. That is they can only be accessed from inside the function. 

```
// code here can NOT use carName

function myFunction() {
  var carName = "Volvo";

  // code here CAN use carName

}
```

A variable declared outside a function, becomes Global and so it has global scope. This means that all scripts and functions on a web page can access it. 

```
var carName = "Volvo";

// code here can use carName

function myFunction() {

  // code here can also use carName 

}
```

Finally, it's important to know that if you assign a value to a variable that has not been declared, it will automatically become a Global variable. Because of this behavior it is important to not create global variables unless intended. This can lead to problems such as overwriting window variables.

**This:**  In the context of JavaScript the keyword 'this' refers to the object it belongs to. It has different values depending on where it is used:
 
*  In a method, this is the owner object.
*  Alone, this refers to the global object.
*  In a function, this refers to the global object.
*  In a function, in strict mode, this is undefined.
*  In an event, this refers to the element that received the event.
*  Methods like call(),and apply()can refer this to any object.
 
Now that we understand scope, hoisting, and this let's look at some of their relationships.

**How do ES6 syntaxes such as `let` and `const` affect hoisting and scope, compared to `var`?**

JavaScript treats all variable declarations using "var" as if they are declared at the top of a functional scope or global scope regardless of where the actual declaration occurs. Basically, this is hoisting.

Here is an example in a functional scope:

```

function getShape(condition) {

    // shape exists here with a value of undefined
   
	 // OUTPUT : undefined
    console.log(shape);
   
	 if (condition) {
        var shape = "square";
        // some other code
        return shape;
    } else {
        // shape exists here with a value of undefined
        return false;
    }
}```

The if/else black don't create a local scope, therefore, shape is accessible everywhere outside the if block and within the function with an 'undefined' value.

Seeing the default behaviour of JavaScript compare this to 'let' and 'const'.

The syntax for let is similar to 'var', just replace 'var' with 'let' to declare a variable with its scope being only that code block. Place your 'let' declarations at the top in a block so they'll be available within that entire block.

```
function getShape(condition) {
// shape doesn't exist here
// console.log(shape); => ReferenceError: shape is not defined
if (condition) {
        let shape = "square";
        // some other code
        return shape;
    } else {
        // shape doesn't exist here as well
        return false;
    }
}
```

Shape exists only inside the if block, and throws an error when accessed outside of it instead of outputting undefined.

'const' declarations are similar to 'let' and 'var', lifecycle is the same as 'let' but some rules need to be followed.

Bindings declared using 'const' are treated as constants, and therefore they cannot be re-assigned values once defined. Due to this, every 'const' declaration must be initialized at the time of declaration, as show below.

```
// valid 
const shape = "triangle";
// syntax error: missing initialization
const color;
// TypeError: Assignment to constant variable
shape = "square"
```

You can modify an object's property, as shown below.

```
const shape = {
    name: "triangle",
    sides: 3
}
// WORKS
shape.name = "square";
shape.sides = 4;
// SyntaxError: Invalid shorthand property initializer
shape = {
    name: "hexagon",
    sides: 6
}
```

**How is `this` different in an arrow function compared to a function declared with the `function` keyword?**

In classic function expressions, the 'this' keyword is bound to different values depending on the context in which it is called. With arrow functions however, it uses 'this' from the code that contains the arrow function. For example, look at the setTimeout function below:

```
// ES5
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(function() {
      console.log(this.id);
    }.bind(this), 1000);
  }
};
```

In the ES5 example, .bind(this) is required to help pass the 'this' context into the function. Otherwise, by default 'this' would be 'undefined'.

```
// ES6
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(() => {
      console.log(this.id);
    }, 1000);
  }
};
```

ES6 arrow functions can't be bound to a 'this' keyword, so it will go up a scope, and use the value of 'this' in the scope in which it was defined.

**What is a closure in JavaScript?  Why is it useful?  Give an example.**

A closure is a feature in JavaScript where an inner function has access to the outer function's variables. Which is a scope chain.

The closure has three scope chains:

* it has access to its own scope -- variables defined between it's curly brackets
* it has access to the outer function's variables
* it has access to the global variables

To make things simpler, let's look at a simple closure:

```
function outer() {
   var b = 10;
   function inner() {
        
         var a = 20; 
         console.log(a+b);
    }
   return inner;
}
```

Two important things are happening here:

* an outer function 'outer'  which has a variable 'b', and returns the 'inner' function
* an inner function 'inner' which has its variable called a, and accesses an 'outer' variable 'b', within its function body

The scope of variable 'b' is limited to the 'outer' function, and the scope of variable 'a' is limited to the 'inner' function.

Let us now invoke the outer() function, and store the result of the outer() function in a variable 'X'. Let us then invoke the outer() function a second time and store it in variable 'Y'.

```

var X = outer(); //outer() invoked the first time
var Y = outer(); //outer() invoked the second time
```

Taking this one step at a time:

1. Variable 'b' is created, it's scope is limited to the outer() function, and its value is set to 10.
2. The next line is a function declaration so nothing to execute.
3. On the last line, 'return inner' looks for a variable called 'inner', finds that this variable 'inner' is actually a function, and so returns the entire body of the function 'inner'.
4. The contents returned by the return statement are stored in 'X'.
5. Function outer() finishes execution, and all variables within the scope of outer() now no longer exist.

Once a function completes its execution, any variables that were defined inside the function scope cease to exist. That means the lifespan of the variable is the lifespan of the function execution.

Thus, when outer() is invoked the second time:

1. A new variable 'b' is created, its scope is limited to the outer() function, and its value is set to 10
2. The next line is a function declaration, so nothing to execute
3. 'return inner' returns the entire body of the function 'inner'
4. The contents returned by the return statement are stored in 'Y'
5. Function outer() finishes execution, and all variables within the scope of outer() now no longer exist

So in both 'X' and 'Y' functions their variables only come into existence when the function is running, and cease to exist once the functions complete execution.

When X() or Y() are executed we are essentially executing the 'inner' function. When this happens two things occur:

1. Variable 'a' is created, and its value is set to 20
2. JavaScript now tries to execute 'a+b'. JavaScript knows that a exists since it just created it. But variable 'b' no longer exists since 'b' only exists while the outer() function is in execution. However, the outer() function finished execution long before we invoked X().

So how does JavaScript handle this?

The 'inner' function can access the variables of the enclosing function due to closures in JavaScript. Basically, the 'inner' function preserves the scope chain of the enclosing function at the time the enclosing function was executed, and thus can access the enclosing function's variables.

In our example, the 'inner' function had preserved the value of b=10 when the outer() function was executed, and continued to preserve (closure) it. Thus the 'inner' function has three scope chains as mentioned in the beginning.

Closure is the best tool in our toolbox for creating encapsulation.

It makes work with callbacks for asynchronous tasks simple. We use the variables we want, and they will be alive by the time the callback is called.
