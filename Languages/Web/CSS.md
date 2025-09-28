# CSS (Cascading Style Sheets)

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [Selectors](#selectors)
- [@rules](#rules)
- [Attributes](#attributes)
  - [Text](#text)
  - [Box Model](#box-model)
  - [Positioning and Layout](#positioning-and-layout)
  - [Transitions and Transforms](#transitions-and-transforms)
  - [CSS Filters](#css-filters)
- [Values](#values)
  - [Functions](#functions)
  - [Gradients and Backgrounds (color values)](#gradients-and-backgrounds-color-values)
- [CSS3](#css3)

## Usage

- web development
- styling of [HTML](./HTML.md) in a json format

## References

> https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps
>
> Further: https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/How_CSS_works

## Overview

- add "class" attribute to html element, to define a subclass that can be styled individually (using .classname)
- can directly be included in HTML using the `<style>` element in the `<head>` part of the document or the `style="CSS"` attribute directly in the opening tag of an element (priority: CSS-file < head < element)
- comments: `/* ... */`

Main Syntax: `selector { property: value }`

General:

```css
html_element_name[, ...] {
  style_definition
}
```

Attributes:

- color
- background-color
- border
- font => font-family, font-weight, font-size (in px/%), font-style, ...
- width, height
- margin, padding => margin/padding-top/right/bottom/left
- background => background-color/image/position/repeat/attachment

Structure:

- property: value == declaration
- several declarations == declaration block
- declaration block + selector == rule[set]

## Selectors

- Class => specified as an HTML attribute
  - html_element_name.html_element_class_name { ... }
- Child => all of the childs that are surrounded by the parent
  - parent child { ... }
- Adjacent child => the one child that directly follows the opening tag of the parent
  - parent + child { ... }
- State => based on state of the HTML element (e.g. for links (a-element): link, visited, hover)
  - html_element_name:state { ... }

## @rules

> https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/How_CSS_is_structured#rules

## Attributes

### Text

- font-family => can contain several fonts => if the first one does not work, the next is used
- font-size => text value, px/em
- font-style => italic, bold, oblique
- font-weight => number value, light/bold/bolder
- font-variant => normal, small-caps, ...
- color => string/hex
- text-align => left/right/center
- vertical-align => top/middle/bottom/baseline/sub/super, px
- text-decoration => none/inherig/overline/underline/line-through/blink
- text-indent => px, cm, em, ...
- text-shadow => px (x-coordinate) px (y-coordinate) px (blur radius) color
- text-transform => capitalize/uppercase/lowercase
- letter-spacing => normal, px
- word-spacing => normal, px
- white-space => nowrap/pre/pre-line/pre-wrap

### Box Model

- Margin Area > Actual Border > Padding Area > Actual Content
- margin/padding => top/right/bottom/left

- border-style => none, dotted, dashed, double, groove, ridge, inset, outset, hidden
- border-width => px
- border-color
- width, height => px, %
- min/max-width/height
- background-color
- background-image => url(“...”)
- background-repeat => repeat-x, repeat-y, no-repeat, inherit, ...
- background-attachment => fixed, scroll
- list-style-type => lower-alpha, circle, square
- list-style-image, list-style-position
- styling tables: border-collapse, border-spacing, caption-side, empty-cells (hide), table-layout (auto, fixed)
- styling links => use the events (hover, link, ...)
- styling the mouse cursor => set attribute style and add style “cursor: ...”
  - auto, crosshair, default, move, help, text, wait, n-resize, s-resize, ne-resize, sw-resize, nw-resize, se-resize, e-resize, w-resize, pointer, progress, not-allowed, no-drop, vertical-text, all-scroll, col-resize, row-resize

### Positioning and Layout

- display => block, inline, none
- visibility => visible, hidden, none
- position => static (move with page), fixed (fixed on page), relative (relative to normal position)
  - => set: top/right/bottom/left
- floating => left, right, none (elements are placed on the same height)
  - => may be combined with clear => left, right, both (keeps space around the element empty)
- overflow => scroll, hidden, visible => use these for text
- z-index => higher z-index is more in front of other elements
  - => last drawn is on top => normally by x/y => but then by z-layers

### Transitions and Transforms

- transition
  - transition-property
  - transition-duration => s
  - transition-timing-function => ease, ease-in, ease-out, ease-in-out, linear, cubic-bezier(n,n,n,n)
  - transition-delay => s
- transform (can contain multiple) => rotate(deg), translate(x, y), skew(deg), scale(x, y)
  - transform-origin
  - for 3d: rotateX(deg), rotateY(deg), rotateZ(deg) (same for translate)
  - can also set a perspective attribute (distance from viewer to object
- @keyframes-rule => several keyframes for an animation
  - => each: <percent> { <styling> }
  - => if from 0% to 100% it is the same as using “from” and “to”
  - => usage: set animation properties
  - animation-name => name of the defined keyframes
  - animation-duration => s
  - animation-timing-function => ease, ease-in, ease-out, ease-in-out, linear, cubic-bezier(n,n,n,n)
  - animation-delay
  - animation-iteration-count => number or “infinite”
  - animation-direction => normal/reverse/alternate/alternate-reverse

### CSS Filters

filter functions => used in “filter” attribute (can contain several filters):

- drop-shadow(width height blur color)
- grayscale(percent)
- sepia(percent)
- saturate(percent)
- hue-rotate(deg)
- invert(percent)
- opacity(percent)
- brightness(percent)
- contrast(percent)
- blur(px)

## Values

### Functions

- calc(...) => can be assigned as value to a numeric property e.g. calc(90% - 30px)
- transform functions can be assigned to a transform property
  - rotate(...) => rotates by an angle e.g. rotate(0.8turn)

### Gradients and Backgrounds (color values)

- linear-gradient([direction,] startcolor [% position], ... , endcolor [% position])
  - direction => left/bottom/right/top or combination of those, deg-value
- repeating-linear-gradient => as above, but is repeated when then positions (using px) are passed
- radial-gradient([position,] shape or size, color-stops)
  - position: top/right/bottom/left
- background-size => contain/cover, px
- background-clip => padding-box/content-box
- opacity => float-value from 0 to 1
  - or: filter: alpha(opacity = int-value from 0 to 100)
- Setting multiple background images:
  - background-image: url(1), url(2), ...
  - background-position: <pos1>, <pos2>, ...
  - background-repeat: ...
- => or only one value that applies for all

## CSS3

- vendor-prefixes:
  - Firefox: -moz-
  - Safari/Chrome: -webkit-
  - Opera: -o-
  - Internet-Explorer: -ms
- pseudo classes, pseudo elements
- @font-face rule
- New Attributes:
  - border-radius => px => allows rounded corners (can be set for each corner individually)
  - box-shadow => [“inset” keyoword] horizontal-offset vertical-offset [blur] [spread] [color]
  - text-shadow => offset-x offset-y blur color
  - word-wrap => normal/break-word
- Colors:
  - allows transaprency by using an rgba(r,g,b,a) color-definition or hsl(hue, saturation, brightness)
