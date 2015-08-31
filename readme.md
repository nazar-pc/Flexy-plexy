# Flexy-plexy
Ridiculously simple, incredibly powerful grid system

## Technology
Grid system is based on flex layout and implemented as SASS/SCSS mixin

## How this differs from other grid systems?
ENORMOUSLY!

Imagine, there is single mixin that allows you to do complex layouts with any number of columns of arbitrary size with different number of columns on each row. This is just a single line of code!

## It is responsive?
Absolutely

## Show me how it works!
Oh well)

Some markup:
```html
<div class="my-flex-container">
	<div>1</div>
	<div>2</div>
	<div>3</div>
	<div>4</div>
	<div>5</div>
	<div>6</div>
	<div>7</div>
	<div>8</div>
	<div>9</div>
	<div>10</div>
	<div>11</div>
	<div>12</div>
	<div>13</div>
	<div>14</div>
	<div>15</div>
</div>
```

A bit of SCSS:
```css
.my-flex-container {
	@include flexy-plexy(1em, 1 2 3, 1 1 1, 1, 2 2);

	@media (max-width: 1000px) {
		@include flexy-plexy(2em, 1 2, 1);
	}

	@media (max-width: 500px) {
		@include flexy-plexy(2em, 1 1, 1);
	}

	border : 1px solid red;

	> * {
		border : 1px solid blue;
	}
}
```

#### [Demo](https://nazar-pc.github.io/Flexy-plexy/)

### What we just did?
First, we've created general grid:
* with gutter `1em`
* first row with 3 columns that have ratio `1:2:3`, namely, first column will be 1/3 of last and twice as small as second
* second row with 3 columns of equal size
* third row with single column
* forth and any number of following rows with 1 columns of equal size (`2 2` is basically the same as `1 1`, columns are calculated relatively to each other)

Second, we've created responsive grid for at most `1000px`:
* gutter `2em`
* first row with two columns that have ratio `1:2`
* second and any number of following rows with width `100%`

Third - yes, responsive grid for at most `500px` width:
* gutter `2em`
* first row with 2 columns of `50%` width
* second and any number of following rows with width `100%`

And the last - borders so that you can see how it works visually.

### Rules
Well, you should already know how to use it, but here are some rules:
* first argument is gutter width
* any number of arguments starting from second are rows
* columns are represented as numbers separated by spaces
* column width is always calculated relatively to other columns, so `3 7` means that first column will have `30%` width and second `70%`, ratio `3:7`
* last row's rules will be applied to any more rows available
* you can use regular media queries to create responsive grid - just use mixin inside

## What else?
We love Web Components:) So `<template>` elements will not cause any issues if you use [Polymer](https://github.com/Polymer/polymer)'s `dom-if` or `dom-repeat`.

## Advanced
#### nth-child
In fact, first argument may contain not only gutter.
Usually Flexy-plexy generates CSS that uses `nth-of-type` selector, which means that you can use it with `<template>`, `<style>` and `<script>` elements inside without breaking markup.
However, this also means that you can use only one type of elements, namely, only `<div>` or only `<article>`, which is not always convenient.
For some cases you may want to use `nth-child` instead, just pass `child` keyword alongside with gutter:
```css
@include flexy-plexy(1em child, 1, 1 3 1, 1);
```

#### Hide columns
Well, setting width to 0 allows you to hide column completely:
```css
@include flexy-plexy(1em, 1 2 0 3, 2 2 2, 1, 2 2);
```
Third column in example above will be hidden completely and will not affect layout in any way.

## License
MIT, see license.txt
