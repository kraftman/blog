naming:

Humans like labels, and naming things.

Take this story for example

A and B walked to the shops. A bought a F and C, B bought a B and a S.
B and A ate the F and B together.

What didn't they eat? Its a simple example so its not to hard to go back and look, but if I'd used Andy, Bernard, Fish &amp; Chips, and Burger &amp; Salad, you wouldn't need to go back and look, because you're brain has already associated those things together and done the work for you.

Code is the same.
If I write c.should.have.all.keys(['first_name', 'address', 'last_name']) Then you have to look up what c is or work it out from they expected keys.

If I wrote
contactRequiredKeys = ['first_name', 'address', 'last_name']
contact.should.have.all.keys(contactRequiredKeys) Then you're offloading a bunch of work to your brains natural ability to associate names to objects, and you can focus on the rest of the code.

On a similar note, use every chance you can to provide extra information to the reader in the code. If you were describing a house you could say 'the house was colourful' or you could say 'the house was red'. More detail in the same amount of words.


stories:

Humans are designed to remember stories. So why not write software as a story? Use the innate ability of abstraction and context to help us understand what's happening.

Names:

Names are key to abstracting complex objects into groups: e.g. a house.

&nbsp;

&nbsp;