#Function Declaration vs Expression

###What is a function in javascript?
It is 'First-Class-Object' that can include variables and functions like a class, also can be assigned to a variable, can be passed as a parameter to another function, can be made in runtime. It seems it acts like everything.

###What's the difference between function declaration and expression?
**Function Declaration**
It is also called function statement. It's literally declaration of a function. So, just by declaring a function doesn't do anything like returning something but being hoisted. Once a function is declared it is automatically hoisted to the root scope(top). So it can be reached anywhere like a global variable.

This is an example for this.
```javascript
// function declaration
function funDec() {
  console.log('I am Declaration!');
};
```
When we execute this code it does nothing because it is just declaration.

**Function Expression**
It is also called function literal. When this kind of codes are executed a returning value is assigned to some variables or just expressed(displayed). It does something unlike above.

There are several ways of function expression.
1. anonymous function expression
2. named function expression
3. self invoking function expression

This is an example for this.
```javascript
//anonymous function expression
var exp = function() {
    console.log('exp');
};

//named function expression
var exp = function foo() {
    console.log('exp');
};

// self invoking function expression
(function exp() {
    console.log('exp');
})();
```
The first and second way assign a function to the variable called exp. So, when executed the function itself is assigned to the variable. And then it is callable. But it is the same as function declaration in that it does not call a function.

But when the last one(self invoking) is executed it is called right away so we can see 'exp' in our monitor.

###Reference
[Blog](http://insanehong.kr/post/javascript-function/)

[Blog](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)

[Stack Overflow](http://stackoverflow.com/questions/1013385/what-is-the-difference-between-a-function-expression-vs-declaration-in-javascrip)
