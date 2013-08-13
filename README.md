#CS
NOTE: Work in progress!

##Cascading Sheets

### Section 1 - Intro

Comments in cs have to begin with `/*` and end with `*/`, like this:
```css
/* This is a comment */
```
Comments are never parsed - they are just for you.

### Section 2 - Selectors
NOTE: Unlike CSS, in cs space has no special meaning, descendant selector is now `>>`.

All names (tag names, namespaces, classes...) has to be in range `[^ .#:={}<>"'!~*;,\/|\s]`.

#### Element selectors
These can be combined just by writing them consecutively (with or without spaces), AND rule is applied on them.

**Tag name selector**  
Pattern: `E`  
Meaning: An element in default namespace (if no namespace defined, then in no namespace) with tag name "E". Special tag name `*` means an element of any tag name.  

**Namespace selector**  
Pattern: `ns|E`  
Meaning: _Always followed by an Tag name selector._ An element with tag name "E" and namespace "ns". Special namespace `*` means any/no namespace, empty namespace (like `|E` for a specific element or `|*` for any element) means an element that hasn't namespace.  

**Class name selector**  
Pattern: `.bold`  
Meaning: An element that has class "bold". Classes are listed in the element's `class` attribute, separated by out-of-range characters (see heading of Section 2).  

**ID selector**  
Pattern: `#menu`  
Meaning: An element whose attribute `id` is equal to "menu".  
NOTE: Because ID is an unique identificator, there can be only one element with given id in the whole document.  

**Has attribute selector**  
Pattern: `[foo]`  
Meaning: An element that has attribute "foo", whatever value of the attribute.  

**Aproximate attribute equality selector**  
Pattern: `[foo=bar]` or `[foo="bar"]`  
Meaning: An element that has attribute "foo" equal to any case-permutation of "bar".  
NOTE: Any value that contains spaces has to be quoted.  
NOTE: This selector is not equal to CSS `[foo=bar]` selector, do not confuse!  

**Exact attribute equality selector**  
Pattern: `[foo==bar]` or `[foo=="bar"]`  
Meaning: An element that has attribute "foo" exactly equal to "bar".  

TODO: Add `[foo^="bar"]`, `[foo$="bar"]`, `[foo^=="bar"]`, `[foo$=="bar"]` ("^" for "beggins with" and "$" for "end with")

**Has rule selector**  
Pattern: `{float}`  
Meaning: An element, which has a non-default cs rule "float".  

**Rule equality selector**  
Pattern: `{float=left}`  or `{float="left"}`  
Meaning: An element, which has a cs rule "float" with value equal to "left" (or which would have value equal to "left" if rules of this selector didn't exist).  

#### Combinators
**Child combinator**  
Pattern: `E1 > E2`  
Meaning: Element "E2", which is a child of element "E1".  

**Descendant combinator**  
Pattern: `E1 >> E2`  
Meaning: Element "E2", which is contained somewhere in element "E1" ("E1" can be child of "E2" or child of its child or even child of its child of its child etc.).  

**Descendant combinator with defined deepness**  
Pattern: `E1 >(n) E2`  
Meaning: Element "E2" which is contained in element "E1" on the defined deepness level (n=1 means "E2" is a child of "E1", n=2 means "E2" is a child of a child of "E1" etc.).  

**Descendant combinator with defined deepness range**  
Pattern: `E1 >(n1,n2) E2`  
Meaning: Element "E2" which is contained in element "E1" on the deepness level "n >= n1" and "n <= n2".  

**Next-sibling combinator**  
Pattern: `E1 ~ E2`  
Meaning: Elements "E1" and "E2" have the same parent and "E2" comes immediately after "E1" in the document tree.  
NOTE: This selector is not equal to CSS `E1 ~ E2` selector, do not confuse!  

**Following-sibling combinator**  
Pattern: `E1 ~~ E2`  
Meaning: Elements "E1" and "E2" have the same parent and "E2" comes (not necessarily immediately) after "E1" in the document tree.  

**Following-sibling combinator with defined distance**  
Pattern: `E1 ~(n) E2`  
Meaning: Elements "E1" and "E2" have the same parent and "E2" is the "n"th element after "E1".  

**Following-sibling combinator with defined distance range**  
Pattern: `E1 ~(n1,n2) E2`  
Meaning: Elements "E1" and "E2" have the same parent and "E2" is between "n1 - 1"th and "n2 + 1"th elements (so "E2" can be `n1`th, `n1 + 1`th, `n1 + 2`th, ..., `n2`th element).  

**Reference combinator**  
Pattern: `E1 /attr/ E2`  
Meaning: Element "E2" which is referenced by attribute "attr" of "E1" element, attribute has to be ID, may (but doesn't have to) begin with the `#` sign.  


#### Pseudo-classes
**Event pseudo-class**  
Pattern: `E:event(start, end)`  
Meaning: Element "E" that has run through event "start" but hasn't run through event "end" yet. After deactivating by "end" event, may be activated by "start" again. Multiple events may be used as "start" or "end" if separated by OR sign - `|`, eg.: `div:event(mouseover|touch,mouseout|keydown).  

**Endless event pseudo-class**  
Pattern: `E:event(start)`  
Meaning: Element "E" that has run through event "start". Multiple "start" events may be used if separated by OR sign - `|`.  

**One-time event pseudo-class**  
Pattern: `E:event-once(start, end)`  
Meaning: Element "E" that has run through event "start" but hasn't run through event "end" yet. After deactivating by "end" event, MAY NOT be activated by "start" again. Multiple "start" or "end" events may be used if separated by OR sign - `|`.  

**One-time event pseudo-class with reset**  
Pattern: `E:event-once(start, end, reset)`  
Meaning: Element "E" that has run through event "start" but hasn't run through event "end" yet. After deactivating by "end" event, MAY NOT be activated by "start" UNTIL "reset" runs. Multiple "start", "end" or "reset" events may be used if separated by OR sign - `|`.  


### Section 3 - At Rules
In CDS there are some special rules beginning with the "@" char.  
Here's the list of cs's at rules:

#### @import
At import rule lets you load an external cs (or css) file.
```css
/* Syntax */
@import url("path/to/a/file.css");
```

#### @font-face
At font face rule is here to attach special fonts to the document. Detailed specification can be found on <a href="http://www.w3.org/TR/css3-fonts/">W3C website</a>
```css
/* Syntax */
@font-face {
 font-family: Gentium;
 src: url(http://example.com/fonts/Gentium.ttf);
}
```

#### @media
At media rule is used to define responsive styles or print versions. Detailed spec <a href="http://www.w3.org/TR/CSS2/media.html">here</a>.
```css
@media print {
 font-family: "Courier New";
}
```

### Section 4 - Missing features
General:
* Nth everything (http://css-tricks.com/a-call-for-nth-everything/)
* Pseudo-element :wrap to clean HTML of styling-only elements - eg. `parent >  (child1 ~ child2 ~ child3):wrap`
* %of() function - eg. `height: 100%of(a>b{width})

Styling API:
* Merge SVG and HTML styling
* Outline radius
* Outer height and outer width
* Background opacity
* Better multi-layer backgrounds
* Image manipulation (masks, effects, `image-rendering` etc.)
* Placeholder styling
* User defined styles (eg.: User defines his favourite colours in browser - how to use these colours in cs)
* Transitions between pages
* More 3D support for our websites (+ 3D image settings)


(c) by m93a, Apache 2.0
http://www.apache.org/licenses/LICENSE-2.0
