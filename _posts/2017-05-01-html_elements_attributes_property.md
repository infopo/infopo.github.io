---
layout: post
title: HTML - Elements / Attributes / Property
category: etc
---

## HTML Elements (tag라고 생각)
- usually consists of a start tag and end tag, with the content inserted in between
- [w3schools](http://www.w3schools.com/tags/){:target="_blank"}

```
<a></a>
<article></article>
<div></div>
<footer></footer>
<header></header>
<img></img>
<li></li>
<pre></pre>
<table></table>
<th></th>
<h1> to <h6>
```

---

## HTML Attributes

- [w3schools](http://www.w3schools.com/tags/ref_attributes.asp){:target="_blank"}

| Attribute | Belongs to | Description |
| --- | --- | --- |
| async       | \<script>                                                                                                                    | Specifies that the script is executed asynchronously (only for external scripts)     |
| charset     | \<meta>, \<script>                                                                                                            | Specifies the character encoding                                                     |
| class       | Global Attributes                                                                                                           | Specifies one or more classnames for an element (refers to a class in a style sheet) |
| color       | Not supported in HTML 5.                                                                                                    | Specifies the text color of an element. Use CSS instead                              |
| colspan     | \<td>, \<th>                                                                                                                  | Specifies the number of columns a table cell should span                             |
| datetime    | \<del>, \<ins>, \<time>                                                                                                        | Specifies the date and time                                                          |
| height      | \<canvas>, \<embed>, \<iframe>, \<img>, \<input>, \<object>, \<video>                                                              | Specifies the height of the element                                                  |
| headers     | \<td>, \<th>                                                                                                                  | Specifies one or more headers cells a cell is related to                             |
| href        | \<a>, \<area>,\<base>, \<link>                                                                                                 | Specifies the URL of the page the link goes to                                       |
| id          | Global Attributes                                                                                                           | Specifies a unique id for an element                                                 |
| name        | \<button>, \<fieldset>, \<form>, \<iframe>, \<input>, \<keygen>, \<map>, \<meta>, \<object>, \<output>, \<param>, \<select>, \<textarea> | Specifies the name                                                                   |
| onclick     | All visible elements.                                                                                                       | Script to be run when the element is being clicked                                   |
| onfocus     | All visible elements.                                                                                                       | Script to be run when the element gets focus                                         |
| onmouseover | All visible elements.                                                                                                       | Script to be run when a mouse pointer moves over an element                          |
| src         | \<audio>, \<embed>, \<iframe>, \<img>, \<input>, \<script>, \<source>, \<track>, \<video>                                            | Specifies the URL of the media file                                                  |
| style       | Global Attributes                                                                                                           | Specifies an inline CSS style for an element                                         |
| value       | \<button>, \<input>, \<li>, \<option>, \<meter>, \<progress>, \<param>                                                             | Specifies the value of the element                                                   |

```
<h1 id=””>
<footer id=””>
```

---

## Property
| | |
| --- | --- |
| element.id | Sets or returns the value of the id attribute of an element |

```
var x = document.getElementById("myAnchor").id;
```

---

## Methods
```
var x = document.getElementById("myAnchor").id;
```

