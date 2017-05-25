ES6

## Let-Const 
Hoisting --> move varbiable declartions to the top of the nearest
function and make them global at this level

```javascript
for (var i = 0; i < 10; i++) {
  console.log(i);
}
//this will treat i as a global vaiable

console.log('i after loop-->', i);

function ourFunction() {
  var j;
  //anything declared inside this block will only exist in this function
  // ex. j will exist inside for loops etc as well as outside
}
```

the more global state you have the more potential to cause probrlems
function Scope --> anything you declare will be scoped to the nearest function not to the nearest block


ES5 SOLUTION -- put into a function
```javascript
function counter (){
  for (var i = 0; i < 10; i++) {
    console.log(i);
  }
}
```
### LET
```javascript

  for (let j = 0; j < 10; j++) {
    console.log(j);
  }
  
  
```

### CONST
```javascript
  const express = require('express');
```
```javascript
  const x = 1;
  x=2;        //error on reassignment line
  console.log(x);
  
  
```
