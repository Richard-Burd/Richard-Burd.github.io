---
layout: post
title:      "Limits of Big O Notation"
date:       2021-04-20 12:30:26 -0400
permalink:  limits_of_big_o_notation
---

**Abstract:** *There are times when the big O notation of a programming algorithm will not predict performance the way many developers expect it to.&nbsp;  This article attempts to first explain why that is in abstract terms, and then offer a strategy for selecting an optimal algorithm (or multiple algorithms working together) to be implemented in a software build.*  



Let's start out by looking at a screenshot from [Jon Krohn's excellent video](https://www.youtube.com/watch?v=5yJ_QLec0Lc){:target="_blank"} on big O notation which I would recommend watching if you are totally unfamiliar with this topic:

![big o notations arranged on a grid by Jon Krohn](https://i.imgur.com/pUzkOKi.png)

Many lessons on big O will show something similar to this with the idea of conveying one simple truth: there exists a spectrum of big O notations that can be arranged from the least efficient scaling to the most efficient scaling, and in our case above, O(n!) would scale with the least amount of efficiency while O(log n) would scale with the most efficiency.&nbsp;  In this way, if I have two computer programming functions that do the exact same thing, and I must choose to use one of them in my software build, and all I know about these two computer programming functions is that one of them has a big O notation of O(n<sup>2</sup>) while the other has a big O notation of O(n), then I should choose to implement the one with the O(n) notation.&nbsp;  The whole point of this article is show why that isn't always true, and to explore how one might go about selecting the most efficient option for implementation.&nbsp;  I will specify *computer programming* functions when discussing actual code so as not to confuse them with the *mathematical* functions we will be looking at below.&nbsp;

In *Figure-1* below we have a series of functions you can view [here on desmos.com](https://www.desmos.com/calculator/nuzg9tvbl9){:target="_blank"} in more detail.

[
![figure one](https://i.imgur.com/qxVkPQr.png)
](https://www.desmos.com/calculator/dw6per4vkt){:target="_blank"}

The takeaway here is that we can observe two mathematical functions with a big O notation of *O(n<sup>2</sup>)* that scale worse than the function with a big O notation of *O(n!)*.&nbsp;  At the same time, we can also see three mathematical functions where the opposite is true.&nbsp;  Now to be sure, all of the *O(n<sup>2</sup>)* functions will scale better than the single *O(n!)* function ***if*** all of the the x and y values (on the grid) were to go to infinity.&nbsp;  Now imagine two computer programming functions that followed trajectories similar to what is shown above; in such a circumstance, the computer programming function with the optimal big O notation might not be the most efficient one within the space shown.&nbsp;

Now let's consider the following python pseudocode in figure 2 below:

![figure two](https://i.imgur.com/2eJX9KL.png)

Here we see what can happen when conditionals are introduced; the big O of our `python_function()` is basically useless and doesn't tell us anything about our overall performance.&nbsp; This is because the big O here is only relevant when the input variable (x) has a value greater than or equal to 10, and is also less than 20, and yet the `python_function()` accepts values above and below that range.&nbsp;   A rule of thumb here is that: *if and when a function contains conditionals that evaluate its own input variable, the big O notation of that function might not be useful for evaluating efficiency*.&nbsp;  Instead, we would want to valuate the subcomponents of that function separately.&nbsp;

Now let's take a look at a bird's eye view of big O notation in figure 3 below:

[
![figure three](https://i.imgur.com/bXoHRT0.png)
](https://www.desmos.com/calculator/zuhpohsbtv){:target="_blank"}


This is similar to Jon Krohn's Microsoft-paint-sketch introduced at the beginning of this blog post, but it is a bit more comprehensive and contains more big O notations.&nbsp;  You can view these same math functions [here on desmos.com](https://www.desmos.com/calculator/wanscrgyzq){:target="_blank"} where you can zoom in and out to see how they better relate to each other.&nbsp;  In that workspace you'll see these simplest equations that correspond to the big O notations on the right below :

|  Simplest Equation  | Big O Notation |
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

Figure 3 above uses these 'simplest' equations to graph the various big O notations displayed therein.&nbsp;  Note that it does not use more complex equations like Figure 1 above, or Figure 5 below.&nbsp;

There are already several great articles describing the big O notations for various programming operations.&nbsp;  Don Cowan has an excellent [summary table](https://www.donkcowan.com/blog/2013/5/11/big-o-notation){:target="_blank"} and Şahin Arslan has some great [JavaScript example code](https://dev.to/humblecoder00/comprehensive-big-o-notation-guide-in-plain-english-using-javascript-3n6m){:target="_blank"}.&nbsp;  Usman Malik has a [similar article with Python code](https://stackabuse.com/big-o-notation-and-algorithm-analysis-with-python-examples/){:target="_blank"} as well.&nbsp;  We will not repeat this material here but instead try and answer two questions:

*If I have multiple (computer programming functions I can implement into a software build, but I am not sure what the big O notations for all of them are, how would I go about selecting the most optimal function?*

*If I do know the big O notations for my algorithms, should I just implement the one with the best big O notation, i.e. the big O that scales the most efficiently?&nbsp;*

***This section is under development***


[
![figure four](https://i.imgur.com/R1KMZ4u.png)
](https://www.desmos.com/calculator/lvfipf0q6p){:target="_blank"}
***This section is under development***
[
![figure five](https://i.imgur.com/gb6yr7k.png)
](https://www.desmos.com/calculator/1hqyvyveh6){:target="_blank"}

OK, so at this scale we start to see some problems.&nbsp;  In the space shown above, the (math) functions are intersecting each other all over the place, let's see what the implications of that are in figure 5 below:

![figure six](https://i.imgur.com/1sQ3XE3.png)

So here we see that at this scale, different big O notations have efficiencies that are at variance with what they would be at, say, infinity.&nbsp;  Now how would we find out the different efficiencies for multiple functions, and would we use big O?&nbsp;  Let's look at figure six below.  In figure 6 we have different (competing) functions plotted out to see which one is the best for our purposes:

![figure seven](https://i.imgur.com/OFGpLrF.png)

What the heck are we in need of a stochastic analysis for!?&nbsp;  Let's say we had a function to analyze different human beings based on their individual height, and that we passed these heights into a function that looks something like this:
```python
def python_human_height_function_one(height):
```
In this situation, we already know that [human height is normally distributed](https://ourworldindata.org/human-height#height-is-normally-distributed){:target="_blank"}, and so if we had to choose between two functions that accomplish the same calculation on a human height, but that do so using different methods (and that also have different big O notations) we would want to know which of the two functions works best with human heights that are likely to be entered into the function.&nbsp;  For example, I know some people are taller than 7 feet but there are very few such people, and thus, I wouldn't choose a function that worked faster for people above 7 feet, but much slower for people under 5 because I'm more likely to have the latter than I am the former.&nbsp;

The truth is that when your trying to choose what function to use among a competing set of functions, the big O notation really doesn't tell you much at all in terms of which function you should choose, ***this is because the input variables you'll be passing to those functions will not necessarily result in the y-axis reaching infinity***.&nbsp;  Shen Huang found something along these lines when he discovered a function with a big O of *O(n & log(n))* that was slower than another function doing the same work, but having a big O of *O(n<sup>2</sup>)*.&nbsp;  The raw code for his two functions is available [here](https://trinket.io/python/87a3166026){:target="_blank"} and you can read about it at the bottom of this blog post [here](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/#Why-BigO-doesn%E2%80%99t-matter){:target="_blank"} under subsection 7: ***Why Big O doesn’t matter*** .&nbsp;


In the next figure, we see a more accurate depiction of what you would get if you were to do this sort-of experiment in a real world setting:

![figure eight](https://i.imgur.com/JyToYfz.png)

You can use an online tool like [GeoGebra](https://www.geogebra.org/){:target="_blank"} to plot your function performance and then do either [liner regression or curve fitting](https://www.youtube.com/watch?v=TmYl6k4e_AE){:target="_blank"}, depending on what you need.&nbsp;  For example, the `third_function` above (green path) would need some curve fitting because it angles sharply (around the point where x=26.5) whereas the `second_function` (blue path) would call for some linear regression because it is more or less a straight line.&nbsp;  The latter has a linear trajectory whereas the former has polynomial one.&nbsp;  The `first_function` appears to follow an exponential path but within the bounded area we are operating on it, it is pretty close to straight as well so you could do linear regression on the red dots and then use the subsequent line to find the intersection with the `second_function`(blue path) line.&nbsp;
