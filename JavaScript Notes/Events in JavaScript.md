## Events in JavaScript

Browser perfom honey wala koee bhi action jisko JavaScript listen kar sakta hey or uskay honey per koee code execute karta hey. 

There are three ways to add an event listner to an element but the most appropriate and recommended approach is using `addEventListner()` method.

```js
element.addEventListner('eventType', handlerFx(event), propogationType)
```

## Event Type

Kis tarah ka event hey, for example `click`,  `change`, `keydown`, and `load`

## Handler Function

Yeah woh code hota hey jo ham event k occure honey per execute karna chahatey heyn. Yeah aik callback function hota hey. 

JavaScript is function ko by default aik argument pass karta hey jisay event object kehtay heyn. Jo hamey event k barey mazeen information deyta hey.

## Propagation Type

Yeah aik `boolean` value hoti jo by default false hoti hey or is say ham yeah mention kartey hey k event <mark>child say parent ki tarf travel karna chaye</mark> (Event Bubbling) ya phir<mark> parent say child ki tarf travel karna chaye</mark> (Event Capturing)

<img title="" src="https://media.geeksforgeeks.org/wp-content/uploads/20250128215812380422/Event-bubbling-and-capturing.png" alt="Event-bubbling-and-capturing" width="391" data-align="center">

### Event Bubbling

Jab event child say parent ki tarf travel karta hey

```js
<style>
  body {
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  #parent {
    width: 300px;
    height: 300px;
    background-color: rgba(137, 43, 226, 0.242);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #child {
    width: 200px;
    height: 200px;
    background-color: blueviolet;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 25px;
    font-family: "Scribd Ja SN";
  }
</style>

<div id="parent">
  <div id="child">Child</div>
</div>

<script>
  const parent = document.querySelector("#parent");
  const child = document.querySelector("#child");

  child.addEventListener("click", (e) => {
    console.log("Child click hua!");
  });

  parent.addEventListener("click", (e) => {
    console.log("Parent click hua!");
  });
</script>
```

**Browser Console:-**

```js
> Child click hua!
> Parent click hua!
```

### ### How to stop Event Bubbling?

If you want to stop event bubblign and only want the event to be triggered on the target element (woh element jispay event occured howa hey)

```js
element.addEventListner('click', event => {
    event.stopPropagation()
})
```

### What si Event Capturing?

Ager app chahtey ho k event parent say child ki tarf travel karey to isay event capturing kehtay heyn. App isay allow kar saktey by setting the third parameter of `addEventListner()` method as `true`

```js
element.addEventListner('click', e => {...}, true);
```

Example:-

```js
<style>
  body {
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  #parent {
    width: 300px;
    height: 300px;
    background-color: rgba(137, 43, 226, 0.242);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #child {
    width: 200px;
    height: 200px;
    background-color: blueviolet;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 25px;
    font-family: "Scribd Ja SN";
  }
</style>

<div id="parent">
  <div id="child">Child</div>
</div>

<script>
  const parent = document.querySelector("#parent");
  const child = document.querySelector("#child");

  child.addEventListener(
    "click",
    (e) => {
      console.log("Child click hua!");
    },
    { capture: true }
  );

  parent.addEventListener(
    "click",
    (e) => {
      console.log("Parent click hua!");
    },
    true
  );
</script>
```

**Browser Console:-**

```js
> Parent click hua!
> Child click hua!
```

## What is `event.target.matches()`?

Event handler function k ander jab `event` object k zariye say milney waley target element k sath jab yeah method call kia jata hey to true retrun karta hey ager target element jispay evnet occure huwa hey uska CSS selector is funciton ko pass kiye huway CSS selector say match karta hey

**Parameter**

A valid CSS Selector like `.class`, `#id` etc.

**Output**

true, or false

```js
<div id="parent" style="background: lightblue; padding: 20px">
  Parent
  <button id="child">Child</button>
</div>

<script>
  const parent = document.querySelector("#parent");
  const child = document.querySelector("#child");

  parent.addEventListener("click", (e) => {
    if (e.target.matches("#child")) {
      console.log("Child click hua!");
    }
  });
</script>
```

## What is `event.preventDefault()`

`event.preventDefault()` kisi event ke **default browser behavior** ko **rok deta hai**.

```js
<form id="myForm">
  <input type="text" required>
  <button type="submit">Submit</button>
</form>

<script>
  document.getElementById('myForm').addEventListener('sub
mit', function(e) {
    e.preventDefault(); // stops form from reloading page
    alert('Form submission stopped!');
  });
</script>

```

**NOTE**

There is property of event object called `defaultPrevented` that let us know is the `preventDefault()` method is called on event object or not.

## Event Delegation

Event delegation ek technique hai jisme hum ek parent element par event listener lagate hain, aur uske child elements ke events ko handle karte hain — bina har child par alag listener lagaye.

[Learn Event Delegation In 10 Minutes - YouTube](https://youtu.be/cOoP8-NPLSo?si=bp_r5K_CptCXK4Bn)

## ClietnX and ClientY

Browser ki viewport k hisab say mouse pointer k X and Y coordinates ko retrun karta hey. Yani browser jisko ham client keh rahey heyn uski jo window hey uskay hisab say X and Y value of the position of the mouse pointer.

```js
<script>
  document.addEventListener("mousemove", (e) => {
    console.clear();
    console.log(`ClientX: ${e.clientX}`);
    console.log(`ClientY: ${e.clientY}`);
  });
</script>
```

This is an example of browser viewport.

<img title="" src="file:///C:/Users/mrasi/AppData/Roaming/marktext/images/2025-10-06-17-05-38-image.png" alt="" width="549" data-align="center">

## screenX and screenY

Yeah apkey computer ya laptop ki screen k hisaab jo mouse pointer k postion k X and Y coordinates ki value ko return karti heyn.

```js
<script>
  document.addEventListener("mousemove", (e) => {
    console.clear();
    console.log(`screenX: ${e.screenX}`);
    console.log(`screenY: ${e.screenY}`);
  });
</script>
```

<img title="" src="file:///C:/Users/mrasi/OneDrive/JavaScript%20Notes/diagram-export-06-10-2025-17_22_23.png" alt="diagram-export-06-10-2025-17_22_23.png" width="332" data-align="center">

## pageX and pageY

Yeah web page ki height or length k hisaab say mouse pointer k X and Y coordinate ki value ko deyta hey

```js

```


