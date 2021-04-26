---
layout: post
title:      "When Big O Does and Does Not Matter"
date:       2021-04-20 12:30:26 -0400
permalink:  when_big_o_does_and_does_not_matter
---
![header image for big O blog post](https://i.imgur.com/cUNNt64.jpg)
**Abstract:** *There are times when the big O notation of a programming algorithm will not predict performance in a meaningful manner, and then there are times when the opposite is true.&nbsp;  This article attempts to first illustrate why this is the case in abstract terms, and then show a strategy for selecting an optimal algorithm, or in some cases multiple algorithms, to be implemented in a software build.*

**Prerequisites:** [Jon Krohn's excellent video](https://www.youtube.com/watch?v=5yJ_QLec0Lc){:target="_blank"} on big O notation.&nbsp; Don Cowan has an excellent [summary table](https://www.donkcowan.com/blog/2013/5/11/big-o-notation){:target="_blank"} and Şahin Arslan has some great [JavaScript example code](https://dev.to/humblecoder00/comprehensive-big-o-notation-guide-in-plain-english-using-javascript-3n6m){:target="_blank"}.&nbsp;  Usman Malik has a [similar article with Python code](https://stackabuse.com/big-o-notation-and-algorithm-analysis-with-python-examples/){:target="_blank"} as well.&nbsp;  We will not repeat this material here, instead we'll try and explore some stuff that doesn't get as much attention.&nbsp;

Here we have all of the common big O notations graphed according to their base equations

[
![figure one](https://i.imgur.com/s8ym6sh.png)
](https://www.desmos.com/calculator/zuhpohsbtv){:target="_blank"}

The big O is less relevant as the x values approach zero

[
![figure two](https://i.imgur.com/vntUmT6.png)
](https://www.desmos.com/calculator/pdyismhsil){:target="_blank"}

So far, our graphs have only used these base equations for displaying big O:

|  Base Equation  | Big O Notation |
|--|--|
| y = n<sup>n</sup>   | O(n<sup>n</sup>) |
| y = (n!)| O(n!) |
| y = n<sup>3</sup>| O(n<sup>3</sup>) |
| y = 2<sup>n</sup> | O(2<sup>n</sup>)|
| y = n<sup>2</sup> | O(n<sup>2</sup>)|
| y = n log n | O(n log n)|
| y = n | O(n)|
| y = <span>&#8730;</span>n | O(<span>&#8730;</span>n)|
| y = log n | O(log n)|
| y = 1 | O(1)|

Let's look at what happens when our graph equations deviate from the base equations

[
![figure three](https://i.imgur.com/BrSBwi9.png)
](https://www.desmos.com/calculator/l3448fpf3v){:target="_blank"}

Now let's observe some more contrived examples.

[
![figure four](https://i.imgur.com/fhYXa4L.png)
](https://www.desmos.com/calculator/ttbfaf0beb){:target="_blank"}

As your computer programming functions become more complex, they start to deviate from the base equation trajectories (shown in the table above), and they take on more unpredictable shapes when graphed.

Now let's look at a hypothetical example where you have an app, like LinkedIn, and you want to do a search on all of the app users to find which users are (or ever have been) architects.&nbsp;  We can either search the user bios or user job titles to find occurrences of 'architect,' and keep in mind, (before we progress) that this is all a somewhat contrived example, because you'd be using a database for all of this and what follows isn't at all a "best practices" archetype, but rather, it's an abstraction to illustrate fundamentals.  So we have a Python dictionary with a couple of functions that search through it.&nbsp;

[
![link-one](https://i.imgur.com/MJ4NiLK.png)
](https://replit.com/@Richard_Burd/Big-0-Examples){:target="_blank"}

[
![figure five-point-one](https://i.imgur.com/EONrxOX.png)
](https://www.desmos.com/calculator/nosydzyl3d){:target="_blank"}

Now let's look at the same example, but pull things apart a little differently

[
![link-one](https://i.imgur.com/MJ4NiLK.png)
](https://replit.com/@Richard_Burd/Big-0-Examples){:target="_blank"}

[
![figure five-point-two](https://i.imgur.com/FCwYulo.png)
](https://www.desmos.com/calculator/nosydzyl3d){:target="_blank"}

The takeaway here is that big O really matters where scaling matters such as where you are doing an operation on all of your users, and you hope someday to have everybody in the world signed up as a user for your app.&nbsp;  Just imagine the following code:
```python
def prosess_payment_for_all_users(all_users_in_database):
```
You'd want to consider the big O for that function before implementing it.&nbsp;  But sometimes the big O doesn't matter because it isn't so relevant.&nbsp;  Shen Huang found something along these lines when he discovered a function with a big O of *O(n & log(n))* that was slower than another function doing the same work, but having a big O of *O(n<sup>2</sup>)*.&nbsp;  [Here is the raw code for his two functions](https://trinket.io/python/87a3166026){:target="_blank"} and you can read about it at the bottom of [this blog post](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/#Why-BigO-doesn%E2%80%99t-matter){:target="_blank"} under subsection 7: ***Why Big O doesn’t matter***.&nbsp;

Your computer programming functions can even have several nested subsections that each have their own trajectories; this can be especially true if your conditional statement evaluates an input variable.

![figure six](https://i.imgur.com/pi4rWuR.png)

Here are some trajectories, forget about equations and big O for a minute:

![figure seven](https://i.imgur.com/3N1q2Hv.png)

Say you wrote some code and then refactored it to make it read better; you want to know which code runs faster, the old version or the new one.&nbsp;  In the process you run into one of these problems:

 - *You know the big O for both code versions but suspect the one with the least efficient big O is actually the faster version.*

 - *You can't figure out the big O for one or both versions...maybe you have three versions or more*

If you run into this situation, here's what you do: you go onto [GeoGebra.org](https://www.geogebra.org/?lang=en)  and plot some test results you gathered from running your different code versions:

![figure eight](https://i.imgur.com/PPyfedA.png)

So imagine if we had some python code that looked like this:
```python
def python_human_height_function_one(height):
```
We already know that [human height is normally distributed](https://ourworldindata.org/human-height#height-is-normally-distributed){:target="_blank"}, so we don't care about this being able to scale (towards infinity) and instead we want the most efficient function that operates within accepting plausible human heights.&nbsp;

Here is a more realistic version of what plotting test results would look like, you'll have to plot your function performance and then do some [liner regression and/or curve fitting](https://www.youtube.com/watch?v=TmYl6k4e_AE){:target="_blank"}

![figure nine](https://i.imgur.com/CGcbRtu.png)

**Conclusion:** *Although some algorithms scale less efficiently, they may nonetheless be more appropriate for particular circumstances.&nbsp;  Every now and then, the optimal solution will even involve seemingly redundant algorithms working together.&nbsp;*
