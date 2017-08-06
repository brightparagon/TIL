# Meta tag
Meta tag is used for the definition of meta data of a web page. It includes character set(charset), keywords, description, author, etc. This meta data is helpful for search engines to find and evaluate a web page, which is called SEO(Search Engine Optimization).

### Character Set
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <p>안녕하세요!</p>
    <p>Hello!</p>
  </body>
</html>
```
Common values for charset are UTF-8 and ISO-8859-1. The former is character encoding for Unicode and the latter is character encoding for the Latin alphabet. But the UTF-8(Unicode) covers almost all of the characters symbols in the world.

### Keywords
```html
<meta name="keywords" content="Learn HTML TIL TODAY I LEARNED">
```
These keywords provide keywords about a web page.

### Refresh
```html
<meta http-equiv="refresh" content="60">
```
This meta tag refreshes a web page every one minute.

### Reference
http://poiemaweb.com/html5-tag-basic

https://www.w3schools.com/html/html_charset.asp

https://www.w3schools.com/tags/att_meta_charset.asp
