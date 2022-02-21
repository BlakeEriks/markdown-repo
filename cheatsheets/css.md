# CSS

## Specificity

The specificity of a CSS selector determines which styles have the priority. It's represented by 4 values -> `a, b, c, d`, and are calculated using the following rules.

1. `a` is whether inline styles are being used. If the property declaration is an inline style on the element, a is 1, else 0.
2. `b` is the number of ID selectors.
3. `c` is the number of classes, attributes and pseudo-classes selectors.
4. `d` is the number of tags and pseudo-elements selectors.

Each successive value trumps those after it. Ex specificity of `0,1,0,0` is greater than `0.0.10.10`. If equal, the later rule trumps. 

## Resetting & Normalizing

__Resetting__ is stripping away all default browser styling on elements. 

__Normalizing__ preserves useful default styles rather than resetting everything. It also corrects bugs for common browser dependencies.

## Floats

__Float__ is a CSS positioning property. Floated elements remain a part of the flow of the page, and still affect the positioning of other elements. Text will flow around floated elements.

The CSS `clear` property will position an element below `left`/`right`/`both` floated elements.

If a parent contains nothing but floated elements, its height will be 0. This can be fixed by `clear`'ing the last child float.

## Z-index

Z-Index controls the vertical stacking order of elements on a webpage. It only affects elements that have a position value that is not `static`. Normally elements appear and layer in the order they appear in the DOM.

A stacking contexxt is an element that contains a set of layers. Within a local stacking context, the z-index values of its children are set relative to that element rather than to the document root. Layers outside of that context — i.e. sibling elements of a local stacking context — can't sit between layers within it. If an element B sits on top of element A, a child element of element A, element C, can never be higher than element B even if element C has a higher z-index than element B.

