#What is atob() and btoa() in javascript?
Those are browser implementation.

* btoa() is a method of window object that encodes a string in base-64.
* It uses 'A-Z', 'a-z', '0-9', '+', '/', '=' to encode.
* Then atob() decodes a base-64 encoded string.

###Why named like that?

'a' stands for ASCII and 'b' for binary. It's for mnemonic purposes.

###How to use?

```javascript
let str = 'Hello there.';
let encoded = btoa(str);
let decoded = atob(encoded);
```

###Reference
https://www.w3schools.com/jsref/met_win_atob.asp

https://www.w3schools.com/jsref/met_win_btoa.asp

http://stackoverflow.com/questions/33854103/why-were-javascript-atob-and-btoa-named-like-that
