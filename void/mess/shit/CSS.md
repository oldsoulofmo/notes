
## Pseudo-classes

Style the state of many HTML elements.

```CSS
button:hover{
	color: blue;
	text-width: 24px;
}

input:checked{
	width:24px;
	height:24px;
}
```

## Pseudo-elements

Pseudo-elements are like pseudo-classes, but they don't target a specific state. Instead, they target "sub-elements" within an element.

```CSS
input::placeholder {
    color: goldenrod;
}
p::before {
    content: '→ ';
    color: deeppink;
  }

  p::after {
    content: ' ←';
    color: deeppink;
  }
```

> [!NOTE] NOTE
> In CSS, we can differentiate between _children_ and _descendants_. Think of a family tree: a child is only one level down from the parent. A descendant might be 1 level down (child), 2 levels down (grandchild), 3 levels down ...

## Combinators

Using combinators we can target direct children of an element, or saying so we can target children and descendants.

## Units

## Inheritance

```css
a {
  color: -webkit-link;
  cursor: pointer;
  text-decoration: underline;
}
```

These styles are part of the _user-agent stylesheet_. Each browser includes their own stylesheet full of base styles like this. There are some hard rules in the HTML specification, but for the most part, each browser comes up with its own default styles. That's why focus rings look so different across browsers!

```css
a {
  color: inherit;
}
```

## The cascade

Applying a styling to the same element using a selector or a class will lead to the cascade putting these two in a conflict where the priority goes to classes, IDs have a priority over both of them and the chain goes on ... But, if we really go into a component based library like `React` then we'll never face this problem.

## Directions

###### Logical properties

```css
p {

  display: block;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;

}
```


> [!NOTE] Note
> These properties are equivalent to the 4 cardinal directions: `margin-top`, `margin-bottom`, `margin-left`, and `margin-right`.
> > `margin-block` refers to the vertical axis. `margin-block-start` refers to the top, since block elements are stacked top-to-bottom. 
> > >Similarly, `margin-inline-start` refers to the left edge, since "inline" is the horizontal direction, and words are placed left-to-right.
 > > > > Why use these alternatives? Because not all languages are left-to-right, top-to-bottom. If you were to switch your browser's language to Arabic, `margin-inline-start` would add spacing to the right instead of to the left, since Arabic is a right-to-left language.
> > > > > These alternatives are known as _logical properties_. It's not just margin: there are logical variants for padding, border, and overflow as well.

## The Box Model

It consists of : 

- Content.
- Padding.
- Border.
- Margin.

The default behaviour  of `box-sizing` (default value, `content-box`) is to add up any border or padding to the final calculated dimensions.


> [!NOTE] `box-sizing: border-box`
> It is the natural behaviour we expect, we get dimensions of the contain or "box" we intend to have and we don't get any additional space added up.

> I start every project with this.
> 
```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```


> [!NOTE] Padding
> Padding is the area between the content and the border.
> ```css
> box{
> padding: t r b l;
> /* or */
> padding: t/b r/l;
> }
> ```

## Units 

Comeback later for it !


> [!NOTE] Border
> The border color in not specified it will take the font's color, to set this explicitly we can use `border: 1px solid currentColor`.
>  > ##### Border vs outline 
>  > Outlines are lines outside of the element's border, they do not take space which means they do not affect the layout, they're just some cosmetic addition we can use to style our elements and give them nice looking distance from their borders.
>  > > Outlines have the same properties as borders.
>  > > > It's important to never apply this styling : 
>  > > > ```css
>  > > > button { 
>  > > > outline: none; 
>  > > > }
>  > > > ```
>  > > > This rule is sometimes used to hide the blue or black ring that can accompany interacting with a button or link. Sometimes, designers ask us to do this.
>  > > > 
>  > > > The problem is that this totally breaks navigation for keyboard users; that ring is required for them to know which element is currently focused!
>  > > 
>  > >  > The only exception is if we provide a suitable alternative. For example:
>  > >  > ```css
>  > >  > button { 
>  > >  > outline: none;
>  > >  > }
>  > >  > 
>  > >  > button:focus {
 background: navy;
 color: white;
 }
>  > >  > ```
>  > >  > Be careful with this: the focus indicator should be at least as high-contrast/noticeable as the default focus indicator.


```css
.outline-offset {
  width: 100px;
  height: 100px;
  border: 4px solid darkviolet;
  outline: 4px solid currentColor;
  outline-offset: 4px;
}
```


> [!NOTE] Margin
> It can be sometimes obscure but if we do it right then we'll get what we have imagined. 

```html
<main>
  <section class="content">
    Hello World
  </section>
</main>
```

```css
.content {
  width:50%;
  margin-left: auto;
  margin-right: auto;
  background: palevioletred;
  padding: 16px;
}

main {
  width: 100%;
  height: 200px;
  border: 3px solid silver;
}
```

This code above will center a child inside it's parent container, tow downsides of this trick is : 
- This only works for horizontal margin. Setting top/bottom margin to `auto` is equivalent to setting it to `0px`.
- This only works on elements with an explicit width. Block elements will naturally grow to fill the available horizontal space, so we need to give our element a `width` in order to center it.

> ##### Outdated ? 
> You may be wondering if this technique for centering is outdated, now that we have modern layout rendering modes like Flex box and Grid. 
>  >The answer is “no”, but it's a bit nuanced.
>  

## Flow layout

The flow layout is the standard normal layout we know, most basic pages are on flow layout. Other layouts do exist like  Positioned layout, “Flexible Box” layout (AKA Flexbox), and Grid layout (AKA CSS Grid). For now, though, let's focus on _Flow layout_ which is the default layout. 

The world of layout consists of blocks and inlines, block stack on each other, while inlines do not. 

In a nutshell, to make a picture fit to it's container without adding a line as it is dealt with in typography we add : 
```css
div{
	line-height: 0;
}
```

For inlines, lines can wrap and when they do ... some styling is only adapted as if the inline is one box and sometimes we do not want that, what we want is deal with lines all of them as boxes : 

```html
<p>
  <strong>Hello, my name is mohammed chaouki.
    </strong>
</p>
```

```css
p {
  max-width: 125px;
}

strong{
  background-color:peachpuff;
  padding-left: 10px;
  padding-right: 10px;
  box-decoration-break:clone;
}
```


> [!NOTE] Inline-block
>There is one more primitive display value we haven't talked about, and it's a sort of Frankenstein: _inline-block_.
>
Essentially, inline-block allows you to drop a block element into an inline context. It's a block in inline's clothing.
>
>Another way to phrase this: it's an element that _internally_ acts like a block element, but _externally_ acts like an inline element. The parent container will treat it as an inline element, since it's external. But the element itself can be styled like a block.

> Inline-block doesn't line-wrap, which means a longer link has to break onto the next line way too early.
>  > To avoid this problem we might wanna choose short links(bad for accessibility) or use effects on links that aren't part of a paragraph.
>  

### Width algorithms

Block elements will expand to fill the available space, seems like they have a default value of `width: 100%` but no, that is not the case. 

Using percentage based width we tell the child element to take the the whole width of it's parent if we define it as `100%`, Parent is `400px` width ? then child is also `400px` width no matter what  circumstances we have (margins, ...).

`width: auto` will make the element grow as much as it's able to but no more, it takes into account circumstances. 

```css
h1 {
  /* width: 100%; */
  margin: 0 16px;
  background-color: chartreuse;
}
```

In the case above, our `h1` will grow to consume (100% - 32px), since there is 16px of margin on either side. (`width: auto`)

It's a subtle but important distinction: by default, block elements have _dynamic sizing_. They're context-aware.

### Keyword values

- min-content.
- max-content.
- fit-content.


> [!NOTE] figures 
> To make figures actually take the available space we might wanna use 
> ```css
> figure {
> 	width: min-content;
> }
> ```


### Height algorithms

Different than width's behaviour, as for heights they wanna take the least minimal height possible and enough.

```css
html, body {
  height: 100%;
}
.wrapper {
  min-height: 100%;
  border: solid;
}
```


