#CDS

##Cascading Definition Sheets

### Section 1 - Introduction
CDS is a new way to describe your HTML6-based markups. It merges DTD and CSS to one syntax.  
With CDS you are able to:
* style your documents
* create your own namespaces
* define childs and their parents

CDS keeps back compatibility with CSS, so if you are a webmaster, learning new syntax will take a few _minutes_.

### Section 2 - At Rules
In CDS there are some special rules beginning with the "@" char.  
Here's the list of CDS's at rules:

#### @import
At import rule lets you load an external CSS or CDS file.

```css
/* Syntax */
@import url("path/to/a/file.css");
```
