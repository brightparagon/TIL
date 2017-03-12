#window.onload
It is one of global event handlers. It fires after a entire page is loaded including
window, xmlhttprequest, scripts, css, images, etc.

###So what is it for?
It happens often that scripts in the head tag are loaded before HTML DOM and resources
like images. It possibly leads to incomplete rendering as developers intended it to be.
Here comes this window.onload making this right. Because it fires after all these
things are loaded, which makes all the necessary resources positioned in the right DOM.

###Example
Let's say we need to make an image modal which works when users click the image.

```html
<img id="myImg" src="..." alt="...">

<div id="myModal" class="modal">
  <span class="close">&times;</span>
  <img class="modal-content" id="img01">
  <div id="caption"></div>
</div>
```

Then we need scripts that make it working.
```javascript
let modal = document.getElementById('myModal');

let img = document.getElementById('myImg');
let modalImg = document.getElementById('img01');
let captionText = document.getElementById('caption');
img.onclick = function() {
  modal.style.display = "block";
  modalImg.src = this.src;
  captionText.innerHTML = this.alt;
};

let span = document.getElementsByClassName('close')[0];

span.onclick = function() {
  modal.style.display = "none";
};
```

Depending on the environment like browsers and network status it works fine and doesn't sometimes.
So, to make sure it works 100% as we wanted it to do, we need to put scripts in that window.onload like below.

```javascript
window.onload = function(){
  let modal = document.getElementById('myModal');

  let img = document.getElementById('myImg');
  let modalImg = document.getElementById('img01');
  let captionText = document.getElementById('caption');
  img.onclick = function() {
    modal.style.display = "block";
    modalImg.src = this.src;
    captionText.innerHTML = this.alt;
  };

  let span = document.getElementsByClassName('close')[0];

  span.onclick = function() {
    modal.style.display = "none";
  };
};
```

Then it should work as we think.

###Reference
https://developer.mozilla.org/ko/docs/Web/API/GlobalEventHandlers/onload

http://stackoverflow.com/questions/588040/window-onload-vs-document-onload

http://linuxism.tistory.com/271
