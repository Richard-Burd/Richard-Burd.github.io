---
layout: post
title:      "Using Graphics for Object Oriented Program Design Development"
date:       2017-09-19 13:09:35 -0400
permalink:  using_graphics_for_object_oriented_program_design_development
---


This blog post explains my CLI Data App Project submission, the repo for which is [here]( https://github.com/Richard-Burd/richardburd-cli-app) and a video demonstration is available [here]( https://youtu.be/6PWwNzizCOs) where you can see the program in action.

As a visual thinker, I’m fixated on the question of how we can graphically represent the world around us.  In my time practicing architecture, I would draw floor plans that represented physical space on a map.  My days as a U.S. Army logistics officer in Afghanistan were spent creating critical-path diagrams that represented time within a month or year so we could predict supply shortages.  Most programmers I’ve worked with don’t use diagrams because they have good quantitative reasoning abilities; they can form complex models in their heads of how their code works, but when they have to collaborate with each other, they often resort to the old-fashioned ‘white-board’ where their hard-to-read, un-intuitive, hand-drawings create unnecessary frustration and headaches.  This was one of my main motivations for [developing my own graphic standards for illustrating process flow]( https://richard-burd.github.io/2017/09/15/object_oriented_architecture_for_visual_thinkers/).  

Programming presents a unique problem; we expect out programs to do certain things at certain points in time; we often determine these points as the user and yet other points are tied to the world clock…sometimes our program must do both, as is the case with my CLI App Program called “Boulder-WeatherCheck.”  Fig. 1 below shows the two most common graphical schemes discussed above, time and space, as they could relate to code:

![Imgur](https://i.imgur.com/wTsp1XK.png)

As we can see, there isn’t a good way to display our classes, methods, variables, and modules altogether in time.  We could create a time-based flow chart of what we expect our program to do and when we expect it to execute different components, but this would divide up, for example, the command line interface (CLI) into several different nodes on a timeline.  Although object oriented program designs may take on significant complexity in the *time* dimension, the flow chart format cannot adequately capture the organizational breakdown needed to display the program’s architecture.  Therefore, the space orientation modified with time markers will prove to be a better solution as we will explore further below.

Before we get started with all that, let’s take a quick look at a graphic showing how I went about designing my program in Fig. 2 below:

![Imgur](https://i.imgur.com/K3hKXSD.png)

OK, so here we have a flow chart showing one of my earliest brainstorming sessions where I attempt to figure out what I’m trying to do.  This is clearly a flow-chart of sorts, and at this point in the process I didn’t care about what code was collaborating with what other code or where;  I had no picture in my mind of what code blocks needed to be created other than the weather database shown in the green box.  From here, I was able to start thinking about actual code blocks and arrive at something that looked more like Fig. 3 below:   

![Imgur](https://i.imgur.com/zLJ8gwb.png)


Now we have a sense of how the code will be broken down into separate blocks (represented above by rectangles) - each with a particular responsibility.  The double-sided arrows show collaborating relationships, but still no real sequence or order to things.  On a totally different but somewhat related note, I decided I wanted to spend some time playing around with GitHub which we hadn’t done so much of in the Flatiron School curriculum.  Specifically, I wanted to divvy up my project into three separate sections so that I would have three separate GitHub [user] accounts contributing to my project, each contributor being *me* on the other end of course.  Why do all this and make a big mess?  Because the whole point of GitHub is version control with multiple users and so I wanted to see what happens when multiple users start contributing conflicting submissions; how would I save my project and how would three different users see information being displayed during various merge requests?  Fig 4 below lays all this out:

![Imgur](https://i.imgur.com/lHFxAfR.png).

Here we have my three user accounts named Red, Green, and Blue-Burd according to their respective avatar colors.  Green-Burd is the overall project leader and maintains the master repo.  Red-Burd’s job is to figure out how to scrape the weather.com URL for the weather data I need to make my program work, and Blue-Burd has to write the overall CLI.  When Green-Burd brings together the ‘upper-half’ and ‘lower-half’ of the project, it should all just work.  The CLI was designed using Avi’s reasoning in [this video here]( https://www.youtube.com/watch?v=_lDExWIhYKI) where he shows us how to use fake-data to ‘spoof’ the CLI into thinking it’s running a real program.  In a similar fashion, I copied the `class WeatherDatabase` into the CLI along with some code to create an instance of the class like so: 
```
class WeatherDatabase 
  attr_accessor :time, :rain, :temperature, :cloud, :wind, :problems
  @@all = []
  
  def initialize
    @@all << self
    @problems = []
  end

  def self.all
    @@all
  end

  def self.delete_all
    @@all = []
  end
end

first_hour = WeatherDatabase.new 
first_hour.time = "12:00 pm"
first_hour.temperature = 70
first_hour.rain = 2
first_hour.cloud = "Partly Cloudy"
first_hour.wind = 2
second_hour = WeatherDatabase.new 
second_hour.time = "1:00 pm"
second_hour.temperature = 70
second_hour.rain = 2 
second_hour.cloud = "Clear" 
second_hour.wind = 2
third_hour = WeatherDatabase.new 
third_hour.time = "2:00 pm"
third_hour.temperature = 70
third_hour.rain = 2
third_hour.cloud = "Clear"
third_hour.wind = 2
```
Once the CLI is made aware of the code block shown above, the CLI & parameter logic [the upper-half of the program] will work even though it is unaware of the lower half.  The only part of the CLI that won’t work (without the lower-half) will be the CLI’s prompt to ask the user for the exact times they want to analyze since these times have already been pre-defined in the code above.  You can check out Blue-Burd’s code [here]( https://repl.it/KpBS/0) –notice there’s no Nokogiri requirement, or scraping of any URL.  Getting back to the issue of multiple user interface in GitHub, Fig. 5 below shows one of the many data points not visible outside a team project:

![Imgur](https://i.imgur.com/NVfXusW.png)

Here, GitHub gives us a flow-chart called ‘network’ that shows us how the different users contribute when they submit and merge their different blocks of code in a timeline format;  this allows for troubleshooting when you know the program was working before a certain user ‘merged’ with you and screwed things up.  It also shows us which users are working on what blocks of code.

**Working Towards Graphic Illustration of Both Time and Space** 
After refining the information in Fig. 3 discussed earlier above, I came to something that looks like Fig. 6 below:

![Imgur](https://i.imgur.com/yi1SUPB.png)

Here we have blocks of code and arrows showing the collaboration between them, but now our arrows show both the direction and the time-sequence of the information shared.  We start with the arrow that has a circle with ‘1’ inside it and follow the chain down to the ‘4’ arrow aiming at the database in the lower right-hand corner of the graphic.  After that, we start again at the CLI with sequence ‘5’ and follow a chain of collaborations back to the CLI with the ‘9’ arrow.  The truth is, this sequence isn’t that complicated and so the final process flow chart in Fig. 7 below didn’t require any sequence markings:

![Imgur](https://i.imgur.com/KJUUwmB.png)

In this diagram I have all my classes and modules clearly defined, but the arrows between them are showing collaboration in a totally different way; in this scheme we see which classes are instantiated in their neighbor classes, the arrowheads are pointing to the class that instantiates the *other* class at the start of the curvy arrow line.  In example, the `class WeatherDataBase` is instantiated inside the `class DataRequester`.  Fig. 7 is in fact a “street-map” level drawing of the “floor-plan” level drawing [here]( https://i.imgur.com/8g2XrVp.png). And yet there is really no way to incorporate the time-sequence arrows of Fig. 6 onto this diagram.  How did I solve this problem?  The old fashioned way, I built a time-sequence model in my head and made sure my classes were being instantiated according to the needs of that model.  As time goes on and my projects become more complex, I anticipate there being a need to develop ways of graphically tracking *time* as a significant factor. 

**OK but how are graphics helpful if you don’t have a clear picture of what you are doing such as what is illustrated in Fig. 6 & 7 above?** 

Here’s where Fig.8 comes in handy:

![Imgur](https://i.imgur.com/ew3OsMQ.png)

So at the point this drawing was made, I had the `class DataScraper` and `class DataRequester` fully built and working; but every other method in my program was class-less.  The `class WeatherDatabase` was partially built but still incomplete.  The methods in highlighter-yellow were still yet undefined but conceived as part of my program.  I had no concept or intention of using three GitHub accounts to submit the project or even how the whole upper-half of the program was going to work; I simply wanted to see if it was possible to enter in a start-hour and an end-hour, then scrape weather data from weather.com for the hours specified…that’s all.

By moving some purpose-defined green boxes around, and connecting them with some curvy arrows, I was able to *see* the program’s architecture 3 or 4 steps out from where I was with the actual code.  In other words, I could first draw-out my next methods, *then* develop a schema of how they would interact and what outputs they would need to produce.  From there I just needed to remember the right way to instantiate a class, define a variable, or iterate over a dataset.  Iteration methods were the hardest, but now I could foresee *exactly* what outputs I wanted my iterators to produce before I started writing them; this saved a ton of time.  

**Conclusion**

Having a good way to draw out your program can be super-helpful when you’re learning to code, and may even come in handy when you try and get multiple programmers to collaborate on a project.  I personally found that once I started drawing out all my code in graphic form, I was able to work much faster and actually get things done.  Prior to developing a graphic system, I would spend hours or days trying to get an `rspec` test to pass whereas now I can get this done in a fraction of the time.  In terms of starting a project from scratch, I found this portfolio project to be much easier (and more fun) then the previous labs where I had no way of seeing what I was doing.  Relying on code alone can be like flying a plane at night and relying solely on instruments to land…having the graphics in front of you can be like putting on a pair of night-vision goggles so you’re able to see what you’re doing in physical space, as opposed to relying on a bunch of numbers.  Here is my CLI Data App project fully illustrated in final form:

![Imgur](https://i.imgur.com/NJVwawn.png)

