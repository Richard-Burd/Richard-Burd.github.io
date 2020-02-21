---
layout: post
title:      "How to Submit a form to a Rails API Created with Javascript or HTML"
date:       2020-02-21 20:10:25 +0000
permalink:  how_to_submit_a_form_to_a_rails_api_created_with_javascript_or_html
---


The curriculum for the front-end web development module has a lot of discussion about how to set up the `index` and `show` actions in the Rails controllers.  We even learn how to refactor the information in these controllers using serializes.  One thing I found consistently absent were discussions on how to set up a `create` action within the controllers themselves.  In the Pokemon-Teams-Lab, we learn how to `index`, `show`, and `destroy`, but there is no discussion on how to `create` because of the odd-ball nature of how this lab spawns the actual pokemons; it's a random process where the user does not choose to define any of the Pokemon's characteristics, but rather, the Pokemons self-generate their own parameters using some online thingamajig.

So if you would like to know how to set up a user-submittable form in the front end, (using Javascript or plain HTML) so that your user can define some characteristics of an object being created in the Rails API backend, you're in the right place.  To be sure, the Toy-Tale lab sort-of does this, but it doesn't use a Rails API, it uses a janky JSON server instead.

Rather that talking about how this works with words, and making you read boring text, I just make a graphical illustration instead, which you can click on below and enlarge.  Enjoy!


<a href="https://i.imgur.com/vRBiDHA.jpg"><img src="https://i.imgur.com/vRBiDHA.jpg" title="source: imgur.com" /></a>
