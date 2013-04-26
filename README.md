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
