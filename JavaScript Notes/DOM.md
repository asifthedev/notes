## DOM

DOM ka matlab hota hai **Document Object Model**.

Ye basically **HTML / XML document ka programming interface** hota hai jo JavaScript ko page ke elements ko **read, change, add aur delete** karne ki power deta hai.

Jab browser koi HTML page load karta hai, to woh us HTML ko ek **tree structure** me convert kar deta hai jise **DOM tree** kehte hain

## Element Selectors

### Select By ID

```html
<h1 id="heading">JavaScript with Chai aur Code</h1>
<p id="subtitle">Amazing playlist</p>
<script>
  const heading = document.getElementById("heading");
</script>
```

### Select By Class

```html
<h1 id="heading" class="title">JavaScript with Chai aur Code</h1>
<p class="subheading">Amazing playlist</p>
<script>
  const subheading = document.getElementsByClassName("subheading");
</script>
```

### querySelector()

`querySelector()` in JavaScript is a powerful method used to select and retrieve the first element that matches a specified CSS selector from the document.

Parameters:

- `selectors`: A string containing one or more valid CSS selectors.

**By ID.**

```js
const myElement = document.querySelector("#myId");
```

**By class.**

```js
const firstArticle = document.querySelector(".article");
```

**By Tag Name.**

```js
const firstDiv = document.querySelector("div");
```

**By Attribute.**

```
const autoplayElement = document.querySelector("[autoplay]");
```

### querySelectorAll()

Yeah woh sarey nodes ko return karta hey jo given selector say mathc kartey heyn unlike query selector jo sirf first matching node return karta tha

**Parameters**

A valid CSS selector.

**Return Type**

A nodelist.

```js
document.querySelectorAll("selector")
```

## Properties of Elements

Here, some properties and methods are directly accessible on DOM elements.

### id

Returns the value of the id attribute

```html
<h1 id="heading" class="title">JavaScript with Chai aur Code</h1>
<p class="subheading">Amazing playlist</p>
<script>
  const heading = document.getElementById("heading");
  console.log(heading.id); // heading
</script>
```

### className

Returns the value of the class attribute

```html
<h1 id="heading" class="title">JavaScript with Chai aur Code</h1>
<p class="subheading">Amazing playlist</p>
<script>
  const heading = document.getElementById("heading");
  console.log(heading.className);
</script>
```

## Methods of Elements

### getAttribute

**Parameters**

Name of the attribute in string

```html
<h1 id="heading" class="title">JavaScript with Chai aur Code</h1>
<p class="subheading">Amazing playlist</p>
<script>
  const heading = document.getElementById("heading");
  console.log(heading.getAttribute("class")); // title
</script>
```

**Return type**

Kisi bhi element k kisi bhi attribute ki value ko retrun karta hey

## setAttribute()

Kisi bhi attribute ki value set karney kelye use hota hey

**Parameters:** $attribute^1$, $value^2$

```js
> heading.setAttribute("class", "asif")
> heading
> <h1 id="heading" class="asif">JavaScript with Chai aur Code</h1>
```

## Styling with JavaScript

You can use the `style` property with any of the DOM elements, followed by a CSS styling property to apply CSS dynamically through JS.

```js
> heading
> <h1 id="heading" class="asif">JavaScript with Chai aur Code</h1>
> heading.style.color = "green"
```

**Output:-**

<img src="file:///C:/Users/mrasi/AppData/Roaming/marktext/images/2025-10-03-08-32-52-image.png" title="" alt="" width="622">

## Accessing Content and Values of Elements

### element.innerText

```js
> heading
> <h1 id="heading">JavaScript is <span style="display: none">
  amazing</span></h1>
> heading.innerText
> "JavaScript is"
```

### element.textContent

```js
> heading
> <h1 id="heading">JavaScript is <span style="display: none">
  amazing</span></h1>
> heading.textContent
> "JavaScript is amazing"
```

**Difference-:**

The difference between `innerText` and `textContent` is that `textContent` also returns the text of nested elements with having even if their CSS property  is `display: none`, as shown in the above code snippet, even though the display of the span element insdie the heading is none, but still its text is returned by the `textContent`# JavaScript with Chai aur Code

### innerHTML

As name refers, it retruns the text along with nested tag or HTML inside an element.

```js
> heading
> <h1 id="heading">I love <span id="objectName">JavaScript</span></h1>
> heading.innerHTML
> I love <span id="objectName">JavaScript</span>
```

## Convert Nodelist or HTML Collection into Array

You can use from method of array class and pass your Nodelist or HTML Collection

```js
Array.from()
```

## How to get all children of an element

**HTML**

```html
<div id="parent">
  <p class="day">Monday</p>
  <p class="day">Tuesday</p>
  <p class="day">Wensday</p>
  <p class="day">Thursday</p>
</div>
```

**Browser Console**

```js
> const parent = document.querySelector("#parent");
> parent.children
> HTMLCollection(4) [p.day, p.day, p.day, p.day]
```

### How to get first child of an element

```js
> const parent = document.querySelector("#parent");
> parent.firstElementChild
> <p class="day">Monday</p>
```

### How to get the last child of an element

```js
> parent.lastElementChild
> <p class="day">Thursday</p>
```

## How to get the next sibling of an element

ager app ko kisi bhi element ka usay exact agey wala sibling chaye to app:-

```js
> item2
> <li id="item2">Burgar</li>
> item2.nextElementSibling
> <li id="item3">Wrapper</li>
```

### How to get the previous sibling of an element

```js
> item2
> <li id="item2">Burgar</li>
> item2.previousElementSibling
> <li id="item1">Pizza</li>
```

### How to get the parent of an element

```js
> child
> <p class="day">Monday</p>
> child.parentNode
> <div id="parent">...</div>
```

## Creating new element

```js
<div id="parent"></div>

<script>
  // creating element
  const child = document.createElement("p");

  // setting the id attribute as day1
  child.setAttribute("id", "day1");

  // Efficient method of setting inner text
  const textNode = document.createTextNode("Monday");
  child.append(textNode);

  // Adding in the page for visibility 
  const parent = document.getElementByI\t");
  parent.appendChild(child);
</script>
```

## How to replace an element with a new one in the DOM

1. Select the element

2. Call replaceWith() on the selected element

3. Pass the new element as an argument

```js
<ul id="list">
  <li id="item1">Alo</li>
  <li id="item2">Gobhi</li>
  <li id="item3">Mttar</li>
</ul>

<script>
  const item3 = document.querySelector("#item3");

  const newItem = document.createElement("li");
  newItem.setAttribute("id", "item3");

  newItem.append(document.createTextNode("Tmater"));

  item3.replaceWith(newItem);
</script>
```

## How to remove an element from the DOM

1. Selecte the element

2. call the `remove()` function on it.

```js
element.remove()
```
