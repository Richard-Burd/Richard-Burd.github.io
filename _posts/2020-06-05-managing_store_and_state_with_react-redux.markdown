---
layout: post
title:      "Managing Store & State with React-Redux"
date:       2020-06-05 23:51:23 +0000
permalink:  managing_store_and_state_with_react-redux
---

While working on my final project in the online web developer curriculum I encountered more difficulty with Redux than with anything else.&nbsp;  The core problem was our requirement to use a central Redux store in order to manage state, while also utilizing a backend Rails API to sent & receive data.&nbsp;  I kept thinking to myself: *'what do I need this central Redux store for!?'*   I could just import data to a component's state and make the necessary changes...then at another point in time, when editing some other thing, I could just hit up the server  once again and ask for some fresh data and edit that data accordingly.

<p>

I ended up with a sort-of compromise where I asked my React components to request server data using a central Redux store, but then when changes were made to that data, the server was accessed directly with a page refresh following the interaction.&nbsp;  In this way, the flow went from react to server to store and back to react again in a singular flow.  I'm not sure if this is what the instructors intended but it turned out architecturally easy to manage.&nbsp;  Don't worry, below I have lots of cool graphics to explain all of this.

## The Problem Being Solved

First a little bit about the app itself.&nbsp; It is designed to be an interactive parameter editor for something called the [ArduPlane](https://ardupilot.org/plane/) open source software suite.&nbsp; This software provides autonomous control for unmanned aerial vehicles (UAV's) and has several, [customizable parameters](https://ardupilot.org/plane/docs/parameters.html) that can be adjusted so as to tailor the software to a specific UAV body, or what we would call an **airframe** in aviation jargon.&nbsp;  Users of this software have two problems that this app must consider:

 1. Users are often adjusting their parameters in places with poor internet connection such as those out in a field environment.  
 2. Users often tweak their parameters between flight tests in the field but cannot remember which parameters do exactly what.

The main objective of this app is to address the latter while keeping in mind the former as a significant design consideration.

![](https://ardupilot.org/application/files/8714/8419/9139/2048x1536-1.jpg)
*a team of drone technicians getting ready for takeoff somewhere outside*
<p>

In order to adjust the aforementioned parameters, users interact with a not-so intuitive GUI designed for simplicity and parsimony.&nbsp;  Here is an example of what they're looking at:

![enter image description here](https://ardupilot.org/plane/_images/missPlannTuningTECS.png)

Because the interface is so basic, users often struggle to keep track of which parameters do what and so they end up making cheat-sheets like this one I put together several years ago:
![Imgur](https://i.imgur.com/yzeb0vr.png)

So then, this app is designed to be a graphically intuitive, ArduPlane parameter editor guide that does what this 2D graphic above does, but interactively!&nbsp;  In sum, the app provides a user with graphics that *illustrate* what each parameter does and how changing *that* parameter will effect outcomes with responsive, animated graphics.

<p>

To be sure, this app is in no way ready for first flight since it is a v.0.1 demonstrator.&nbsp;  The Arduplane software has somewhere around 90 flight-parameters and all this app does is create, read, update, and delete (**CRUD**) three of them, along with an associated airframe.&nbsp;  Even with this small delivery, the number of React components used to create this app far exceed the [project requirements](https://learn.co/tracks/full-stack-web-development-v8/module-17-redux/section-5-redux-final-project/react-redux-portfolio-project).&nbsp;

## Let's Look at the App Itself
The app let's a user CRUD an airframe with a name & some basic info.&nbsp;  When an airframe is created, a default set of 3 parameters are also created for, and associated with,  that same airframe.&nbsp;  These parameters control the airframe's maximum allowable [pitch, roll, and yaw](https://en.wikipedia.org/wiki/Aircraft_principal_axes) while in an [autonomous flight mode](https://ardupilot.org/plane/docs/flight-modes.html):&nbsp; 

![Imgur](https://i.imgur.com/FtbLpaB.jpg)

The three parameters are edited on the ***/airframes/:id/params***  path as shown in the lower right-hand box in the illustration above.&nbsp;  There are three interactive graphics that change orientation as the user manipulates their values.  This allows the user to *see* what their changes are doing rather than having to remember specifics they read way back from the boring [documentation](https://ardupilot.org/plane/docs/parameters.html).&nbsp;
<p>

While manipulating these parameters, the user is sending their changes to a local React component state on the front-end, rather than the Redux store.  Only when the user *saves* their changes are those changes sent to the server.  The user only grabs data from the server whenever absolutely necessary since they will likely be in a field environment far away from solid internet access:&nbsp; 


![Imgur](https://i.imgur.com/CQg659p.jpg)

When putting this together initially, It made sense to update the Redux store first (with user changes) and then dispatch an action request to update the back-end Rails API server as well.&nbsp;  This turned out to be less than ideal because it meant that, for at least some short duration of time, the store and server would not be synchronized.&nbsp;  This meant that the communication between store and server had to be monitored carefully and 'babysat' when new changes were made.&nbsp;  The solution was to create two, completely separate, one-way communication paths as shown below.&nbsp;  First let's discuss the path on the left-side of the diagram shown with grey arrows that say *request* and *read*:


![Imgur](https://i.imgur.com/OOAT9L4.jpg)
What's happening here is that the React functional components (such as `AirframeData.js` ) are sending requests for data to the Redux layer, and the Redux layer in turn grabs the appropriate data from the server, and then puts it in the proper place within the central Redux store.&nbsp;  Now something entirely different goes on when a user persists to the back-end database.&nbsp;  Let's look at the grey arrows on the right-hand side of the diagram above; there we have the user creating, updating, and deleting data on React container components like `Airframe.js` & `AirframeForm.js` that use a React class component's local state rather than a central Redux store.&nbsp; Once those actions are sent to the appropriate Redux action controller, that action controller bypasses the Redux reducers and store altogether so it can go straight to the back-end server.&nbsp;  This is immediately followed by a page reload and now the server and store are always synced with changes traveling unidirectionally, from server to store and never the other way around.&nbsp;  This makes expansion and manipulation of the code base much easier because we are only keeping track of persistence in one direction as opposed to two.&nbsp;  The philosophy here is: *if the user hasn't saved their changes, the store doesn't care to know about it yet.*

<p>

All in all this meets the project requirements and maximizes the utility of both Redux and the Rails back-end API.&nbsp;  If I learned anything from this project it was that the dimension of *time* is still quite hard to keep track of and effectively manage.&nbsp;  Therefore, anything I can do to simplify the architecture of sequences will be useful down the road.
