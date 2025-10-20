**Tags:** [[Web development]]

`class="list section"` means the html tag is part of both *list* and *section* classes.
Priorities: ID > Class > Type > Anything else.
Some properties are inherited, check MDN docs to make sure which ones are inherited and which ones aren't.
Using this:
```
* {
  outline: 2px solid red;
}
```
shows you outlines around the different boxes in an html page.
The order is always: top | right | bottom | left, and you can use a shorthand (one `10px` for ex) to specify the same value for each side.
If top and bottom are the same and right and left are the same then you can simply put 2 values.
When using border-box in the box-sizing attribute, the browser substracts the border and padding from an element's width. On the contrary, the default box-sizing (content-box) adds them up.

![[how-to-center-a-div.png]]

`display: grid;` enables an element to set all of its children as a grid of columns and rows, and it' more efficient and uses less code than other solutions.

CSS variables make refactoring code much easier. They cascade like everything else in css so you can override them within selectors. CSS also has a calc function that might allow you to make more refactorable and sophisticated code. `counter-reset` property allows you to create a counter from css and show it in your html code, this can serve to make dynamic lists for example.

`::before` specifies what happens before that specific element is rendered, and using the `content` attribute, you can prefix the element.
`:focus-within` stays active, for example a dropdown menu so that it doesn't disappear and do nothing when you click on one of the options.

Using the url value on the background image attribute using base64 embeds the image into the page and helps avoid extra network calls to load the image.

`padding: min(5em, %8);`: This means that the padding takes the smallest value between 5em and 8% of the screen (ie. if the screen is small enough that the em value of 8% of its width is bigger than 5em, it will automatically choose %8 of the screen as the value).

The `vw` unit scales the font relatively to the screen when applied to the font-size attribute. Using `width: clamp(...);` makes responsiveness towards device screen width less tedious to write (putting the vm unit value in 'preferred'). Using the calc function to mix both vw and rem units (eg. `calc(5rem+5vw)`)  allows the zooming to work since vw only takes into consideration the screen width. `dvh` unit helps adjust the height responsively.

To make images responsive, use max-width to 100%, height to auto, and to standardize the images dimensions use aspect-ratio, and `object-fit: contain/contain;` to make sure no stretching happens.

![[side-navbar.png]]

Add and remove the inert attribute in the javascript code to avoid tabbing interaction while the bar is off screen.

If you want an easy "masonry-style" layout, inside your container you can use the `columns` attribute. To control their spaces use the column gaps property. Putting display to block and adding a bottom margin takes care of vertical spacing.

Accent color and caret color properties chance the default colors of form elements, cursors inside them, etc.

Using position relative on a parent, then inset 0 and margin auto on the child centers the child inside the parent completely.

overflow-y auto will make it so that only a vertical bar is visible and only when needed.

filter: drop-shadow(...) adds shadow to transparent images.

The clip path property clips images into any shape you decide for creativity. The same thing can be done to shape checkboxes.

For circling motion animations, use conic-gradients.

Resize property allows the user to resize elements that have overflow hidden by themselves.

Backdrop filter blur on a transparent element makes the element look like glass.

:not(child-element-pointer-or-whatever) excludes a child from the properties applied by the css selector. :has is also useful in a different way.

![[text-gradient.png]]

overflow-x scroll and giving the container the same size as the children, and specifying a scroll-snap-time for the parent, a scroll-snap align for the children,  creates a smoother and better UX swiper.

Using min-height with the vh unit makes sure the element grows when there's more height.

```
*{
	padding: 0;
	margin: 0;
}
```
Defaults all elements' spacings to 0.

Position sticky an top 0 makes the navbar stick to the top when you scroll.

(js defer attribute in the html (??))

