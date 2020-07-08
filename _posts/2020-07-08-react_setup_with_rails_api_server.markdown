---
layout: post
title:      "React Setup with Rails API Server"
date:       2020-07-08 14:51:00 -0400
permalink:  react_setup_with_rails_api_server
---

This walkthrough describes the process for setting up a Ruby on Rails (back-end) API server to work with a front-end React app.  This was used to create this project [here](https://github.com/Richard-Burd/react-redux-portfolio-project).&nbsp; When properly set up, you will be able to go into your new application's main directory and run `$ rails start` to boot up both the front & back ends simultaneously.&nbsp; As always, let's do this through pictures:

![enter image description here](https://i.imgur.com/AXxXSBS.jpg)

The two gems you need to copy & paste here are:
```
gem 'rack-cors', '~> 1.1.1'
gen 'foreman', '~> 0.82.0
```
...feel free to try newer versions if available...these are what I used.  Next, we need to go in and change some of the Rails boilerplate code:

![enter image description here](https://i.imgur.com/40Oh6XP.jpg)
Here is the block of code shown above...copy & paste it into ./config/application.rb as shown above.
```
config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'
    resource '*', headers: :any, methods: [:get, :post]
  end
end
```
Next, create the following directory:&nbsp;&nbsp;**./lib/tasks/start.rake** &nbsp;&nbsp;...then copy & paste this code into it:
```
task :start do
  exec 'foreman start -p 3000'
end
```
Now when you run **$ rails start** the program should boot and you should be able to navigate to both the front & back ends as shown below.
![enter image description here](https://i.imgur.com/C0vGLhY.jpg)
If you would like more detailed information on this setup, see this blog post [here.](https://www.newline.co/fullstack-react/articles/how-to-get-create-react-app-to-work-with-your-rails-api/)&nbsp; It goes into more detail than this quick-reference guide blog-post.&nbsp;  Note that the author there does not utilize the ***rack-cors*** ruby gem, and I do not use the author's recommendation for [setting up the proxy](https://www.newline.co/fullstack-react/articles/how-to-get-create-react-app-to-work-with-your-rails-api/#setting-up-the-proxy).&nbsp;That said, they more or less accomplish the same thing.
