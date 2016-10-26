#FOUNDATIONS session 4

##Basilica

Examine code with regards to the [recipe schema](https://schema.org/Recipe) at [schema.org](http://schema.org/docs/gs.html). Here is an [example](http://www.foodnetwork.com/recipes/food-network-kitchens/basil-pesto-recipe2.html).

Note the `<abbr>` tag and the absence of a wrapper div (even though the design shows a centered document). The document contains 2 script tags. Examine the page n the browser's dev tools. NOte the console message and the classes applied to the html tag.

```css
* { 
    margin:0; 
    padding:0; 
}
body { 
   font: 100%/1.5 "Lucida Grande", "Lucida Sans Unicode", Verdana, sans-serif; 
   color : #333;
   max-width: 840px;
   margin: 0 auto;
   margin-top: 24px;
} 
article {
	float: left;
	width : 50%;
	padding : 16px;
}

aside { 
	float : left;
	width : 50%;
	padding : 16px; 
}
```
Note the footer. Because both columns have been floated it can wrap.

```css
footer {
    clear: both;
}
```

Faux columns

```css
.content { 
  background : url(img/html.png) repeat-y 50% 50%;
}
```
Note that we cannot see the background image. The content div has collapsed because its direct children have been floated. We have looked at a number of methods that can be used to prevent collapsing. E.g.:

```css
.content { 
  background : url(img/html.png) repeat-y 50% 50%;
  float: left;
}
```

Here we will use the clear fix method. 

```css
.content:after { 
	content:"."; 
	display:block; 
	height:0; 
	clear:both; 
	visibility:hidden; 
}
```

The method uses `:after` to insert a character after the div and then sets it to `display: block` and `clear: both` to prevent collapsing.

Since box collapsing is rather common let's create a generic class that we can use elsewhere.

Change the selector and updated the method to something shorter and more modern:

```css
.cf:before,
.cf:after {
    content: " ";
    display: table;
}

.cf:after {
    clear: both;
}
```

Add the cf class to the content div.

We'll return to the :before and :after pseudo-classes later.

##The Branding Header

Add the green background to the branding div.

```css
header {
	position : relative;
	height : 120px;
	background :#88a308;
	border-radius: 8px 8px 0px 0px;
}
```

Add absolute / relative positioning and create a viewable area for the image. (Note: we can get the image dimensions via the inspector.) 

`@import url(futura/stylesheet.css);`

```css
header h1 { 
	position : absolute; 
	top: -80px; 
	left:-100px;
	z-index: 90;
	padding-left: 260px;
	padding-top: 90px;
	background: url(img/basil.png) no-repeat;
	font-family: FuturaStdLight, sans-serif; 
	font-weight: normal;
	color:#fff;
	font-size: 5rem;
}
```


```css
header h1 {
    transform: translateY(-80px) translateX(-100px);
	padding-left: 260px;
	padding-top: 90px;
	background: url(img/basil.png) no-repeat;
	font-family: FuturaStdLight, sans-serif; 
	font-weight: normal;
	color:#fff;
	font-size: 5rem;
}
```

Note:

```html
<header>
	<h1>Basilica!</h1>
	<a class="beta" href="#">Beta</a>
</header>
```

Note the current position of the beta link.

```css
header h1 {
    ...
    float: left;
}
```

Allows the beta to situate itself but may effect other elements of the page.

```css
header a.beta {
	background: url("img/beta.png") no-repeat;
    color:#fff;
    font-size: 1.5rem;
	position: absolute; 
	z-index: 300;
	top:-20px;
    right:-10px;
	width:85px;
	height:85px;
    line-height:85px;
	text-align:center;
	text-transform: uppercase;
}
```

```css
header a.beta:hover {
	transform: rotate(0deg) scale(1.2);
}
```


```css
header a.beta {
	...
	transition: all 1s ease;
}
```

Note: the absolute positioning on the beta link is creating a horizontal scrollbar. 

Change to `right: 10px;`.

##Mobile First Approach

Analysis in the device view indicates a horizontal scroll due to a combination of settings. Comment out the offenders:

```css
header h1 {
    /*transform: translateY(-80px) translateX(-100px);
	padding-left: 260px;
	padding-top: 90px;*/
	background: url(img/basil.png) no-repeat;
	font-family: FuturaStdLight, sans-serif; 
	font-weight: normal;
	color:#fff;
	/*font-size: 5rem;*/
}
```


```css
/*article {
    float: left;
    width : 50%;
    padding : 16px;
}

aside { 
    float : left;
    width : 50%;
    padding : 16px; 
}*/
```


```css
.content {}

.content {}

article, aside {
    box-sizing: border-box;
    padding: 1rem;
}

@media only screen and (min-width: 768px) {
    header {
        height: 120px;
    }
    .content {
        background: url('img/html.png') repeat-y 50% 50%;
    }
    article {
        float: left;
        width: 50%;
    }
    aside {
        float: left;
        width: 50%;
    }
}
```

Branding

```css

header {
    ...
    height: 80px;
}

header h1 {
    transform: translateY(10px) translateX(30px);
    font-family: FuturaStdLight, sans-serif;
    font-weight: normal;
    color: #fff;
    font-size: 3rem;
}

```

Large screen

```css
@media only screen and (min-width: 768px) {

	...

	header {
        height: 120px;
    }

    header h1 {
        transform: translateY(-80px) translateX(-100px);
        padding-left: 260px;
        padding-top: 90px;
        background: url(img/basil.png) no-repeat;
        font-family: FuturaStdLight, sans-serif;
        font-weight: normal;
        color: #fff;
        font-size: 5rem;
    }
}


##Navigation

```css

nav {
    background: #e4e1d1;
    border-top: 0.5rem solid #ebbd4e;
    padding: 0.5rem 1rem;
}

nav li {
    float: left;
    list-style: none;
    margin-right: 0.5rem;
}

nav a {
    text-align: center;
    font-size: 1.5rem;
    padding: 8px;
    color: #fff;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
}
```

Use Modernizr

```css
.cssgradients .nav-storeit a {
    background: linear-gradient(to bottom, #dfa910 0%, #fcde41 100%);
    border-radius: 6px;
}

.cssgradients .nav-storeit a:hover {
    background: linear-gradient(to bottom, #fcde41 1%, #dfa910 99%);
}

.cssgradients .nav-pickit a {
    background: linear-gradient(to bottom, #ABC841 0%, #6B861E 100%);
    border-radius: 6px;
}

.cssgradients .nav-pickit a:hover {
    background: linear-gradient(to bottom, #6B861E 1%, #ABC841 99%);
}

.cssgradients .nav-cookit a {
    background: linear-gradient(to bottom, #6F89C7 0%, #344E8B 100%);
    border-radius: 6px;
}

.cssgradients .nav-cookit a:hover {
    background: linear-gradient(to bottom, #344E8B 1%, #6F89C7 99%);
}
```
Flexbox

```css
nav {
    background: #e4e1d1;
    border-top: 0.5rem solid #ebbd4e;
    padding: 0.5rem;
    display: flex;
    align-items: center;
}

nav ul {
    display: flex;
}

nav li {
    /*float: left;*/
    list-style: none;
    margin-right: 0.5rem;
}

nav p {
    margin-right: auto;
}

```

Format Content

```css
h2, h3 {
    color: #88a308;
    margin: 8px 0;
    font-size: 1.4rem;
    letter-spacing: -1px;
}

a {
    color: #f90;
    text-decoration: none;
    transition: color 0.5s linear;
}
li > h4 {
    margin-top: 12px;
}
aside li {
    list-style: none;
}
article li, article ol {
    margin-left: 1rem;
    margin-bottom: 0.5rem;
}
```

Animate Links

```css
.content a:hover {
    color: #88a308;
    transition-property: color;
    transition-duration: 1s;
    transition-timing-function: linear;
}
```
or `transition: color 0.2s linear;`


Footer

```css
footer {
    clear: both;
    background: #88A308;
    border-radius: 0 0 8px 8px;
    padding: 40px 10px 10px 1rem;
    text-align: right;
}
```

##Homework

1. Create a small screen version of the page using media queries and a new breakpoint for smaller screens (540px). Pay attention to the header in portrait mode. Try re-implementing the basil image as a branding element.

##NOTES

###Flex xolumns

```css
@media only screen and (min-width: 768px) {
    ...
    .content {
        background: url('img/html.png') repeat-y 50% 50%;
        display: flex;
    }
    .content_sub {

    }
    ...
}
```


```css
@media only screen and (min-width: 768px) {
	...
    .content {
        display: flex;
    }
    .content_sub {
        background: #F5FAEF;
        box-shadow: -4px 0px 4px #ddd;
    }
    ...
}
```

###SVG

###CSS Starburst
<body>
<div class="rect-container">
<div class="rect copy">Beta!</div>
<div class="rect one"> </div>
<div class="rect two"> </div>
<div class="rect three"> </div>
</div>
</body>
add styles
<style>
.copy {
    color: #fff;
    z-index: 999;
    font-size: 90px;
    text-align: center;
    line-height: 200px;
}
.rect-container {
    width: 200px;
    height: 200px;
    position: relative;
    top: 100px;
    left: 100px;
    -webkit-transform: scale(.4) rotate(15deg);
    cursor: pointer;
    -webkit-transition: all 0.2s linear;
}
.rect-container:hover { -webkit-transform: scale(.5) rotate(0deg) }
.rect {
    width: 200px;
    height: 200px;
    background: #f90;
    -webkit-transform: rotate(0deg);
    position: absolute;
    top: 0;
    left: 0;
}
.two { -webkit-transform: rotate(30deg) }
.three { -webkit-transform: rotate(60deg) }

</style>



###Tap Highlight Color

###JavaScript Beta Window

<script src="js/jquery.js"></script>

<script>
	jQuery('.branding h2').addClass('emphasis');
	$('.branding h2').addClass('emphasis');
</script>

$(document).ready(function() {
		$('.branding h2').addClass('emphasis');
	});

<script>
(function() {
	$('.branding h2').on('click', function() {
		alert('test');
		$(this).toggleClass('emphasis');
	});
	})();
</script>

<div class="betainfo">
<p>Information about the beta program<p>
</div>

.betainfo {
    display: none;
    width: 200px;
    height: 100px;
    background: #fff;
    border: 1px solid #999;
    position: absolute;
    top: 10px;
    left: 50%;
}

Then try this to center the box:
left:calc(50% - 100px);

<script>
(function() {
	$('.branding h2').on('click', function() {
		$('.betainfo').toggle();
		$('.betainfo').fadeToggle();
	});
})();
</script>

$('.branding h2').on('hover', function() {
console.log('Hello World!');























