---
layout: post
title:      "Sinatra Portfolio Project Review"
date:       2018-02-05 23:44:02 -0500
permalink:  sinatra_portfolio_project_review
---


Before starting this portfolio project, I began a paradigm shift away from illustrating whole programs to just illustrating the general frameworks they were written in.  The idea is, if we can graphically conceptualize the framework in a single illustration, we can recycle that illustration and use it on multiple projects.  From the outset of this portfolio project, I coded in an ambitiously complex set of object models to see if I could get them to collaborate properly. Although this project allowed me to explore Active Record’s abilities in depth, the stringent requirements for restful routes limited my abilities to refactor my controllers and views.  This was partly due to me using the more complex *slugging* of objects in the URLs rather than using object ID’s, but also due to another fundamental limitation: our use of Sinatra did not explore the abstracting-out of embedded Ruby code. 


**Principles of Object Model Relation**

The diagram below (Fig.1) shows the three different kinds of relationships that you can use to tie object models together.  The first one (the has-many-belongs-to relationship) is shown with a simple green arrow between the methods inside the Artist & Song classes:
![Imgur](https://i.imgur.com/h068dVf.png)
The second and most complex, as it involves the definition of six methods (two in each object model) is the join table relation.  Here I have the join table colored blue and the relation arrows also colored in blue.  This is done to highlight what I call the *relationship-loop* between all six methods.  If you look closely, these six blue arrows form a contagious, unbroken, loop between all six methods.  If any of these six methods are missing, Active Record will produce a cryptic error message and you won’t always know which of the six you’re missing…so it’s a good idea to diagram them all out.


**The Ping-Pong Game**

Getting the object models working is the easy part because you can first draw up the model relations, then type out the code based on what your drawing tells you to type.  When I created my migrations the first time around, everything just *worked* out of the box because I had this illustration to work from:

![Imgur](https://i.imgur.com/IRiuHbM.png)
Because of the dynamic *time* dimension in the controller-view relationships however, it isn’t possible to illustrate them in the same fashion and so other methods of visual aid need to be relied upon to track the code’s progression.  This is where the idea of a *paradigm* comes in handy.  First let’s look at Fig.2. below to better understand the relationship between views & controllers:

![Imgur](https://i.imgur.com/vxXw4ye.png)

I like to think of this as a ping-pong match with the controller on one side, and the view on the other.  You first have to create instance methods on the control side (within the various *get, post, & delete* requests) that define the interaction; this is analogous to good opening serve.  From there the form inside the view has to receive these instance variables and produce a hash out of it; the hash will be as nested or as large as the serve it receives requires it to be.  That hash then becomes the ball being thrown back to the controller who then has to read it and then transfer the relevant data back to the database via Active-Record.  From here the controller is ready for the next view that requires yet another set of instance variables to then define the view’s hash properly…the process then repeats itself until the user stops clicking on submit buttons.

The problem here is not that we need an illustration of how my library app works specifically, but that we really need something that captures these complex Sinatra framework processes instead.  The solution to that problem is below:

![Imgur](https://i.imgur.com/GyMEYlT.png)

I discuss this drawing above in more detail in my previous blog post, but the main idea is to have a sort-of ‘master-template’ that I can rely on every time I want to create a Sinatra app.  Here I have a framework for Sinatra using files & objects from the Flatiron School’s Fwitter and Playlister labs.  Everything in pink are my notes which first walk me through the creation of migrations, then the ping-pong game discussed above.  

One other problem here is that in order to meet the requirements of the portfolio assignment, the URL routes must be restful.  Time could’ve been saved by effectively making the *new* and *edit* pages exactly identical, but when doing this I ended up with either question marks in my URL’s or URL’s that did not convey the RESTful convention.  If I learned anything at all I figured out why many websites *do not* use RESTful routing…because it is somewhat annoying to have as a design requirement.


**Very Smelly Code**

To get a sense of how this all works, let’s look at the *edit-a-book* page as it would be rendered in a browser:

![Imgur]( https://i.imgur.com/xMmtX6u.jpg)

So here we want to render all possible authors, languages and genres that a book could possibly take in as associations, below is a code snippet from this page:

```
      <% if !author.name.include?("- Author Unknown") || author == @book.author %>
        <% if author == @book.author %>
          <li><b><input type="checkbox" name="book[author_id]" id="<%= author.name %>" value="<%=author.id%>" checked>  <%=author.name%>&emsp;&emsp;&emsp;</input></b></li>
        <% else %>
          <li><b><input type="checkbox" name="book[author_id]" id="<%= author.name %>" value="<%=author.id%>">  <%=author.name%>&emsp;&emsp;&emsp;</input></b></li>
        <%end%>
```
So basically we’re saying that if the book’s author matches an element of the authors array, go ahead and mark the author as checked.  Right after that we’re iterating over the same authors array again but to include all the other (unchecked) authors.  Before any of this happens, the code searches for author names that include `” – Author Unknown”` to exclude those authors associated with a single, unattributed book.  This is already repetitive but I have not yet figured out how to make a new method that would intake a couple of variables within the actual ERB.  This next part smells even more:
```
<% lang_array = @languages.sort_by {|lang_obj| lang_obj.name} %>
  <ol style="font-size:120%; color: grey">
    <%lang_array.each.each do |language| language_id = language.id %>
      <% if @book.languages.include?(language) %>
        <li><b><input type="checkbox" name="booklanguage[langs][][language_id]" id="<%= language.name %>" value="<%=language.id%>" checked> <%=language.name%>&emsp;&emsp;&emsp;</input></b></li>
      <% else %>
        <li><b><input type="checkbox" name="booklanguage[langs][][language_id]" id="<%= language.name %>" value="<%=language.id%>"> <%=language.name%>&emsp;&emsp;&emsp;</input></b></li>
      <%end%>
    <%end%>
  </ol>
  <br></br>
  <br></br>
<h3>Select from the list of Genres below</h3>
<% gen_array = @genres.sort_by {|gen_obj| gen_obj.name} %>
  <ol style="font-size:120%; color: grey">
    <% gen_array.each.each do |genre| genre_id = genre.id %>
      <% if @book.genres.include?(genre) %>
        <li><b><input type="checkbox" name="bookgenre[gens][][genre_id]" id="<%= genre.name %>" value="<%=genre.id%>" checked> <%=genre.name%>&emsp;&emsp;&emsp;</input></b></li>
      <% else %>
        <li><b><input type="checkbox" name="bookgenre[gens][][genre_id]" id="<%= genre.name %>" value="<%=genre.id%>"> <%=genre.name%>&emsp;&emsp;&emsp;</input></b></li>
      <%end%>
    <%end%>
  </ol>
```
Now here the languages and genres are exact replicas of each other, again it would be nice to have these refactored into a templating method but would I have to do all of that in Ruby or is there a way to do it in ERB instead?  A similar problem occurs throughout the library as I display the data by location, language, genre, or time period; each ERB file is a near duplicate of its neighbor.

As I finished this all up so as to meet the project requirements I wondered if & when it isn’t a better idea to stick with the repetition and forgo refactoring.  After all, anybody onboarding this code will be able to recognize the repetitions and probably better figure out what is going on.  If I had all the time in the world though, I would not be able to resist the itch to get everything as refactored as possible. 



