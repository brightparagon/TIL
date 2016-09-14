#Promise in Javascript

###What is it?
It's an assurance that we will get a result from an action in the future. When an async
function doesn't return a result for some reasons this promise will return a reason
for an error.

###Why need it?
In many cases in making async functions there is a problem due to the multiple calls of
these functions that include another async function. Even calling just one async function
can cause a problem like when the server couldn't return a result for some reasons.
In this case the async function wouldn't work as we built it.

Here comes the necessity of Promise. With this Promise we can define appropriate
reactions based on the results of our calls(success or fail), which leads to
more reliable structure of the program we make.

Further details about how to use this Promise in a project will be dealt with in another document.

This is also related to [$q service in AngularJS](https://docs.angularjs.org/api/ng/service/$q).

###Reference
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise

http://haroldrv.com/2015/02/understanding-angularjs-q-service-and-promises/

http://www.webdeveasy.com/javascript-promises-and-angularjs-q-service/
