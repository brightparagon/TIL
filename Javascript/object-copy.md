# Object Copy in JavaScript
It happens sometime to need a copy of a certain plain object. But it is easy to fail to get an object as we wanted it to be at first without knowing how the variable assignment(= operator) works in JavaScript especially when copying objects. The reason why I'm writing this one is also because I failed it..(!)

### Two ways to duplicate an object

# Shallow Copy
When copying an object shallowly, it only duplicates the address(reference) the original variable points to into the new variable.

So, in this case, it isn't right just to copy an object using '=' operator because making changes to the new variable affects directly the original object which is not what we want.

For example,
```javascript
let source = {
  a: 'a',
  b: 'b',
  c: 'c'
};

let target = source;

console.log(source);
/*
  a: 'a',
  b: 'b',
  c: 'c'
*/

target.a = 'b';
console.log(source);
/*
  a: 'b',
  b: 'b',
  c: 'c'
*/
```

# Deep Copy
This way duplicates everything including all the elements in an original object into the new variable. So, it is safe now to make any changes to the new object because this new object is a totally new one whose address is different from the original one. It doesn't have influence to the old one at all.

# Object.assign()
There is an useful function to copy objects: Object.assign(targetObject, sourceObject).

It gives us a whole new object only when copying an object with one depth because it copies the references of properties.

For example,
```javascript
let source = {
  a: 'a',
  b: 'b',
  c: 'c'
};

let target = Object.assign({}, source);

console.log(source);
/*
  a: 'a',
  b: 'b',
  c: 'c'
*/

target.a = 'b';
console.log(source);
/*
  a: 'a',
  b: 'b',
  c: 'c'
*/
console.log(target);
/*
  a: 'b',
  b: 'b',
  c: 'c'
*/
```
It is not enough to do deep copy using Object.assign() as I mentioned above. The alternative is to use JSON.parse(JSON.stringify()) like below.
```javascript
let source = {
  a: {
    a: 'a'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
};

let targetWithAssign = Object.assign({}, source);
let targetWithStringify = JSON.parse(JSON.stringify(source));

targetWithAssign.a.a = 'b';

console.log(source);
/*
  a: {
  	a: 'b'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
*/
console.log(targetWithAssign);
/*
  a: {
  	a: 'b'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
*/

source = {
  a: {
    a: 'a'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
};

console.log(source);
/*
  a: {
    a: 'a'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
*/

targetWithStringify.a.a = 'b';

console.log(source);
/*
  a: {
    a: 'a'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
*/
console.log(targetWithStringify);
/*
  a: {
  	a: 'b'
  },
  b: {
    b: 'b',
    c: 'c'
  },
  c: 'c'
*/

```

### Reference
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy
