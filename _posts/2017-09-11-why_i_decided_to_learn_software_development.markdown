---
layout: post
title:  "Object Oriented Architecture for Visual Learners"
date:   2017-09-11 13:51:58 -0400
---


The basic problem with learning code is that, at some point, there are simply too many pieces & parts to keep track of.  If you’re a visual learner like me, you’ll often be frustrated that you can’t see some sort of ‘grand-scheme’ or floor-plan for what is going on in front of you.  Since I work with programmers, I can see how they do things; they have multiple computer monitors on their desk that let them see five or six collaborating methods (or functions) all at once, and make judgements based on this view.  The actual workspaces wherein we divvy up classes & methods into separate folders are largely designed (at least in part) to help the programmer make sense of all their code.

A while back I finally had enough and decided that I needed to develop some sort of symbology to represent the code I was reading and designing.  I needed a two-dimensional representation of what I was doing so I could track classes & methods that were collaborating with each other and see how they were doing it; what follows is the system I came up with.
For starters, let’s look at some code familiar to all Flatiron School students, the Dog class, Fido the `Dog.new`, and Avi the dog owner:
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
First, let’s start out with the Dog class in Fig. 1 below.  There you can see the Class represented as a simple green box.  The instance variables are red boxes and the methods are pink ellipses.

![Imgur](https://i.imgur.com/zjZh05H.png)

The idea here is to have a different symbol for each type of data; we can quickly glance at `class Dog` and see its overall structure.  This isn’t particularly helpful when we compare it to the `class Dog` code because at this point, the class is fairly small and it isn’t collaborating with any other class or module.  We also don’t have any sense of what instance variables or modules are talking to each other or why, which brings us to Fig.2.

![Imgur](https://i.imgur.com/z2iNePE.png)

Here we can see the relationships expressed as curvy little red lines with arrowheads; the arrow points to the method that calls the instance variable (or other method) at the other end of the curvy red line; `speak_up` for example, calls both `bark` as well as `name` so we want to visually represent those relationships.  At this point our graphic still isn’t that useful; we can look to the code on the right-side of Fig.2 and know all this same information.  Why bother to do any of this?  Because we’re going to reach a point real fast where we’re able to show more relationships in graphic form, than we can fit on a single monitor, this of course leads us into Fig.3 below.

![Imgur](https://i.imgur.com/xQVeMFb.png)

Here’s where the rubber meets the road, but first, we need some housekeeping.  On the right we have a symbol legend that tells us what is going on.  As programs get more complex, we need these to remind ourselves (let alone others) what we were drawing and why; so far I’m up to a library of some +30 symbols.  The full text of this program (which is up above) wouldn’t fit in this diagram unless we shrunk the text size way down.  Here we don’t need to read through anything to see the most important relationship: that each instance of `class Owner` is the value of `owner` in the `class Dog`.  Additionally, we see that `class Owner` and `class Dog` collaborate with each other.

**Following the Path of Abstraction**
A while back I was working on the Tic Tac Toe with AI project [here](https://learn.co/lessons/ttt-with-ai-project) and got totally stuck on it.  I could not keep track of all the collaboration and so my solution to one `rspec` test would invariably cause another one somewhere else to fail.  In particular, I couldn’t figure out the `current_player.move` call that was supposed to go in the `turn` method inside the `class Game`.  Where the heack was `current_player` getting the ability to call `move`!?  And more importantly, how was the user expected to input a value for that method when there were no calls for the user to do so in the `class Game`!?  This was frustrating, so I began to develop my methodology for graphically representing the program and then came up with the idea of what I call ‘abstraction markers.’  These little numbered diamonds show the “plumbing” of code; you can trace inheritance through variables & methods to their point of origin.  In this example below, we can see that in the `class Game`, there are a series of what look like little blue pills with a method inside, accompanied by an abstraction marker diamond.  From here I can see that the illusive user input originated in the `class Human` located inside the `module Players`;  at this point I can solve the lab with ease.

![Imgur](https://i.imgur.com/L6ooeVe.jpg)

I started out writing a method to scrape data from a live website which could be represented as `some_core_method_to_my_project` in Fig. 4 up above.  As you would expect, other methods followed that manipulated this data into a format that I liked and thought I’d be able to work with.  At some point I found myself having so many methods that it was time to find a home for some of them inside a class or module, which takes us to Fig. 5 below.

![Imgur](https://i.imgur.com/3Vwx09T.png)

Here, my second, third, and fifth methods all work towards some common goal or have a unified purpose; for that reason they can be housed in a class together.  Not shown here is the fact that, now when I want to use these methods, I need to instantiate (or create an instance of) my `class FirstClass`.  This brings up a whole other issue I haven’t figured out how to illustrate yet; time.  Classes are created with the idea that at some point in time, an instance of that class will be created in order to do something; sometimes a program will create (and run on) just one instance of that class whereas other times it will create multiple instances.  I found the issue isn’t whether or not you will create multiple instances of a class, but rather if a chunk of code needs to happen at a certain point in a sequence of events, that determines what methods get put into a single class together.  Methods are similar but generally can be used at multiple points in time along the program’s life-cycle.

![Imgur](https://i.imgur.com/2gUm05e.png)

Fig. 6 above is really just a repeat of the cycle described in Fig. 5 previously.  Here the fourth, sixth, and seventh methods finally have a home whereas the fate of the remaining three methods is still up for grabs; they could end up in a class or module together, or with newer yet uncreated methods.  In an overly simplistic nutshell, this is how I went about designing my [CLI Data App Portfolio project](https://learn.co/lessons/cli-data-gem-assessment), but stay tuned for more on that in my next blog post.  Here’s what my app it looks like in graphic form:

![Imgur](https://i.imgur.com/EKeTIGz.png)

**OK great, but what program do we use to make graphics like this?**
I use [Inkscape](https://inkscape.org/en/) which is the free and open source equivalent to Adobe Illustrator.  You only need to learn about 1% of what the program is capable of, Google & YouTube around for it if you’re interested. 





