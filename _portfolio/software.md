---
layout: page
title: Software Development Projects
header-img: "img/banners/software.png"
exclude: true
---
<style>
  .media-icons-&-description{
  }

  .icon-container {
  }

  .description {
    font-style: italic;
  }

  .github-icon {
    height: 50px;
    float: left;
    margin-bottom: 30px;
  }

  .youtube-icon {
    height: 50px;
    padding-left: 10px;
    margin-right: 40px;
    margin-bottom: 30px;
  }

  @media only screen and (min-width: 500px) {
    .youtube-icon {
      float: left;
    }
  }
</style>

## Software Design / Development Portfolio
Welcome to the software section of my design portfolio.&nbsp; I recently graduated from the [Flatiron School's](https://flatironschool.com/){:target="_blank"} full stack web development program and below are three of my portfolio projects from the coursework, as well as some other things I am working on.&nbsp;  If your would like more information, please click on the GitHub icons below to go to the respective repo where the `README.md` file will contain greater detail.&nbsp; Each project also has a YouTube link to a recorded walk-through.

---
---

## Airborne Pallet Tracker App
<div class="media-Appicons-&-description">
  <div class="icon-container">
    <a href="https://github.com/Richard-Burd/front-end-portfolio-project" target="_blank">
      <img class="github-icon" src="/img/misc/github.svg" alt="">
    </a>

    <a href="https://www.youtube.com/watch?v=CoZzR6K59Gg" target="_blank">
      <img class="youtube-icon" src="/img/misc/youtube.svg" alt="">
    </a>
  </div>
  <p class="description">This single page application was built in pure JavaScript per assignment specifications and allows users to keep track of airborne shipping pallets</p>
</div>


The Airborne Pallet Tracker is my submission for the Flatiron School's [Front-end Portfolio Project](https://github.com/learn-co-students/js-spa-project-instructions-v-000){:target="_blank"}.&nbsp; This application was designed to help military & humanitarian logisticians keep track of airborne shipping pallets by color coating priority and weight classifications.&nbsp;  The user can keep track of how much space they have left in their storage areas, and decide which pallets have the highest priority to ship on the next available aircraft.

![app callouts & UX/UI design](https://i.imgur.com/ifnGo2x.jpg)

In order to reinforce fundamentals, this project had to be built in JavaScript alone *sans* any library or framework.&nbsp;  This led me to develop something I call the [builder-method](https://github.com/Richard-Burd/front-end-portfolio-project/blob/master/README.md#this-is-pure-javascript-by-design){:target="_blank"} in order to organize the massive amount of JavaScript code that resulted from this requirement.&nbsp;  The back-end of this application utilizes a [Rails API](https://github.com/rails-api/rails-api){:target="_blank"} that is shown below on the left in light-green boxes.&nbsp;  The JavaScript front-end is shown below on the right in light-blue boxes.

[
![schematic software diagram](https://i.imgur.com/28nI5ly.jpg)
](https://drive.google.com/file/d/1NrvuzRWSfcoiCbybQw29HBd4O9ObTcpo/view?usp=sharing){:target="_blank"}

---
---

## ArduPlane Drone App
<div class="media-icons-&-description">
  <div class="icon-container">
    <a href="https://github.com/Richard-Burd/react-redux-portfolio-project" target="_blank">
      <img class="github-icon" src="/img/misc/github.svg" alt="">
    </a>

    <a href="https://www.youtube.com/watch?v=hYASLZsfUOw" target="_blank">
      <img class="youtube-icon" src="/img/misc/youtube.svg" alt="">
    </a>
  </div>
  <p class="description">This app utilizes React & Redux per assignment specifications and lets users of the ArduPilot software modify their drone parameters and see what those changes look like in a responsive GUI</p>
</div>

The ArduPlane Drone App is my submission for the Flatiron School's [React-Redux Portfolio Project](https://github.com/learn-co-students/react-redux-assessment-v-000){:target="_blank"}.&nbsp; This app is designed to be an interactive parameter editor for the [ArduPlane](https://ardupilot.org/plane/){:target="_blank"} open source software suite. This software provides autonomous control for unmanned aerial vehicles (UAV's) and has several, [customizable parameters](https://ardupilot.org/plane/docs/parameters.html){:target="_blank"} that can be adjusted so as to tailor the software to a specific UAV body, or **airframe** in aviation jargon.&nbsp; This app is designed to be an interactive parameter editor for the ArduPlane open source software suite. This software provides autonomous control for unmanned aerial vehicles (UAV’s) and has several, customizable parameters that can be adjusted so as to tailor the software to a specific UAV body, or airframe in aviation jargon.

The default ground station control applications for ArduPilot are [Mission Planner](https://github.com/ArduPilot/MissionPlanner){:target="_blank"} and [APM Planner](https://github.com/ArduPilot/apm_planner){:target="_blank"}.&nbsp; Unfortunately, they both contain poor GUI's for parameter adjustments which inspired the idea for this project.  

![UX/UI design of the ardupilot app](https://i.imgur.com/FtbLpaB.jpg)

This application utilizes the [React Router](https://reactrouter.com/web/guides/quick-start) to create RESTful routs in lieu of a single page application.&nbsp;  It also makes use of both functional as well as container components, and Redux to manage state .&nbsp;  A Rails API completes the backend where users can store their parameter settings for later use.

![high level software architecture diagram](https://i.imgur.com/uyd91GW.jpg)

---
---

## Convoy Planner App
<div class="media-icons-&-description">
  <div class="icon-container">
    <a href="https://github.com/Richard-Burd/rails-portfolio-project" target="_blank">
      <img class="github-icon" src="/img/misc/github.svg" alt="">
    </a>

    <a href="https://www.youtube.com/watch?v=z9hnfbXvxCs" target="_blank">
      <img class="youtube-icon" src="/img/misc/youtube.svg" alt="">
    </a>
  </div>
  <p class="description">This Ruby-on-Rails application showcases back-end design features and lets a user figure out how far their convoy can travel before running out of gas</p>
</div>

The Convoy Planner App is my submission for the Flatiron School's [Rails Portfolio Project](https://github.com/learn-co-students/rails-assessment-v-000){:target="_blank"}.&nbsp; The focus of this assignment is building RESTful routes using [Embedded Ruby](https://docs.ruby-lang.org/en/2.3.0/ERB.html){:target="_blank"} (ERB) to build out a minimum viable front-end, while utilizing the MVC Rails architecture for a highly capable back-end.&nbsp; The back-end features several highly collaborative objects, strict controls on user permissions, a secure user login with OmniAuth and the ability to validate user passwords with encryption.

![UX/UI design of convoy planner rails app](https://i.imgur.com/HDSKXNa.jpg)

The diagram below maps out the entire full stack down to the method (function) level.&nbsp;  This gives each Ruby method a graphical representation, usually in the form of an ellipse.&nbsp;  The symbol legend on the right side color-codes the methods according to their type and purpose within the stack.&nbsp;  Critical information for using Rails is highlighted in pink for reference on future projects.&nbsp;  

[
![detailed software architecture diagram](https://i.imgur.com/EAtixUM.jpg)
](https://drive.google.com/file/d/1e8ewC92UAdCqh_GlDWcJuzHGtX7Eg6ZD/view?usp=sharing){:target="_blank"}

---
---

## Cheat Sheets for Languages & Frameworks
For me, the most frustrating part of software development is keeping track of how to do things in all of the different languages & frameworks we use; it is simply too easy to forget how systems work when you are not using them regularly.&nbsp;  To solve this problem I developed a *system* of cheat sheets that involves the following three steps:
1. Watch a series of YouTube tutorials on a new language or framework and create a commensurate repository to write sample code and take notes.
2. Utilize the notes and sample code to create a cheat sheet on how the language (or framework) works, forcing you to show yourself that you understand the material.
3. Dedicate a monitor (in your workspace) for displaying the cheat sheet when using *that* language or framework in a project down the road, and iterate on the cheat-sheet to improve it as you make use of it.

The process can be used on a team's specific technology stack as well; the objective is to create references that are quicker than Google or Stackoverflow so you can get things done faster.&nbsp;  I no longer worry about remembering details on ***how*** to do things because I know ***where*** those details are elucidated in my reference library.&nbsp;  Here are some cheat sheets from the library:
<br/>
<br/>
### TypeScript
The GitHub repository for this cheat sheet is [here](https://github.com/Richard-Burd/typescript-sandbox){:target="_blank"}
[
![preview of a TypeScript cheat sheet](https://i.imgur.com/UUCN0ER.jpg)
](https://drive.google.com/file/d/1TsXNU8dgclsMJDegvNkv3W6qUnM8pUCt/view?usp=sharing){:target="_blank"}
<br/>
<br/>
### Python
The GitHub repository for this cheat sheet is [here](https://github.com/Richard-Burd/python-3-sandbox){:target="_blank"}
[
![preview of a Python cheat sheet](https://i.imgur.com/2FjckVW.jpg)
](https://drive.google.com/file/d/1l2QqzHdfAmrQxy3aPAzy6UsL8Ol36hHZ/view?usp=sharing){:target="_blank"}
<br/>
<br/>
### React Hooks
The GitHub repository for this cheat sheet is [here](https://github.com/Richard-Burd/react-redux-sandbox){:target="_blank"}
[
![preview of a React Hooks cheat sheet](https://i.imgur.com/0EcqUq1.jpg)
](https://camo.githubusercontent.com/0873849d4c76d9234c2af971f546dd96019c5c28597f1efe7a753aa70f055c73/68747470733a2f2f692e696d6775722e636f6d2f304563715571312e6a7067){:target="_blank"}
