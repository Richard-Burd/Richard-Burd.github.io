---
layout: post
title:      "Using Flash Messages to Generate Errors on Multiple Pages (Sinatra)"
date:       2018-03-08 18:38:12 -0500
permalink:  using_flash_messages_to_generate_errors_on_multiple_pages_sinatra
---


If you are building a Sinatra app and you want to use Rack::Flash to generate all of your warning messages displayed to your users, then this is the blog post for you.  Below I will walk you through how to set this all up and get it running.  To be sure, the Learn.co (Flatiron) curriculum *sort-of* covers this [here]( https://learn.co/tracks/full-stack-web-development-v3/sinatra/activerecord/sinatra-playlister) but I will cover these additional topics:
* How to get flash installed properly
* Displaying the right message(s) on the correct views.
* Refactoring the code used to trigger your messages

I have this implemented in my Sinatra portfolio project available [here]( https://github.com/Richard-Burd/sinatra-portfolio-project) for reference.  First go to your Gemfile and add the gem: ` gem "rack-flash3"`  Next, go into your application controller and add the following block: ` use Rack::Flash` this can be put anywhere but I have it in the `configure` block:
```
  configure do
     use Rack::Flash
     set :public_folder, 'public'
     set :views, 'app/views'
     enable :sessions
     set :session_secret, "fwitter_secret"
  end
```
…you will also need to `enable :sessions` somewhere in the controller as shown above.

The final two steps are setting a place for the message to appear in the view as well as establishing the conditions for that message to appear in the controller; let’s do the latter first.  If you look at [./app/views/users/create_user.erb]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/views/users/create_user.erb) you will see the flash message designated on lines 5 through 7:
```
   <% if flash.has?(:signup_page_message) %>
    <%= flash[:signup_page_message] %>
   <% end %>
```
Now the important thing here is the variable name `signup_page_message`  you can name this variable anything you want but each view (i.e. the actual erb file) should have its own unique variable name set to a flash message that it *does not share* with any other flash message on any other view.  This is important because if the message *does* trigger, it will stay in memory, and each time you go to a new page in the web app, the flash message will render if it finds the `flash.has?` block shown above.  If we look at the login page at [./app/views/users/login.erb]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/views/users/login.erb) for example, we can see that the flash message variable is set to `message_for_login_page` - this ensures that the message being passed to it is intended to be viewed only on the login page.  Finally, let’s have a look at lines 14 to 7 on the [./app/controllers/users_controller.rb]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/controllers/users_controller.rb): 
```
post '/signup' do
  if params[:username] == "" || params[:email] == "" || params[:password] == ""
  flash[:signup_page_message] = "Sorry, can you make sure to fill out all three fields: Name, Email, and Password?"
  redirect to 'signup'
end
``` 
Here we have a condition wherein if a new user signing up fails to fill out all three fields (username, email, and password) they will receive an error message telling them what they did wrong.  This error message will only show up on the signup page (`create_user.erb` is the view of this page) and nowhere else.  If we look at lines 48 and 49 we see another flash message in the `post ‘/login’` request:
```
flash[:message_for_login_page] = "Oops, your username & password combo is incorrect; click here to sign in as a new user."
erb :'users/login'
```
…the difference here is that now we are defining the flash message input parameter as ` message_for_login_page` instead of ` signup_page_message`.  This means that the code in the block above will only render if (and when) the warning message is fired and only on the login page where this parameter is defined [here]( https://github.com/Richard-Burd/sinatra-portfolio-project/blob/master/app/views/users/login.erb#L5):
```
<% if flash.has?(:message_for_login_page) %>
  <a href="/signup"><%= flash[:message_for_login_page] %></a>
<% end %>
```
…and thus, this message will not render (under any circumstances) on the signup page.


**Bottom Line**

Don’t put this code in any of your erb files:
```
<% if flash.has?(:message) %>
  <%= flash[:message] %>
<% end %>
```
…because simply defining all this variable as `message` will cause messages you intended for one view to show up on other views as well.  Be specific with defining this variable as belonging to the view you want it to render on.

