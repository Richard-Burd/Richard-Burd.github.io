---
layout: post
title:      "Everything You Need to Slug URLs in Sinatra"
date:       2018-03-09 18:31:43 +0000
permalink:  everything_you_need_to_slug_urls_in_sinatra
---

In the Sinatra module we learn about restful routes and how to properly incorporate an object id number into our app’s URLs.  In this lab [here](https://learn.co/tracks/full-stack-web-development-v3/sinatra/activerecord/sinatra-playlister) we encountered a workspace that puts the object’s name into the URL rather than the object’s id number.  I thought this was cool and wanted to do the same thing for [my Sinatra portfolio project here](https://github.com/Richard-Burd/sinatra-portfolio-project) since I already knew how to use the object id.  What follows is a step-by-step process for anyone who wants to do the same thing.

**Step 1 – Setup a Ruby Method to ‘Slug’ the Strings**
The playlister workspace has a module to do this [here]( https://github.com/learn-co-students/playlister-sinatra-v-000/blob/solution/app/models/concerns/slugifiable.rb) and I made something similar in the commensurate directory for my project [here](https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/models/concearns/slugifiable.rb).  These are methods that ‘slug’ the string going into your URL. Sluging a string means to make it appropriate for something…in this case we are deleting all spaces and replacing them with dashes; we are also making all letters in the string lower case.  By doing this, we are ensuring the string will appear without ‘20%’ markings or capital letters in the URL itself.

**Step 2 – Add the Validation(s) in the Object Model(s)**
This is the important part and you have two options.  The first way is to write some code in the controller that asks if the string you want to slug is already in use.  In example, if I have a book I want to create and I want the book’s title to appear in the URL rather than the book’s id number, I will want to see a URL like `www.example.com/books/moby-dick` and *not* a URL like `www.example.com/books/15` because the `15` doesn’t really tell me anything.  Now to do this I can write some code like this [here]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/8ddbb992ea726b755e97109cde75aae7903883fc/app/controllers/books_controller.rb#L21) inside the controller: 
```
taken_book_title = Book.find_by(:title => params[:book][:title])
  if taken_book_title.present?
  flash[:message] = "Sorry, but that book title is already taken, please choose another title."
  redirect to '/books/new'
end
```
The problem here is that this will not check for alternative capitalizations, and even if it did, this code is beginning to make this post request rather dense, that is, it has more lines of code than it really needs.

OK so here’s the correct way to go about doing all this.  First, you add something like the following line of code to the object model (in this case, the book object model) [here]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/models/book.rb#L12):
```
validates :title, uniqueness: { case_sensitive: false }
```
This is known as an ActiveRecord [validation]( http://guides.rubyonrails.org/active_record_validations.html) and it basically checks to see if a book’s title is going to be unique among all the other book titles before it is ever created.  It will also disregard the case of the letters in the book title string such that `Moby Dick`, `moby dick`, and `MOBY DICK` will all be considered to be one in the same title, and ActiveRecord will only allow one of them to be used.  Next you add a series of statements like this one [here]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/controllers/books_controller.rb#L21) in the controllers:
```
Book.new(params[:book]).valid?
```
This checks to see if the book being created is in fact valid or not.  If it is then the code will go onto create the new book and if it isn’t (because that book title is already taken) then the code will issue a flash message telling the user to choose another name for the book title.

