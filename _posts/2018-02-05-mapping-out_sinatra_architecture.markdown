---
layout: post
title:      "Mapping-Out Sinatra Architecture"
date:       2018-02-05 06:50:14 +0000
permalink:  mapping-out_sinatra_architecture
---


For a while now I’ve been wondering how programmers keep track of all their work when the code they’re working with is so massive.  It seem the answer is: ‘frameworks.’  Frameworks set up the ground rules so multiple programmers can collaborate on a set of [valid] assumptions, they also disentangle what would otherwise become *spaghetti-code* wherein one little change in the program somewhere will break the whole thing and force you to chase down bugs for weeks on end.  Best of all, they save time by doing a lot of work for you that several programmers would otherwise have to each do on their own, forcing them to all write the same code over & over again.

This is all well and good, but frameworks are not intuitive and idiot proof.  In the case of Sinatra, you have to remember to do certain things in a certain order, and then you need to remember how all of the different elements communicate with each other.  Before you even start, you have to have the correct administrative affairs all set in order or it won’t even work.  Some files even have to be named according to certain conventions or stuff will break.  The solution to all these problems is of course, another illustration!

**Creating a Roadmap to Navigate through Sinatra**

If you haven’t already, I would suggest reading my blog entry on the [symbology I created here]( https://richard-burd.github.io/object_oriented_architecture_for_visual_thinkers) to graphically illustrate code.  Although this system can illustrate an actual program, it isn’t really set up to explain *how* and *when* code works.  For that, I have been relying on a set of ad-hoc notes & sketches as well as (mental) memory.  While working on the various Sinatra labs in the Active-Record module, I used my system to draw out the basic process flow illustration below: 

![Imgur](https://i.imgur.com/yEPbrG9.png)

This is not illustrating any specific lab or workspace, it is just an ad-hoc of several workspaces (from the Flatiron curriculum) showing the full-stack framework.  The back-end is oriented to the left side of the page and the front-end is located towards the right side.  The symbol legend is actually a *master-symbol-legend* that includes my entire symbology, and is not limited to just the symbols used in the drawing itself.  Unlike anything I’ve drawn in the past, this diagram has several boxes & ellipses just sort-of floating in space without any sort-of connection shown to the rest of the program.  This is only possible because I am not illustrating any Active-Record or Sinatra source code that is actually linking these elements together in the background.  For this reason, the Active-Record methods are transition-colored from red to white while the Sinatra methods have a grey-to-white (silver) color scheme to match the Sinatra [hat] official logo.  The new rule introduced: any method using *any* framework in the background to communicate should be multi-colored instead of mono-colored.  

Several important things are missing here; I don’t see how or when to create migrations, seed data, or pass hashes between the forms in my views and the various controllers that transfer the data in those hashes to the models in Active Record, and finally into the SQL database itself.  In order to do all that, I took the drawing above, and added to it until I ended up with this drawing below:

![Imgur]( https://i.imgur.com/GyMEYlT.png)

This second illustration adds a series of sketch-notes throughout the drawing that begin to illustrate (albeit somewhat esoterically) the *when* dimension of using Sinatra.  To start with, in the “Database” column I have everything I need to remember how to create migrations and format a seed file.  Under the “Views” column, I have a Sinatra (User) Forms block that meticulously spells out how a hash is generated from a users’ input, and how the controller then interprets that hash into information that can be transmitted into the database using Active Record.  The Sinatra Nested Forms block explains how to use nested arrays, which I ended up needing to do for my portfolio project.

The result was that, although I created a process flow diagram for the object models in my Sinatra Portfolio project, I did not need to draw out the whole program in order to visualize what was going on.  Instead, all I really needed was this *paradigm* illustration to show me how a Sinatra app is put together and as long as I followed all of the proper naming conventions (as well as the conventions on subdirectories) then I wouldn’t end up getting lost.  The advantage of course is that this saves considerable time since a single illustration can get recycled on each new project it resembles.

