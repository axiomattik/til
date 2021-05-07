# Two-value Syntax of CSS's Display Property

The [CSS Display Module Level 3](https://drafts.csswg.org/css-display/) specification defines a two-value syntax for the display property that explicitly distinguishes between an element's inner and outer display types.

Why is this a good thing?

By default the root element of a web page (`<html>`) creates a *block formatting context* which, inspired by raw text, arranges its child elements in a *normal flow* from left to right<sup>[1](#writing-mode)</sup>, wrapping them onto a new line when it runs out of horizontal space. 

A block formatting context recognises two kinds of elements: `inline` and `block`. Inline elements, such as `a` and `span`, conform to the left-to-right flow direction. Block elements, however, such as `h1..6`, `p`, and `div`, are ensconced between new lines and take up the entire width of their parent, so that they appear to stack like blocks on top of one another.

Given that a web page is generally a two-dimensional document and inline and block elements give us control over both horizontal and vertical layout, we might forgive the naive assumption that this is enough to solve the problem of page layout. However, it becomes clear this is not the case when we try to do something vaguely fancy like allow a paragraph to wrap around an image or create a layout using columns.

In order to achieve these things we need to be able to create new formatting contexts.

Historically this has been done by implicitly changing an element's inner display type by using one of several methods:

- assigning a legacy value to an element's display property
- floating an element
- using absolute positioning
- making use of non-default values of the overflow property

All these methods allow us to extract an element from the normal flow of a document and create a new self-contained region of layout. 

The two-value syntax of the display property makes it explicit what an element's inner and outer display types are so we can have a better idea of whether or not its children will belong to a new formatting context.

The two-value syntax of the display property is:

`display: <display-outside> <display-inside>`

The table below shows the legacy value, its two-value equivalent, and whether or not a new formatting context is created.

legacy value | two-value equivalent | creates new formatting context
:----------- | :------------------- | :-----------------------------
block				 | block flow						| no
inline			 | inline flow				  | no
inline-block | inline flow-root			| yes
flex				 | block flex						| yes
inline-flex  | inline flex					| yes
grid				 | block grid						| yes
inline-grid  | inline grid					| yes
flow-root    | block flow-root			| yes

---

<a name="writing-mode">1</a>: Flow direction can be reversed to right-to-left using [CSS Writing Modes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes).
