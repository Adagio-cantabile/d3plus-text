# d3plus-text

[![NPM Release](http://img.shields.io/npm/v/d3plus-text.svg?style=flat)](https://www.npmjs.org/package/d3plus-text) [![Build Status](https://travis-ci.org/d3plus/d3plus-text.svg?branch=master)](https://travis-ci.org/d3plus/d3plus-text) [![Dependency Status](http://img.shields.io/david/d3plus/d3plus-text.svg?style=flat)](https://david-dm.org/d3plus/d3plus-text) [![Gitter](https://img.shields.io/gitter/room/nwjs/nw.js.svg?style=flat)](https://gitter.im/d3plus/)

A smart SVG text box with line wrapping and automatic font size scaling.

## Installing

If you use NPM, run `npm install d3plus-text --save`. Otherwise, download the [latest release](https://github.com/d3plus/d3plus-text/releases/latest). The released bundle supports AMD, CommonJS, and vanilla environments. You can also load directly from [d3plus.org](https://d3plus.org):

```html
<script src="https://d3plus.org/js/d3plus-text.v0.9.full.min.js"></script>
```

[width]: 700
[height]: 75

## Getting Started

Without a doubt, the most commonly used aspect of this module is [textBox](https://github.com/d3plus/d3plus-text#textBox), which is used for intelligently wrapping SVG text. At it's core, you can simply pass along data points with "text" values and the generator will add them to the page using a set of defaults. Here is a data array containing 3 different sentences to be wrapped:

```js
var data = [
  {text: "Here is some sample text that has been wrapped using d3plus.textBox."},
  {text: "...and here is a second sentence!"},
  {text: "这是句3号。这也即使包装没有空格！"}
];
```

And finally, this is how that data array would be passed to the [textBox](https://github.com/d3plus/d3plus-text#textBox) generator.

```js
new d3plus.TextBox()
  .data(data)
  .fontSize(16)
  .width(200)
  .x(function(d, i) { return i * 250; })
  .render();
```

While [textBox](https://github.com/d3plus/d3plus-text#textBox) comes with some handy defaults, this example shows how any of the methods can be overridden with static values or accessor functions. For more information on how the [textSplit](#textSplit) function splits strings, specifically in languages that don't use spaces, check out [this blog post](https://blog.datawheel.us/english-is-not-chinese-69b43959bb47).

*Please note the `()` at the end of the chain of commands. This is what tells the [textBox](https://github.com/d3plus/d3plus-text#textBox) to finally render to the page, and allows setting multiple properties of the [textBox](https://github.com/d3plus/d3plus-text#textBox) without it trying to render after each one is set.*


[<kbd><img src="/example/getting-started.png" width="700px" /></kbd>](https://d3plus.org/examples/d3plus-text/getting-started/)

[Click here](https://d3plus.org/examples/d3plus-text/getting-started/) to view this example live on the web.


### More Examples

 * [Automatic Font Resizing to Fit Container](http://d3plus.org/examples/d3plus-text/resizing-text/)

## API Reference

##### Classes
* [TextBox](#TextBox)

##### Functions
* [fontExists](#fontExists) - Given either a single font-family or a list of fonts, returns the name of the first font that can be rendered, or `false` if none are installed on the user's machine.
* [stringify](#stringify) - Coerces value into a String.
* [strip](#strip) - Removes all non ASCII characters from a string.
* [textSplit](#textSplit) - Splits a given sentence into an array of words.
* [textWidth](#textWidth) - Given a text string, returns the predicted pixel width of the string when placed into DOM.
* [textWrap](#textWrap) - Based on the defined styles and dimensions, breaks a string into an array of strings for each line of text.
* [titleCase](#titleCase) - Capitalizes the first letter of each word in a phrase/sentence.
* [trim](#trim) - Cross-browser implementation of [trim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim).
* [trimLeft](#trimLeft) - Cross-browser implementation of [trimLeft](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/TrimLeft).
* [trimRight](#trimRight) - Cross-browser implementation of [trimRight](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/TrimRight).

---

<a name="TextBox"></a>
#### **TextBox** [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L11)


This is a global class, and extends all of the methods and functionality of <code>BaseClass</code>.


* [TextBox](#TextBox) ⇐ <code>BaseClass</code>
    * [new TextBox()](#new_TextBox_new)
    * [.render([*callback*])](#TextBox.render)
    * [.data([*data*])](#TextBox.data)
    * [.delay([*value*])](#TextBox.delay)
    * [.duration([*value*])](#TextBox.duration)
    * [.ellipsis([*value*])](#TextBox.ellipsis)
    * [.fontColor([*value*])](#TextBox.fontColor)
    * [.fontFamily([*value*])](#TextBox.fontFamily)
    * [.fontMax([*value*])](#TextBox.fontMax)
    * [.fontMin([*value*])](#TextBox.fontMin)
    * [.fontResize([*value*])](#TextBox.fontResize)
    * [.fontSize([*value*])](#TextBox.fontSize)
    * [.fontWeight([*value*])](#TextBox.fontWeight)
    * [.height([*value*])](#TextBox.height)
    * [.id([*value*])](#TextBox.id)
    * [.lineHeight([*value*])](#TextBox.lineHeight)
    * [.overflow([*value*])](#TextBox.overflow)
    * [.pointerEvents([*value*])](#TextBox.pointerEvents)
    * [.rotate([*value*])](#TextBox.rotate)
    * [.select([*selector*])](#TextBox.select)
    * [.split([*value*])](#TextBox.split)
    * [.text([*value*])](#TextBox.text)
    * [.textAnchor([*value*])](#TextBox.textAnchor)
    * [.verticalAlign([*value*])](#TextBox.verticalAlign)
    * [.width([*value*])](#TextBox.width)
    * [.x([*value*])](#TextBox.x)
    * [.y([*value*])](#TextBox.y)


<a name="new_TextBox_new" href="#new_TextBox_new">#</a> new **TextBox**()

Creates a wrapped text box for each point in an array of data. See [this example](https://d3plus.org/examples/d3plus-text/getting-started/) for help getting started using the textBox function.





<a name="TextBox.render" href="#TextBox.render">#</a> TextBox.**render**([*callback*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L58)

Renders the text boxes. If a *callback* is specified, it will be called once the shapes are done drawing.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.data" href="#TextBox.data">#</a> TextBox.**data**([*data*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L302)

If *data* is specified, sets the data array to the specified array and returns this generator. If *data* is not specified, returns the current data array. A text box will be drawn for each object in the array.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.delay" href="#TextBox.delay">#</a> TextBox.**delay**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L311)

If *value* is specified, sets the animation delay to the specified number and returns this generator. If *value* is not specified, returns the current animation delay.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.duration" href="#TextBox.duration">#</a> TextBox.**duration**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L320)

If *value* is specified, sets the animation duration to the specified number and returns this generator. If *value* is not specified, returns the current animation duration.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.ellipsis" href="#TextBox.ellipsis">#</a> TextBox.**ellipsis**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L333)

If *value* is specified, sets the ellipsis method to the specified function or string and returns this generator. If *value* is not specified, returns the current ellipsis method, which simply adds an ellipsis to the string by default.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d + "...";
}
```


<a name="TextBox.fontColor" href="#TextBox.fontColor">#</a> TextBox.**fontColor**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L342)

If *value* is specified, sets the font color accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current font color accessor, which is inferred from the [container element](#textBox.select) by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontFamily" href="#TextBox.fontFamily">#</a> TextBox.**fontFamily**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L351)

If *value* is specified, sets the font family accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current font family accessor, which is inferred from the [container element](#textBox.select) by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontMax" href="#TextBox.fontMax">#</a> TextBox.**fontMax**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L360)

If *value* is specified, sets the maximum font size accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current maximum font size accessor. The maximum font size is used when [resizing fonts](#textBox.fontResize) dynamically.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontMin" href="#TextBox.fontMin">#</a> TextBox.**fontMin**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L369)

If *value* is specified, sets the minimum font size accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current minimum font size accessor. The minimum font size is used when [resizing fonts](#textBox.fontResize) dynamically.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontResize" href="#TextBox.fontResize">#</a> TextBox.**fontResize**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L378)

If *value* is specified, sets the font resizing accessor to the specified function or boolean and returns this generator. If *value* is not specified, returns the current font resizing accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontSize" href="#TextBox.fontSize">#</a> TextBox.**fontSize**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L387)

If *value* is specified, sets the font size accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current font size accessor, which is inferred from the [container element](#textBox.select) by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.fontWeight" href="#TextBox.fontWeight">#</a> TextBox.**fontWeight**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L396)

If *value* is specified, sets the font weight accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current font weight accessor, which is inferred from the [container element](#textBox.select) by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.height" href="#TextBox.height">#</a> TextBox.**height**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L409)

If *value* is specified, sets the height accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current height accessor.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d.height || 200;
}
```


<a name="TextBox.id" href="#TextBox.id">#</a> TextBox.**id**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L422)

If *value* is specified, sets the id accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current id accessor.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d, i) {
  return d.id || i + "";
}
```


<a name="TextBox.lineHeight" href="#TextBox.lineHeight">#</a> TextBox.**lineHeight**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L431)

If *value* is specified, sets the line height accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current line height accessor, which is 1.1 times the [font size](#textBox.fontSize) by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.overflow" href="#TextBox.overflow">#</a> TextBox.**overflow**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L440)

If *value* is specified, sets the overflow accessor to the specified function or boolean and returns this generator. If *value* is not specified, returns the current overflow accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.pointerEvents" href="#TextBox.pointerEvents">#</a> TextBox.**pointerEvents**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L449)

If *value* is specified, sets the pointer-events accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current pointer-events accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.rotate" href="#TextBox.rotate">#</a> TextBox.**rotate**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L458)

If *value* is specified, sets the rotate accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current rotate accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.select" href="#TextBox.select">#</a> TextBox.**select**([*selector*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L467)

If *selector* is specified, sets the SVG container element to the specified d3 selector or DOM element and returns this generator. If *selector* is not specified, returns the current SVG container element, which adds an SVG element to the page by default.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.split" href="#TextBox.split">#</a> TextBox.**split**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L476)

If *value* is specified, sets the word split function to the specified function and returns this generator. If *value* is not specified, returns the current word split function.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.text" href="#TextBox.text">#</a> TextBox.**text**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L489)

If *value* is specified, sets the text accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current text accessor.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d.text;
}
```


<a name="TextBox.textAnchor" href="#TextBox.textAnchor">#</a> TextBox.**textAnchor**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L498)

If *value* is specified, sets the horizontal text anchor accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current horizontal text anchor accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.verticalAlign" href="#TextBox.verticalAlign">#</a> TextBox.**verticalAlign**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L507)

If *value* is specified, sets the vertical alignment accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current vertical alignment accessor.


This is a static method of [<code>TextBox</code>](#TextBox).


<a name="TextBox.width" href="#TextBox.width">#</a> TextBox.**width**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L520)

If *value* is specified, sets the width accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current width accessor.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d.width || 200;
}
```


<a name="TextBox.x" href="#TextBox.x">#</a> TextBox.**x**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L533)

If *value* is specified, sets the x accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current x accessor. The number returned should correspond to the left position of the textBox.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d.x || 0;
}
```


<a name="TextBox.y" href="#TextBox.y">#</a> TextBox.**y**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/TextBox.js#L546)

If *value* is specified, sets the y accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current y accessor. The number returned should correspond to the top position of the textBox.


This is a static method of [<code>TextBox</code>](#TextBox).
default accessor

```js
function(d) {
  return d.y || 0;
}
```

---

<a name="fontExists"></a>
#### d3plus.**fontExists**(font) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/fontExists.js#L10)

Given either a single font-family or a list of fonts, returns the name of the first font that can be rendered, or `false` if none are installed on the user's machine.


This is a global function.
**Returns**: <code>String</code> \| <code>Boolean</code> - Either the name of the first font that can be rendered, or `false` if none are installed on the user's machine.  

---

<a name="stringify"></a>
#### d3plus.**stringify**(value) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/stringify.js#L1)

Coerces value into a String.


This is a global function.

---

<a name="strip"></a>
#### d3plus.**strip**(value) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/strip.js#L18)

Removes all non ASCII characters from a string.


This is a global function.

---

<a name="textSplit"></a>
#### d3plus.**textSplit**(sentence) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textSplit.js#L50)

Splits a given sentence into an array of words.


This is a global function.

---

<a name="textWidth"></a>
#### d3plus.**textWidth**(text, [style]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWidth.js#L1)

Given a text string, returns the predicted pixel width of the string when placed into DOM.


This is a global function.

| Param | Type | Description |
| --- | --- | --- |
| text | <code>String</code> \| <code>Array</code> | Can be either a single string or an array of strings to analyze. |
| [style] | <code>Object</code> | An object of CSS font styles to apply. Accepts any of the valid [CSS font property](http://www.w3schools.com/cssref/pr_font_font.asp) values. |


---

<a name="textWrap"></a>
#### d3plus.**textWrap**() [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L6)

Based on the defined styles and dimensions, breaks a string into an array of strings for each line of text.


This is a global function.


* [textWrap()](#textWrap)
    * [.fontFamily([*value*])](#textWrap.fontFamily)
    * [.fontSize([*value*])](#textWrap.fontSize)
    * [.fontWeight([*value*])](#textWrap.fontWeight)
    * [.height([*value*])](#textWrap.height)
    * [.lineHeight([*value*])](#textWrap.lineHeight)
    * [.overflow([*value*])](#textWrap.overflow)
    * [.split([*value*])](#textWrap.split)
    * [.width([*value*])](#textWrap.width)


<a name="textWrap.fontFamily" href="#textWrap.fontFamily">#</a> d3plus..**fontFamily**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L86)

If *value* is specified, sets the font family accessor to the specified function or string and returns this generator. If *value* is not specified, returns the current font family.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.fontSize" href="#textWrap.fontSize">#</a> d3plus..**fontSize**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L95)

If *value* is specified, sets the font size accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current font size.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.fontWeight" href="#textWrap.fontWeight">#</a> d3plus..**fontWeight**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L104)

If *value* is specified, sets the font weight accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current font weight.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.height" href="#textWrap.height">#</a> d3plus..**height**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L113)

If *value* is specified, sets height limit to the specified value and returns this generator. If *value* is not specified, returns the current value.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.lineHeight" href="#textWrap.lineHeight">#</a> d3plus..**lineHeight**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L122)

If *value* is specified, sets the line height accessor to the specified function or number and returns this generator. If *value* is not specified, returns the current line height accessor, which is 1.1 times the [font size](#textWrap.fontSize) by default.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.overflow" href="#textWrap.overflow">#</a> d3plus..**overflow**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L131)

If *value* is specified, sets the overflow to the specified boolean and returns this generator. If *value* is not specified, returns the current overflow value.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.split" href="#textWrap.split">#</a> d3plus..**split**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L140)

If *value* is specified, sets the word split function to the specified function and returns this generator. If *value* is not specified, returns the current word split function.


This is a static method of [<code>textWrap</code>](#textWrap).


<a name="textWrap.width" href="#textWrap.width">#</a> d3plus..**width**([*value*]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/textWrap.js#L149)

If *value* is specified, sets width limit to the specified value and returns this generator. If *value* is not specified, returns the current value.


This is a static method of [<code>textWrap</code>](#textWrap).

---

<a name="titleCase"></a>
#### d3plus.**titleCase**(str, [opts]) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/titleCase.js#L5)

Capitalizes the first letter of each word in a phrase/sentence.


This is a global function.

| Param | Type | Description |
| --- | --- | --- |
| str | <code>String</code> | The string to apply the title case logic. |
| [opts] | <code>Object</code> | Optional parameters to apply. |
| [opts.lng] | <code>String</code> | The locale to use when looking up all lowercase or uppecase words. |


---

<a name="trim"></a>
#### d3plus.**trim**(str) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/trim.js#L1)

Cross-browser implementation of [trim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim).


This is a global function.

---

<a name="trimLeft"></a>
#### d3plus.**trimLeft**(str) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/trim.js#L10)

Cross-browser implementation of [trimLeft](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/TrimLeft).


This is a global function.

---

<a name="trimRight"></a>
#### d3plus.**trimRight**(str) [<>](https://github.com/d3plus/d3plus-text/blob/master/src/trim.js#L19)

Cross-browser implementation of [trimRight](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/TrimRight).


This is a global function.

---



###### <sub>Documentation generated on Fri, 21 Jul 2017 22:48:30 GMT</sub>
