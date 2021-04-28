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

Now let's look at a couple of sheep-counting functions and see what they do; here's a Python function with a big O notation of O(n<sup>2</sup>):
```python
def quadratic_function(sheep):
  counter = 0
  for loop_1 in sheep:
    for loop_2 in sheep:
    counter = counter + 1
    time.sleep(0.02)
    print(f'{counter} .) little quadratic sheep...')
```
And here's one with a big O notation of O(n<sup>3</sup>):
```python
def cubic_function(sheep):
  counter = 0
  for loop_1 in sheep:
    for loop_2 in sheep:
      for loop_3 in sheep:
      counter = counter + 1
      time.sleep(0.001)
      print(f'{counter} .) little cubic sheep...')
```
By now we know quadratic functions scale better than cubic ones, but this use case throws in a monkey wrench: the `time.sleep()` in the quadratic function specifies more time than in the cubic one; this slows the quadratic one down a bit on each function call.&nbsp;  The intent is to show a simplified example of what you can encounter in more complex real-world examples: *it is possible to have a function with a better-scaling big O notation perform worse within a given range of input variables.*&nbsp;  Let's have a look at the code:

[
![link to the repl.it workspace](https://i.imgur.com/EFh2HB9.png)
](https://replit.com/@Richard_Burd/Big-0-Examples){:target="_blank"}

...and here's a trinket for all of you who hate repl.it:
[
![link to the trinket.io workspace](https://i.imgur.com/aJuYbrk.png)
](https://trinket.io/python3/3fa1fd86f5){:target="_blank"}

By changing the `my_sheep` value, you can send that integer count to both functions simultaneously; here are the results of a time test below, showing how long the two functions take to execute given a range of different variable input values:

|  `my_sheep`| O(n<sup>2</sup>) Time |O(n<sup>3</sup>) Time | Fastest
|--|--|--|--|
| 2 | 0.08 | 0.01 | O(n<sup>3</sup>)
| 4 | 0.32 | 0.07 | O(n<sup>3</sup>)
| 6 | 0.76 | 0.30 | O(n<sup>3</sup>)
| 8 | 1.31 | 0.59 | O(n<sup>3</sup>)
| 12 | 2.96 | 2.29 | O(n<sup>3</sup>)
| 16 | 5.23 | 5.13 | O(n<sup>3</sup>)
| 20 | 8.11 | 9.58 | <b>O(n<sup>2</sup>)</b>
| 24 | 11.64 | 15.95 | <b>O(n<sup>2</sup>)</b>
| 32 | 20.85 | 41.42 | <b>O(n<sup>2</sup>)</b>
| 40 | 32.30 | 74.27 | <b>O(n<sup>2</sup>)</b>

Right away we see something strange; between the `my_sheep` value being set to 16 and 20, the winner and looser (timewise) flop!&nbsp;  To see this better, let's look at this same data graphed in GeoGebra:

[
![link to the GeoGebra Workspace](https://i.imgur.com/AvuumxV.png)
](https://www.geogebra.org/graphing/mnyhpc4v){:target="_blank"}

The `quadratic_function` is blue and the `cubic_function` is red.&nbsp;  Right around the intersection point of ***x=16.68, y=5.67*** we can see the swap taking place.&nbsp;  So which function is better!?&nbsp;  The answer is: ***it depends on how many sheep you need to count.*** &nbsp;  If your broader program is of a nature that you will never need to count more than 12 sheep, you could go with the `cubic_function` because it does  a better job counting between 1 and 12 sheep.&nbsp;  Conversely, if you wanted to count more than 12 sheep, the `quadratic_function` would be your choice.&nbsp;


The takeaway here is that big O really matters where scaling matters, and if you needed to count ten thousand sheep, then obviously you would go with the `quadratic_function`.&nbsp;

Now let's say you had a web app, and you were doing an operation on all of your app users.&nbsp;   Imagine if your CEO told you that they expected everyone in the world to become a user of this app in the next month, and that you needed to be ready for that.&nbsp;  Just imagine the following code:
```python
def prosess_payment_for_all_users(all_users_in_database):
```
You'd want to consider the big O for that function before implementing it!&nbsp;

Sometimes the big O doesn't matter because it isn't so relevant.&nbsp;  Shen Huang found something along these lines when he discovered a function with a big O of *O(n & log(n))* that was slower than another function doing the same work, but having a big O of *O(n<sup>2</sup>)*.&nbsp;  [Here is the raw code for his two functions](https://trinket.io/python/87a3166026){:target="_blank"} and you can read about it at the bottom of [this blog post](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/#Why-BigO-doesn%E2%80%99t-matter){:target="_blank"} under subsection 7: ***Why Big O doesn’t matter***.&nbsp;

It should be obvious by now that big O *does* matter, but not all of the time, and not for every function in your software build.&nbsp;  The key concept is scaling and what happens before infinity:

[
![figure five](https://i.imgur.com/NBFLfzs.png)
](https://www.desmos.com/calculator/ejozxwxij8){:target="_blank"}



Now let's look at some cases where big O doesn't matter as much.&nbsp; You could have a programming function with several nested subsections that each have their own trajectories; this can be especially true if your conditional statement evaluates an input variable:

![figure six](https://i.imgur.com/WJtonIF.png)

The big O of this function wouldn't be very useful.&nbsp;

Now here are some trajectories to consider, forget about equations and big O for a minute, and let's think more abstract:

![figure seven](https://i.imgur.com/3N1q2Hv.png)

Say you wrote some code and then refactored it to make it read better; you want to know which code runs faster, the old version or the new one.&nbsp;  In the process you run into one of these problems:

 - *You know the big O for both code versions but suspect the one with the least efficient big O is actually the faster version, given the input variable(s) your working with*

 - *You can't figure out the big O for one or both versions...maybe you have three versions or more*

If you run into this situation, here's what you do: you go onto [GeoGebra.org](https://www.geogebra.org/?lang=en)  and plot some test results you gathered from running your different code versions, like we just saw with the sheep counting example above, then you box-in your results into something that looks like this:

![figure eight](https://i.imgur.com/PPyfedA.png)

Regarding the stochastic analysis, imagine if we had some python code that looked like this:
```python
def python_human_height_function(height):
```
We already know that [human height is normally distributed](https://ourworldindata.org/human-height#height-is-normally-distributed){:target="_blank"}, so we don't care about this being able to scale (towards infinity) and instead, we want the most efficient function that receives *plausible* human heights.&nbsp;  While the the stochastic analysis of input variables is important, it is outside the scope of this big O discussion, but you should be aware of it when trying to find an optimal function.&nbsp;

Here is a more realistic version of what plotting test results would look like, you'll have to plot your function performance and then do some [liner regression and/or curve fitting](https://www.youtube.com/watch?v=TmYl6k4e_AE){:target="_blank"}

![figure nine](https://i.imgur.com/CGcbRtu.png)

In the above diagram we are seeing the lines as blurred because frankly, there are several *'mathy'* way to draw those lines.&nbsp;  In the sheep counting example above, I used GeoGebra's [FitPoly](https://wiki.geogebra.org/en/FitPoly_Command) command to calculate the regression polynomial of the same degree as my function's exponent but there are other methods for doing this.&nbsp;  They too are outside the scope of the discussion, but be aware they exist.&nbsp;

**Conclusion:** *Although some algorithms scale less efficiently, they may nonetheless be more appropriate for particular circumstances.&nbsp;  Every now and then, the optimal solution will even involve seemingly redundant algorithms working together.&nbsp;*
