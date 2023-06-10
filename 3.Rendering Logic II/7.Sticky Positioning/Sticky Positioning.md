# Sticky Positioning

- `position: sticky`  The idea is that as you scroll, an element can "stick" to the edge. At that moment, it transitions from being relatively-positioned to being fixed-positioned.

- In addition to setting  `position: sticky`, you also need to pick at least one edge to stick to (top, left, right, bottom). Most commonly, this is done with  `top: 0px`  (or  `top: 0`; the unit is optional when it's zero).

## Stays in their box
- An often-overlooked aspect of  `position: sticky`  is that the element will never follow the scroll outside of its parent container. Sticky elements only stick while their container is in view.

## Offset

- As we've seen, every  `position`  value changes the way  `top`/`left`/`right`/`bottom`  work:

	-   With relative positioning, the element is shifted from its natural, in-flow position
    
	-   With absolute positioning, the element is distanced from its containing block's edge
    
	-   With fixed positioning, the element is adjusted based on the viewport
    

- With sticky positioning, the value controls the  **minimum gap between the element and the edge of the viewport**  while the container is in-frame.

- We can set it to `0px` if we want it to stick right against the edge, or we can pick a bigger number to give it a bit of breathing room. We can even use negative numbers if we want!

- With sticky positioning, however, it's all about the “stick point”. `top` has no effect until we start scrolling.

- In many cases, we'll want to use `top: 0px` so that the element sticks the moment the user scrolls to that element, but we can choose different values depending on the effect we're going for.

## Not incorporeal

- Earlier, we saw how absolute and fixed elements are “incorporeal”—they don't block out any space, like holograms. If they have any static or relative siblings, those siblings will be positioned as if the absolute/fixed elements don't exist.

- Sticky elements are like relative or static elements in this regard; they're laid out in-flow. They take up real space, and that space remains taken even when the element is stuck to an edge during scrolling.

- When we change our pink box to be  `position: fixed`, the other boxes move up to fill the space, and the parent shrinks to half of its original height.

- Sticky elements are considered "in-flow", while fixed elements aren’t.

## Horizontal stickiness

- Sticky positioning is almost always used with vertical scrolling, but it doesn't have to be!