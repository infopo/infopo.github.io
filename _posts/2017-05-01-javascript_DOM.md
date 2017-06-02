---
layout: post
title: JavaScript and HTML DOM Reference
category: etc
---

- HTML DOM Reference
- DOM(Document Object Model)은 HTML 문서의 모든 요소에 접근하는 방법을 정의한 API다.



### 1. JavaScript Reference  
1. String  
   - split()  
     + string.split(separator,limit)  
     + separator → “” 혹은 “ “ 혹은 “,” 혹은 “o”혹은 “;”  
     + limit은 나누고 싶은 횟수 (넣지 않아도 됨)  
   - replace()  
     + `var str = "Visit Microsoft!";`  
     + `var res = str.replace("Microsoft", "W3Schools");`  
     + `var str = "Mr Blue has a blue house and a blue car";`  
     + `var res = str.replace(/blue/g, "red");`  
     + Mr Blue has a red house and a red car
2. Number  
3. Operators  
4. Statements  
5. Math  
6. Date  
7. Array  
   - push()  
   - `var fruits = ["Banana", "Orange", "Apple", "Mango"];`
   - `fruits.push("Kiwi");`
   - → Banana,Orange,Apple,Mango,Kiwi
8. Boolean
9. RegExp
   - /pattern/modifiers;
   - var patt = /w3schools/i
   - Modifiers
   - Brackets
     + [abc]
     + [0-9]
   - Metacharacters
   - Quantifiers
   - RegExp Object Methods
     + test()
       ㄱ. The test() method tests for a match in a string.
       ㄴ. `var str = "The best things in life are free";`
       ㄷ. `var patt = new RegExp("e");`
       ㄹ. `var res = patt.test(str);`
10. Global
11. Conversion
12. Output
   - JavaScript does NOT have any built-in print or display functions.
   - Writing into an alert box, using window.alert().
   - Writing into the HTML output using document.write().
   - Writing into an HTML element, using innerHTML.
   - Writing into the browser console, using console.log().re

### 2. Browser Objects Reference
a. Window - The window object represents an open window in a browser.
  - Window Object Properties
  - Window Object Methods
    * alert()
      - alert("Hello! I am an alert box!!");
b. Navigator
c. Screen
d. History
e. Location
  
### 3. HTML DOM Reference
a. DOM Document — (Document는 HTML문서 전체를 대상으로 함)
  - cookie
    * returns all name/value pairs of cookies in the current document
    * `document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00; path=/";`
  - write()
    * Write some text directly to the HTML document
    * `document.write("Hello World!");`
b. DOM Elements — (Elements는 HTML문서 내의 Elements (eg. \<h1>, \<p> 등을 대상으로 함)
  - innerHTML
    * `document.getElementById("demo").innerHTML = "Paragraph changed!";`
      - The innerHTML property sets or returns the HTML content (inner HTML) of an element.
      - demo 내의 모든 속성들을 같이 가져온다
      - [링크](http://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_element_innerhtml){:target="_blank"}
  - id
    * `var x = document.getElementById("myAnchor").id;`
    * The id property returns the id of an element
c. DOM Attributes
d. DOM Events
  - onclick
    * HTML → `<element onclick="내가 선언한 함수()">`
      - element → h1 - h6, p, input 같은 object들
    * JavaScript → object.onclick=function(){내가 선언한 함수()};
  - onmouseover, onmouseout
    * HTML → `<element onmouseover="내가 선언한 함수()">`
    * JavaScript → object.onmouseover=function(){내가 선언한 함수()};
e. DOM Style

### 4. HTML Element Objects Reference (Tag)
a. article
b. div
c. script
  - `<script ATTRIBUTE=”VALUE”>`
| ATTRIBUTE | VALUE                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------- |
| type      | - text/javascript (this is default)  - text/ecmascript  - application/ecmascript  - application/javascript  |
| charset   | charset                                                                                                 |
| src       | URL                                                                                                     |
d. input
  - `<input ATTRIBUTE=”VALUE”>`
| ATTRIBUTE | VALUE                                                                                          |
| --------- | ---------------------------------------------------------------------------------------------- |
| type      | button, checkbox, color, date, datetime, email, file, image, number, password, text, time, url |
| align     | left, right, top, middle, bottom                                                               |
| src       | URL                                                                                            |
| value     | text                                                                                           |
| width     | pixels                                                                                         |
e. style
  - `document.getElementById("myH1").style.color = "red";`
  - `document.getElementById("myH1").style.PROPERTY = "VALUE";`
  - `var x = document.getElementsByTagName("STYLE");    // head의 style 부분에 선언한 것들 호출`
| PROPERTY        | VALUE                               |
| --------------- | ----------------------------------- |
| color           | red                                 |
| backgroundColor | gold                                |
| border          | 1px solid royalblue                 |
| fontWeight      | bold                                |
| cursor          | hand, wait, help, zoom-in, zoom-out |
f. a
  - HTML \<a> 요소 (HTML 앵커 요소) 는 하이퍼링크를 정의합니다. 링크의 대상은 같은 페이지가 될 수도 있고, 웹의 어떤 다른 페이지도 될 수 있습니다. 
  - `<a id="myAnchor" href="http://www.w3schools.com">Tutorials</a>`
g. table 
  - table
  - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
h. tr
  - table row
  - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
i. td
  - table data
  - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
    
