Unit vs component tests: a photoshop analogy.


Unit tests test individual components, integration testing tests components with each other, which also indirectly tests those components. So why bother with unit tests?
<h4>The first task</h4>
Lets say two interns, Andy and Bob start at a new company that creates emoticons. Their new boss decides to give them both the same tasks for a while to see who's better.

Their first task is to create a smiley face emoticon for a new emoticon set. The criteria for the icon is that it must be a big yellow face with two eyes, a nose, and a smiling mouth, all in the correct place, and must be a PNG.

Andy opens up Photoshop, creates a new PNG file, draws a big yellow circle, two black dots, and a big toothy smile, saves the file and sends it to the boss.

Bob opens up a Photoshop, creates a new PSD,&nbsp; draws a big yellow circle, eyes, nose, and smile each on seperate layers, and names each layer. Then he exports it as PNG and send them to the boss.

The boss inspects both icons and is happy that all the features are in the right place, and that the files are png, but notices that Andy was finished much faster.
<h4>The second task</h4>
The boss is a bit of a micromanager so once Andy and Bob get back to him he gives them their next task: make a sad face in the same style.

Andy cracks out his PNG, carefully cuts around the smile and removes it, and draws over the top, saves it and sends it to the boss.

Bob cracks out his PSD, hides the smile layer, draws a frown on a new layer, exports it and send it back.

The boss is happy with the results but this time Andy took a lot longer than Bob.

After a few more tasks (sending just the eyes over to another team, changing the background colour of the icon, etc) The boss notices that&nbsp;Bob is frequently slower than Andy, and his changes often results in side effects (accidentally removing the nose, etc).

He decides to talk to Bob, realises he isn't using layers and points him in the right direction.&nbsp;&nbsp;He also decides to update his criteria to check that files are all PSD's with each facial feature on a different layer.

&nbsp;

So the initial criteria are regression tests, and check the end result is what we want. But they don't test the method to get there.

The unit tests enforce the method to get there, and the individual units (the eye layer contains an eye, the eye is black and round), but they don't test the end result.

Because each feature of Bob's file is in a separate layer, we say that the file is extensible: the level of effort required to extend the features is low, and the impact on the existing layers is minimal. Each layer only needs to be changed when that specific facial feature needs to be different, unlike Andy's which has to be modified for any change. In code this is known as the&nbsp;<a href="https://en.wikipedia.org/wiki/Single_responsibility_principle">Single Responsibility Principle</a>.

&nbsp;

Pain points

So unit tests are great, they run fast and give us extra confidence in our code. The problem is that the only work for code that's written to be testable, otherwise you end up doing the equvailent of trying to split Andy's PNG out into layer by carefully cutting each feature out and pasting it into new layers.

&nbsp;