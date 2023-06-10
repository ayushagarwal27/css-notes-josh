# Troubleshooting

- Unfortunately, it's very common to apply `position: sticky` to an element, only for nothing to happen; the element won't stick!

## A parent is hiding/managing overflow

This is probably the most common reason in a large, real-world application.

- When we set  `overflow`  to  `hidden`/`scroll`/`auto`, we create a scroll container. And when it comes to sticky positioning, elements stick  _to the closest scroll container._
- Here's how to think about it:  `position: sticky`  can only stick in one "context". If it's within a scroll container, it can only stick within that container.

- Frustratingly, it doesn't have to be a direct parent, either — it might be a great-great-great-great-grandparent that sets  `overflow: hidden`, maybe to remove an unwanted horizontal scrollbar!

**How do we figure out which element is the culprit?**  Here's a snippet you can run in the browser devtools to figure it out:

```js
// Replace “.the-sticky-child” for a CSS selector
// that matches the sticky-position element:

const  selector  =  '.the-sticky-child';

function  findCulprits(elem)  {
	if  (!elem)  {
	throw  new  Error(
	'Could not find element with that selector'
	);
}
let parent = elem.parentElement;

while  (parent)  {
	const  {  overflow  }  =  getComputedStyle(parent);
	if  (['auto',  'scroll',  'hidden'].includes(overflow))  {
	console.log(overflow, parent);
	z
	parent = parent.parentElement;
 }
}

findCulprits(document.querySelector(selector));
```

- You can copy/paste this snippet into the browser console, replacing  `selector`  with a CSS selector that matches your sticky element. It will crawl up the DOM tree looking for an ancestor with  `overflow`  set to either  `auto`,  `scroll`, or  `hidden`.

**So how do we fix it, once we've found the culprit?**

-   If the culprit uses  `overflow: hidden`, we can switch to  `overflow: clip`. Because  `overflow: clip`  doesn't create a scroll container, it doesn't have this problem!
    
-   If the culprit uses  `auto`  or  `scroll`, you  _might_  be able to remove this property, or push it lower in the DOM. This is a tricky problem, often without a quick solution.

- Just know that if sticky positioning isn't working, there's a good chance that an ancestor is managing overflow.

## The container isn't big enough

-  A sticky element will only follow the viewport  _as long as it remains inside its parent container._

- Make sure that your sticky element has room to move within its parent container.

## The sticky element is stretched

- When using Flexbox or Grid, it's possible for a sticky element to be stretched along the cross-axis. This, in effect, makes it so that the element has no space to move in its parent container.

## There's a thin gap above my sticky header!

- If you intend for an element to sit right against the edge of the viewport, you might discover a thin 1px gap between the element and the edge in Chrome.

- This is a rounding issue with fractional pixels. I've solved this issue by insetting the sticky element by a single pixel:

```css
header {
	position: sticky;
	top:  -1px;  /* -1px instead of 0px */
}
```