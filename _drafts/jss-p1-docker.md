Being a software developer is great. You get to work from home in your birthday suit, play on the computer all day, and you never have to talk to anyone! Now all you need to do is ensure that you can keep this lifestyle up until you retire, and the best way to do that is to ensure your job is secure. Over the years I've worked in a some great companies with some great people, and I've picked up a few tips along the way for ensuring you're irreplaceable. 

Like me, I'm sure you all miss the good old days of long compile times. Many people have tried to ruin them over the years, but thanks to the new craze of docker, we're right back on track.


Image building is the key to slowing this process down.
<h4>Copy everything!</h4>
Copy the entire project into the docker image every time. This means that you have to build a new image, and spin up new containers every time you make a change to your code, perfect!

Avoid volume mounts. Volumes mounts are the devil. They enable you to develop without having to recreate containers or rebuild images. avoid them at all costs

&nbsp;
<h4>Prevent caching</h4>
Unfortunately dockerfiles have an issue where they will cache every step of your build script and won't re run that step if nothing has changed. For example if you copy your package.json file into the image, it won't copy it again unless there's a change. To avoid this, copy the entire project, that way there is always a change, and it will run every time!
<h4>Build every time</h4>
A slow build is useless if you aren't building often. Some sub-optimal builds will create containers from the same image, rather than building a new image each time, this is far too fast.
<h4>Include everything!</h4>
Docker has a concept called a build contexts wherein it loads all of the folders around your dockerfile in case you need them
<h4>Build remotely</h4>
By now you've got to a nice setup where every change requires a rebuild, you've skipped the build cache, and you have to recreate your containers. You're probably wondering how this could get any slower? Here's for our final trick: add source control and image repositories.

What if instead of building locally you built remotely? This adds a whole new layer of scope! Now every time you make a change, you have to commit it, push it, wait for your registry to grab it and build it, then you get to download it from the registry!

Assuming you've followed the previous steps, the image layers should be nice and large, increasing your download times and ensure that the layer always needs to be re-downloaded.

Slow build antipatterns:

Volumes
<ul>
 	<li>allow changes to propogate directly into containers</li>
</ul>
hotreloaders
<ul>
 	<li>webpack dev tools/nodemon ensure you're always testing the latest version without a restart. gross!</li>
</ul>
&nbsp;

Other pro tips:

Never use docker compose. It's far too verbose. If your colleagues can't understand your 400 character 1 line docker script they shouldn't be at your company.

&nbsp;