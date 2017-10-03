---
layout: post
title:      "Object Oriented Architecture for Visual Thinkers"
date:       2017-09-15 15:55:14 -0400
permalink:  object_oriented_architecture_for_visual_thinkers
---


The basic problem with learning code is that, at some point, there are simply too many pieces & parts to keep track of.  If you’re a visual thinker like me, you’ll often find yourself frustrated that you can’t see some sort of ‘grand-scheme’ or floor-plan for what is going on in front of you.  Since I work with programmers, I can see how they do things; they have multiple computer monitors on their desk to display five or six collaborating methods (or functions) all at once, and make judgements based on this interface.  The actual workspaces wherein we divvy up classes & methods into separate folders are largely designed (at least in part) to help the programmer make sense of all their code.

A while back I finally had enough and decided that I needed to develop some sort of symbology for representing the code I was reading and designing.  I needed a two-dimensional 'plan-view' of what I was doing so I could track classes & methods that were collaborating with each other and see how they were doing it; what follows is the system I came up with.  For starters, let’s look at some object-oriented Ruby code familiar to all the full-stack web development Flatiron School students, the Dog class, Fido the `Dog.new`, and `Avi` the dog `owner`:
```
class Dog 
  attr_accessor :name, :owner
  
  def bark 
    "grr ruf ruf"
  end 
  
  def speak_up 
    puts "#{self.name} says '#{self.bark}!'"
  end 
  
  def go_outside_and_get_the_newspaper 
    "#{self.name} happily gets the paper."
  end  
end 

class Owner 
  attr_accessor :name, :dog
  
  def send_dog_to_get_paper 
    puts "#{self.name}'s dog #{self.dog.go_outside_and_get_the_newspaper}"
  end 
end 


fido = Dog.new 
fido.name = "Fido"
avi = Owner.new
avi.name = "Avi"
avi.dog = fido 
puts fido.speak_up
puts avi.send_dog_to_get_paper
```




**Drawing chunks of code**

First, let’s start out with the Dog class in Fig. 1 below.  There you can see the Class represented as a simple green box, inside of which the instance variables are red boxes and the methods are pink ellipses.

![Imgur](https://i.imgur.com/zjZh05H.png)

The idea here is to have a different symbol for each type of data; we can quickly glance at `class Dog` and see its overall structure, even though we can't see what the individual Ruby methods are actually doing, for that we need the actual code.  This isn’t particularly helpful when we compare it to the `class Dog` code because at this point, the class is fairly small and it isn’t collaborating with any other class or module.  We also don’t have any sense of what instance variables or modules are collaborating with each other or why, which brings us to Fig.2.

![Imgur](https://i.imgur.com/z2iNePE.png)

Here we can see the relationships expressed as curvy little red lines with arrowheads; the arrow points to the method that calls the instance variable (or other method) at the other end of the curvy red line; `speak_up` for example, calls both `bark` as well as `name` so we want to visually represent those relationships.  At this point our graphic still isn’t that useful; we can look to the code on the right-side of Fig.2 and know all this same information.  Why bother to do any of this?  Because we’re going to reach a point real fast where we’re able to show more relationships in graphic form than we can fit on a single monitor, this of course leads us into Fig.3 below.

![Imgur](https://i.imgur.com/xQVeMFb.png)

Here’s where the rubber meets the road, but first, we need some housekeeping.  On the right we have a symbol legend that tells us what is going on.  As programs get more complex, we need these to remind ourselves (let alone others) of what we were drawing and why; so far I’m up to a library of some +30 symbols.  The full text of this program (which is up above) wouldn’t fit in this diagram unless we shrunk the text size way down.  Here we don’t need to read through anything to see the most important relationship: that each instance of `class Owner` is the value of `owner` in the `class Dog`.  Additionally, we see that `class Owner` and `class Dog` collaborate with each other.




**Following the Path of Abstraction**

A while back I was working on the Tic Tac Toe with AI project [here](https://learn.co/lessons/ttt-with-ai-project) and got totally stuck on it.  I could not keep track of all the collaboration and so my solution to one `rspec` test would invariably cause another one somewhere else to fail.  In particular, I couldn’t figure out the `current_player.move` call that was supposed to go in the `turn` method inside the `class Game`.  Where the heck was `current_player` getting the ability to call `move`!?  And more importantly, how was the user expected to input a value for that method when there were no calls for the user to do so in the `class Game`!?  This was frustrating, so I began to develop my methodology for graphically representing the program and then came up with the idea of what I call ‘abstraction markers.’  These little numbered diamonds show the “plumbing” of code; you can trace inheritance through variables & methods to their point of origin.  In this example below, we can see that in the `class Game`, there are a series of what look like little blue pills with a method inside, accompanied by an abstraction marker diamond.  From here I can see that the illusive user input originated in the `class Human` located inside the `module Players`;  at this point I can solve the lab with ease.

![Imgur](https://i.imgur.com/L6ooeVe.jpg)

**Using This Graphic System to Design a New Program**

In this lecture [here](https://www.youtube.com/watch?v=_lDExWIhYKI) we got some ideas on how to go about creating a new program.  From a designer’s perspective, Avi’s approach seems somewhat haphazard but from speaking to my colleagues who code for a living; this is normally how things get done.  Sometimes programmers will hand-draw a scheme on a white board (“white-boarding”) but this approach hearkens back to the day when architects drew buildings with pencils instead of on CAD programs.  You can only revise a marker or pencil drawing so many times and as you add new information, you will eventually run out of room on the page (or board) if your drawing gets too big, so it’s better to work with digital diagrams.  For my CLI Portfolio Project, I started out drawing something like what we see in Fig. 4 below:

![Imgur](https://i.imgur.com/aq5kfZf.png)

Here I’ve got a hypothetical method to scrape data from a live website that could be represented as `some_core_method_to_my_project`.  As you would expect, later on I created other methods that manipulated this data into a format that I liked and thought I’d be able to work with.  At some point I found myself having so many methods that it was time to find a home for some of them inside a class or module, which takes us to Fig. 5 below.

![Imgur](https://i.imgur.com/3Vwx09T.png)

Here, my second, third, and fifth methods all work towards some common goal or have a unified purpose; for that reason they can be housed in a class together.  Not shown here is the fact that, now when I want to use these methods, I need to instantiate (or create an instance of) my `class FirstClass`.  This brings up a whole other issue I haven’t figured out how to illustrate yet; *time*.  Classes are created with the idea that at some point in *time*, an instance of that class will be created in order to do something; sometimes a program will create (and run on) just one instance of that class whereas other times it will create multiple instances.  Through my own observation and experimentation, I’ve discovered that class creation isn’t so much governed by if and where you need multiple instances of a given data set, but rather, *when* in a sequence of events that new object, complicated in nature, needs to be brought forth in order to accomplish some given task.  In this way, a class may only have one instance of itself such as with the `class Game` and `class Board` in the Tic Tac Toe (with AI) project mentioned above.  A class may also have only one method or variable such as with the `class DataScraper` and `class DataRequester` shown in my Boulder Weather-Check program discussed below.

![Imgur](https://i.imgur.com/2gUm05e.png)

Fig. 6 above is really just a repeat of the cycle described in Fig. 5 previously.  Here the fourth, sixth, and seventh methods finally have a home whereas the fate of the remaining three methods are still up for grabs; they could end up in a class or module together, or with newer yet uncreated methods.  In an overly simplistic nutshell, this is how I went about designing my [CLI Data App Portfolio project](https://learn.co/lessons/cli-data-gem-assessment), but stay tuned for more on that in my next blog post.  Here’s what that project it looks like in graphic form:

![Imgur](https://i.imgur.com/NJVwawn.png)

As you can see, there is a plethora of symbols in the legend on the right of the page, and these are somewhat different than the symbols in the “Tic-Tac-Toe With AI illustration” above.  The truth is, this drawing is sort of like comments [in the code] but on steroids; in a few split seconds I can check the requirement blocks, see what methods are where and what methods are collaborating with each other across class boundaries, and see where each class is located in the program’s subdirectories.  I can see where classes are instantiated and how they relate to other classes in the program.  I can even use my “blue-pills & pink-pills” to track abstracted information as it moves through the program.  

If you’re thinking all this drawing might be too hard to maintain for a large project you are correct, which is why at some point, we need to abstract things out a bit.  In example, Fig. 7 below takes us all the way back to the same format we encountered in Fig 1:

![Imgur](https://i.imgur.com/HY63sqE.png)

Here we have methods in classes, but no relationships between methods; there are two ways to make use of such a format.  First, as is the case with my Boulder Weather-Check Illustrated diagram above, I have a `module ProblematicWeatherDefined` wherein all the methods do exactly the same thing; if you follow the arrows into (and out of) the module’s purple box, you will see what each method is up to.  Also, I can employ this “abstracted” form of module illustration if I’m working with another programmer and I want to see what his module is doing, but I don’t care about the details as I’m not having my code collaborate with his.  This of course brings us to Fig 8 below:

![Imgur](https://i.imgur.com/a4ocJlY.png)

Now here we take out the methods altogether and simply see what class is instantiating what other class.  Imagine a team of 4 programmers and having a diagram of some 50-60 classes on a sheet of paper; you would only need to see methods and method interactions where the different programmers are trying to coordinate with each other.  This hybrid model of differing levels of abstraction can be easily achieved through managing a drawing’s layers.  

**OK great, but what program do we use to make graphics like this?**

I use [Inkscape](https://inkscape.org/en/) which is the free and open source equivalent to Adobe Illustrator.  You only need to learn about 1% of what the program is capable of, Google & YouTube around for it if you’re interested. 





