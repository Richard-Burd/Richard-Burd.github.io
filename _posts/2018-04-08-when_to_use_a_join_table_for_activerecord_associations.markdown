---
layout: post
title:      "When to Use a Join Table for ActiveRecord Associations"
date:       2018-04-08 14:28:46 -0400
permalink:  when_to_use_a_join_table_for_activerecord_associations
---

I was recently asked if I could sketch up the difference between when you do and don’t use a join table for complex associations.  Let’s take a look at the join table below:
![Imgur](https://i.imgur.com/z5Kt8og.png)
So here we have a join table called ```post_category.rb``` represented by the blue box.  Notice the contiguous loop of arrows highlighted in yellow; if you start anywhere along this yellow path, you will trace it through all of the association statements back to where you started.  All of the code for these objects (and their analogous migration tables) are provided in the illustration.  Now let’s take a look at another project where a join table is *not* used:
![Imgur](https://i.imgur.com/6wmiDsb.png) 
Here we have the ```appointment.rb``` object model in the same place as our previous (blue colored) ```post_category.rb``` join table in the previous example.  What is the fundamental difference between this illustration and the previous one?  Simply put, the ```appointment.rb``` here is an actual thing; it is a full-fledged Ruby class object model that can accept Ruby instance methods.  It also has an analogous migration table (```CreateAppointments.rb```) that contains a row; in this case the ```datetime``` that converts an integer timestamp into a readable format with the month name.  If we wanted to, we could add the location of the appointment, we could also specify start & end times as well.  In effect, the appointment is a join table *with extra stuff going on* - but it uses the same logic (to bind together objects) as an actual join table.  To be sure, we could associate users to ```post_category.rb``` in the first example such that users follow specific post categories, but then it would be better to change the name of ```post_category.rb``` to something like ```topic.rb``` so we know this is no longer simply a join table. 

In sum, when you’re thinking out your associations you want to ask yourself if the object joining two other objects together a ‘thing’ or not.  If it’s not a thing than it’s just a simple join table…but if it’s a thing that does stuff (other than joining two other objects together) then it should be set up as a regular object model as is the case with the ```appointment.rb``` object model above.

