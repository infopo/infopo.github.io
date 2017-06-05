---
layout: post
title: JavaScript and HTML DOM Reference
category: etc
---

- HTML DOM Reference
- DOM(Document Object Model)은 HTML 문서의 모든 요소에 접근하는 방법을 정의한 API다.



### 1. JavaScript Reference  

1. String  
   1. split()  
      1. string.split(separator, limit)
      2. separator &rarr; "" 혹은 " " 혹은 "," 혹은 "o" 혹은 ";"  
      3. limit는 나누고 싶은 횟수(넣지 않아도 됨)                
   2. replace()  
      1. var str = "Visit Microsoft!        
2. Number
3. Operators
4. Statements
5. Math
6. Date
7. Array
   1. push()
   2. `var fruits = ["Banana", "Orange", "Apple", "Mango"];`
   3. `fruits.push("Kiwi");`
   4. &rarr; Banana, Orange, Apple, Mango, Kiwi
8. Boolean
9. RegExp
   1. /pattern/modifiers;
   2. `var patt = /w3schools/i`
   3. Modifiers
   4. Brackets
      1. [abc]
      2. [0-9]
   5. Metacharacters
   6. Quantifiers
   7. RegExp Object Methods
      1. test()  
         - The test() method tests for a match in a string  
         - `var str = "The best thing in life are free";` 
         - `var patt = new RegExp("e");`  
         - `var res = patt.test(str);`  
         - adsfadf   
9. Global
9. Conversion
9. Output
   1. JavaScript does NOT have any built-in print or display functions.
   2. Writing into an alert box, using **window.alert()**.
   3. Writing into the HTML output using **document.write()**.
   4. Writing into the browser console, using **console.log()**.

### 2. Browser Objects Reference

- Window - The window object represents an open window in a browser.
   - Window Object Properties
   - Window Object Methods
       - alert()
       - alert("Hello! I am an alert box!!");
- Navigator
- Screen
- History
- Location
  
### 3. HTML DOM Reference
1. DOM Document — (Document는 HTML문서 전체를 대상으로 함)
   - cookie
      - returns all name/value pairs of cookies in the current document
      - `document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00; path=/";`
   - write()
     - Write some text directly to the HTML document
     - `document.write("Hello World!");`
2. DOM Elements — (Elements는 HTML문서 내의 Elements (eg. \<h1>, \<p> 등을 대상으로 함)
   - innerHTML
     - `document.getElementById("demo").innerHTML = "Paragraph changed!";`
     - The innerHTML property sets or returns the HTML content (inner HTML) of an element.
     - demo 내의 모든 속성들을 같이 가져온다
     - [링크](http://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_element_innerhtml){:target="_blank"}
   - id
     - `var x = document.getElementById("myAnchor").id;`
     - The id property returns the id of an element
3. DOM Attributes
4. DOM Events
   - onclick
     - HTML → `<element onclick="내가 선언한 함수()">`
     - element → h1 - h6, p, input 같은 object들
   - JavaScript → object.onclick=function(){내가 선언한 함수()};
   - onmouseover, onmouseout
     - HTML → `<element onmouseover="내가 선언한 함수()">`
     - JavaScript → object.onmouseover=function(){내가 선언한 함수()};
5. DOM Style

### 4. HTML Element Objects Reference (Tag)

1. article
2. div
3. script
   - `<script ATTRIBUTE=”VALUE”>`  
| ATTRIBUTE | VALUE                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------- |
| type      | - text/javascript (this is default)  - text/ecmascript  - application/ecmascript  - application/javascript  |
| charset   | charset                                                                                                 |
| src       | URL                                                                                                     |
4. input
   - `<input ATTRIBUTE=”VALUE”>`  
| ATTRIBUTE | VALUE                                                                                          |
| --------- | ---------------------------------------------------------------------------------------------- |
| type      | button, checkbox, color, date, datetime, email, file, image, number, password, text, time, url |
| align     | left, right, top, middle, bottom                                                               |
| src       | URL                                                                                            |
| value     | text                                                                                           |
| width     | pixels                                                                                         |
5. style
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
6. a
   - HTML \<a> 요소 (HTML 앵커 요소) 는 하이퍼링크를 정의합니다. 링크의 대상은 같은 페이지가 될 수도 있고, 웹의 어떤 다른 페이지도 될 수 있습니다. 
  - `<a id="myAnchor" href="http://www.w3schools.com">Tutorials</a>`
7. table 
   - table
   - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
8. tr
   - table row
   - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
9. td
   - table data
   - [attributes](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}
    
