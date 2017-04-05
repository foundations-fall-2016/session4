# Definition List Styling

[Here is a summary](http://www.w3schools.com/html/html_lists.asp) of the different types of lists in HTML. And [an article](http://maxdesign.com.au/articles/definition/) specifically on definition lists.

Examine the html in the browser. 

<!-- Note the use of `class="image"` on the `<dd>` elements containing image.  -->

Review the default browser formatting for definition lists using the developer tools.

## The CSS
Create a new `css` folder, create a new empty file within it and add the following CSS code.

```
* {
	margin:0; 
	padding:0;
}

body {
	font-family: Arial, Helvetica, sans-serif;
	margin: 1em;
	font-size: 100%;
}

.menu-list {
	width:300px; 
	border:2px solid #c8cdd2;
	padding:10px 0;
} 
```

And save it as styles.css into the new folder. Use `<link>` to add a reference to this file in the head of the html document and test in the browser.

Note the 300 pixel width and the 10px padding top and bottom.

```
.menu-list dl {
	margin:10px 20px; 
}
```

Note the margins above. We apply left and right margins to the dl. If we were to add 20px padding to the menu-list it would increase the width of the element to 344px which, let's let's pretent for a moment, is not desirable. 

Let's tackle the definition terms `<dt>`.

```css
.menu-list dt {
	letter-spacing: 1px; 
	color: #627081; 
}
```

Now apply some basic formatting to the definitions.

```css
.menu-list dd {
	font-size: 0.875em;
	line-height: 1.6; 
	color: #666; 
}
```

###The Floats

Allow the text to position itself next to image.

```css
.menu-list img {
	float:left;
}
```

The layout appears to break. Let's tackle this one element at a time.
Float the title `<td>` to the opposite side.

```css
.menu-list dt {
	float: right;
	...
}
```

The descriptive text fills a gap between the `<dt>` and the image, assigning widths to each will fix this.

Let's add `width:180px` to the dt using the following calculations. 

Width of box (300px) minus margins around each dl (20px * 2) minus the width of image (80px)

```css
.menu-list dt {
  ...
	width: 180px;
}
```

Now the images are sticking outside their parent `<dl>` container. We want the containing element to expand to encompass its contents.

We can use the same method we have already used - FNE float nearly everything (See Eric Meyer's old yet still [relevant article](http://bit.ly/GQD5MU) wherein it is written "a container will stretch to fit around floated elements within it if the container is also floated.")

```css`
.menu-list dl {
	...
	float:left;
    }
```

Note the entries are exactly the width of the `<dt>`s. 

Assign a width for floated elements. (260 + 20 + 20 = 300, the same width as the menu-list.)

```css
.menu-list dl {
	...
	width: 260px; 
}
```

Now the only thing that's collapsed is the menu-list container.￼

Float the menu-list container the prevent collapsing.

```css
.menu-list {
	float:left;
	...
}
```

After reviewing the final.png design we can see we need to add borders and space to the right of the image with a margin.

```css
.menu-list img {
	...
	margin: 0 8px 0 0;
	padding: 4px;
	border: 1px solid #d9e0e6;
	border-bottom-color: #c8cdd2;
	border-right-color: #c8cdd2;
	background: #fff;
	}
```

The layout breaks. The problem is with the `<dt>`'s widths. 

Change the spacing for the `<dt>`s by subtracting 18px. 

180px minus 18 (8px right margin + 4px padding * 2 + 1px border * 2)

```css
.menu-list dt {
	width:162px;
	...
}
```

Add additional text (in Sublime: `command-shift p / lorem` or `lorem + tab`) to the first dt to examine the behavior when text wraps.

To prevent text from wrapping under the images add a left margin of 98px to the second `<dd>` element.

Let's use a [sibling selector](https://css-tricks.com/child-and-sibling-selectors/).

```css
.menu-list dd + dd {
	margin: 0 0 0 98px; 
}
```


### Changing the float direction 

In the final image the design intention was to alternate the image and text.

We can use the CSS nth-child selector. This method allows us to target the html without adding classes for the sole purpose of controlling the view.

The following selector would target the second `<dl>` element.

`dl:nth-child(2)`

```
.menu-list dl:nth-child(even) dt {
	float:left; 
}

.menu-list dl:nth-child(even) img {
	float:right;
	margin: 0 0 0 8px; 
}

.menu-list dl:nth-child(even) dd + dd {
	margin: 0 98px 0 0; 
}
```

For more information on nth-child read [this article](https://css-tricks.com/how-nth-child-works/) on CSS Tricks.

### Finishing Touches

Set the background image (304px wide plus a 2px border on both sides) and remove the border.

```css
.menu-list {
	...
	/* border:2px solid #c8cdd2; */
	width:304px; 
	background: url(../img/bg.gif) no-repeat top left;
}
```

Add drop shadow to images

`box-shadow: 1px 1px 2px #aaa;`

Or use rgb

`box-shadow: 1px 1px 3px rgb(200, 200, 200);`

Or use rgba.

`box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);`

### Replacing the bg Image

```
border-image:
      linear-gradient(to bottom, black, rgba(0, 0, 0, 0)) 1 100%;
```

Removing the background image and replacing it with CSS is difficult here but worthwhile since it allows us to use the component at any width and height we need.

Note the use of border-image below:

```
.menu-list {
	padding:10px 0;
	float:left;
	width:304px; 
	border-width: 4px 4px 0 4px;
    border-left-style: solid;
    border-right-style: solid;
	border-image: linear-gradient(to bottom, rgb(200, 205, 210), rgba(0, 0, 0, 0)) 1 100%;
    background: linear-gradient(to bottom, rgba(200, 205, 210,1) 0%, rgba(200, 205, 210,1) 1%, rgba(240,240,240,0.4) 1.5%, rgba(240,240,240,0) 100%);
}
```

See [this article](https://css-tricks.com/examples/GradientBorder/) for more examples of fancy border effects (the vendor prefixes - `-webkit-` etc.` - are not really necessary at this point).



## Box Model - Border Box

Working with the alternate box model in version-2-fluid.

This is a simplified version of the first exercise. Examine the html and css.

Remove the width rule from the menu-list and note its size. Add `width: 100%`.

```css
.menu-list {
	...
	/*width: 300px;*/
	width: 100%;
}
```

Note the horizontal scroll bar.

Initialize border-box on all elements:

```css
* {
	...
	box-sizing: border-box;
}
```

No scrolling.

```css
.menu-list dl {
	...
	width: calc(100% - 20px);
}
```

```css
.menu-list dt {
	...
	width: calc(100% - 98px);
}
```


## Responsive Design - Just the Basics

### Media Query

* print

```css
@media print {
	img {
		display: none;
	}
}
```

* screen

Use the width of the browser to change the view.

```css
@media screen and (min-width: 304px){
	.menu-list {
		background: #eee;
		color: #000; 
	}
}
@media screen and (min-width: 620px){
	.menu-list {
		background: #333;
		color: #fff;
	}
}
```

### The meta tag

Use Chrome's toggle device toolbar feature and choose a device.

Note the absence of scaling.

Add the [viewport meta](http://www.w3schools.com/Css/css_rwd_viewport.asp) tag to the head region of the html page and refresh:

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`


