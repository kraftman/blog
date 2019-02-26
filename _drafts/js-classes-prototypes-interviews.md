Javascript: classes, prototypes, and interviews

When preparing for interviews that focus on Javascript, some common themes tend to emerge.
Gotchas about comparisons, questions about scope, hoisting, and closures. One that caught my eye in particular, however, was 'Explain the difference between classical vs prototypal inheritance'.
One article when so far to basically say if a candidate couldn't explain the difference, that would be the interview over.

Classical inheritance:
Objects can only be created by instantiating classes
Doesn't really exist in JS, since there are no abstract classes, just objects pretending
As the level of abstraction increases, entities become more general (chris -&gt; man -&gt; human)

Prototypal:
We only have objects
Only one type of abstraction
Prototypes can inherit from other prototypes, and objects can inherit from prototypes.
When you try and access a property, the engine looks on the object, then at the prototype of the object, and so on.

So classical doesn't really exist in JS, we're done. Right?
Well not quite. Javascript likes to pretend that it does have classes, and can make things a bit messy. There are a lot of ways to skin a cat.
The .prototype property

Object.create, Object.assign.

Types of prototypal inheritance:
Prototypal pattern
Clone an object:
Delegation vs concatenation
Delegation:
object has a link to a prototype for delegation (properties not found are delegated to the prototype, and so on.)
Can use 'new', or Object.create()
changes to the prototype are reflected to the object

Concatenation
object.assign
Copies source properties from multiple objects.
changes to the prototype dont affect the new object

Constructor pattern

dont use classes:
https://performancejs.com/post/hde6d32/The-Best-Frontend-JavaScript-Interview-Questions-(Written-by-a-Frontend-Engineer)
https://github.com/joshburgess/not-awesome-es6-classes
http://www.ianbicking.org/blog/2013/04/new-considered-harmful.html
https://tsherif.wordpress.com/2013/08/04/constructors-are-bad-for-javascript/
https://stackoverflow.com/questions/383402/is-javascripts-new-keyword-considered-harmful
https://medium.com/javascript-scene/the-heart-soul-of-prototypal-oo-concatenative-inheritance-a3b64cb27819