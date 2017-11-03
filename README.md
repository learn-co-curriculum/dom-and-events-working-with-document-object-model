Working with the Document Object Model
---

## Objectives

1. Explain what a tree is in computer science
2. Describe how the DOM works as a tree
3. Practice exploring the DOM

## The DOM

From the Wikipedia homepage, open your console and type in document.  

```javascript
document
// # document
```

If you click on the arrow next to the word document, you will see that document holds one direct subcomponent, html, which itself has two sub-components: head and body.  The document object encloses the HTML, and the HTML element, encloses the sub-components.  In other words, there is a hierarchy here.   

``` shell
  document
     |
    html
   /    \
head    body
```

The document is at the top, HTML is underneath document, and there are two components directly under HTML.  In computer science, we call this structure a tree.  In the tree above, the document is the **parent** of HTML, and HTML is the **child** of document.  HTML itself is also the parent of head and body.    

We can see this through the console.  

```js
document.children
// [html.js-enabled]

let html = document.querySelector('html')
html.children
// [head, body#www-wikipedia-org.jsl10n-visible]
```

Ok, now that we can see what we mean by parents and children, let's represent a couple of other terms.  Each element, document, html, head, and body are called nodes of the tree.  The lines between them are called edges or vertices.  

``` shell
    document (node)
        | (vertex)
       html (n)
  (v) /    \ (v)
(n) head    body (n)
```

The word node, is found throughout the DOM api.

```javascript
document.nodeName
// "document"
document.childNodes
// [<!DOCTYPE html>, html.js-enabled]
```

### Working with a nodelist

Let's take a deeper look at the return value of `document.childNodes`.  

```js
document.childNodes
// [<!DOCTYPE html>, html.js-enabled]

document.childNodes.constructor
// ƒ NodeList() { [native code] }
```

As you can see, it returns to us something called a nodeList.  A nodeList is similar to an array, for example we can retrieve elements by the index.

```js
let html = document.querySelector('html')
html.childNodes
// [head, text, body#www-wikipedia-org.jsl10n-visible]

html.childNodes[0]
// <head> </head>
```

However, there are other methods where we cannot use a nodeList like an array.  For example, there is no `map` method on a nodeList.  But lucky for us it is fairly easy to convery array-like objects in JavaScript to an actual array.  Afterwards, we can then use all of our array methods.  Here let's see an example:

```js
let html = document.querySelector('html')

let children = html.childNodes
children.map
// undefined

let childrenArray = Array.from(children)
childrenArray.map(function(node){ return node.nodeName })
// ["HEAD", "#text", "BODY"]
childrenArray.constructor
// ƒ Array() { [native code] }
```

As you can see from the code above, when working with the nodelist, which we often get when working with elements in the DOM, we cannot access some of our favorite iterator methods.  However, after we coerce the nodelist into an array by using the `Array.from` method, we can use all of our favorite array methods like `map`.

## Resources

- [MDN - Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [MDN - Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)
- [MDN - NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

<p class='util--hide'>View <a href='https://learn.co/lessons/the-dom-is-a-tree'>The DOM is a Tree</a> on Learn.co and start learning to code for free.</p>
