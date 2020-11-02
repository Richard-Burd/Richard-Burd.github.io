---
layout: post
title:      "Longest Common Subsequence"
date:       2020-11-01 12:44:26 -0400
permalink:  longest_common_subsequence
---

Until very recently my illustrations have focused on stack architecture and reference guides.&nbsp;  My latest endeavor involves the creation of visual aids that work towards solving the toughest algorithmic problems, that is, I am not looking here to illustrate large code bases involving APIs & multiple stacks, but rather, to illustrate a single algorithm that must solve some sort of difficult problem...and to date, I haven't really done anything like this.&nbsp;  I am still in the process of creating such a *system* so I have not yet arrived at a final destination, stay tuned for the final product in a future post.&nbsp;  

Okay, so l only go big or go home, therefore we're gonna start with a tough coding problem called the ***longest common subsequence***, or 'LCS' for short.&nbsp; Apparently [Google uses LCS in hiring interviews](https://www.youtube.com/watch?v=10WnvBk9sZc){:target="_blank"} so it is an ideal place to start trying to figure out how to graphically visualize complex algorithms.&nbsp;  The basic idea it to take two inputs, what we'll call `string1` and `string2`, and find the longest sequence of characters that are common to both of these values.&nbsp;  In this example, I will be working in JavaScript and the input values will look like this:
```
const string1 = "rqvjtweyrztuyio";
const string2 = "qzxwevrtbyrw";
```

There is a live REPL [here](https://repl.it/@Richard_Burd/Longest-Common-Subsequence#index.js){:target="_blank"} and a Git repo [here](https://github.com/Richard-Burd/longest-common-subsequence){:target="_blank"} for reference, and both use the aforementioned input values.&nbsp;

My goal is to create an algorithm that is similar to this [Dynamic Programming](https://rosettacode.org/wiki/Longest_common_subsequence#Dynamic_Programming_4){:target="_blank"} solution.&nbsp; I am still not sure exactly how this algorithm works, and I am not looking to replicate its logic, just its output.&nbsp; Let's put`string1` and `string2` onto a spreadsheet below in figure 1 with `string1` along an '**x**' axis and `string2` along a '**y**' axis:&nbsp;

[
![fig.1 LCS diagram](https://i.imgur.com/apwySod.jpg)
](https://drive.google.com/file/d/1NyPIxt_I8YnAzIA0KzFM2U6bLehSOr3V/view?usp=sharing){:target="_blank"}

Here we can see all of the matches between the two strings (shown in pink above) so now in order to find the longest common subsequence (LCS) we would need to find a series of characters that follow one of the blue arrow paths below in figure 2:&nbsp;

[
![fig.2 LCS diagram](https://i.imgur.com/0X2UWYc.jpg)
](https://drive.google.com/file/d/1YPKqj8WQjKRnkAdgxxCwhUK7bz3UcxHI/view?usp=sharing){:target="_blank"}

If you've got a good eye, you'll see that the longest common subsequence (LCS) is `qwerty`!&nbsp;  Let's take a look at the LCS highlighted in yellow below in Figure 3:&nbsp;

[
![fig.3 LCS diagram](https://i.imgur.com/kPK3en3.jpg)
](https://drive.google.com/file/d/1gAa6watrUILOm77KQ57-DlC7J-zuXRn5/view?usp=sharing){:target="_blank"}
You can see that each character (or lower-case letter in our example) occurs in both `string1` and `string2` and *each of these characters also occur in the same chronological order*.&nbsp;  These are the essential characteristics of the LCS.&nbsp;

I am not looking for the most efficient solution, just one that is reliable and may need refactoring later on.  At this point I am going to create some JavaScript Object Notation (or JSON) code for each of these matches, let's see what that looks like in Figure 4 below:&nbsp;

[
![fig.4 LCS diagram](https://i.imgur.com/Ucc2ytO.jpg)
](https://drive.google.com/file/d/1-F0A_hPPtbJlxHm5KY0OMEfbgXoVLDcJ/view?usp=sharing){:target="_blank"}
So here we are calling each of these matches (shown in pink) a ***location*** - and assigning each one a `locationOrder` in the JSON.&nbsp;  The ordering starts from the top left & ends in the bottom right of the matrix.&nbsp;  If we take a look at the JSON code we also see each location is aware of its own coordinates in the matrix with `x` and `y` values.&nbsp;  The location is also cognizant of its `descendants` - these are the other locations located to the right *and* bottom of the current location.&nbsp; So let's have a look at the **t** qwer**t**y' in order to better understand this.&nbsp;  Go ahead and zoom into the t in the lower right-hand corner where you'll find the following JSON code:
```
{
  locationOrder: 13,
  x: 11,
  y: 8,
  descendants: [ 14 ],
  progenyCenses: 1,
  character: 't'
}
```
This is telling us that our **t**:

 * is the 13th location in our matrix

 * is located in the 11th column on the matrix (x-axis)

 * is located in the 8th row on the matrix (y-axis)

 * has one location to its right and bottom, so that location is a
    descendant, and that descendant's `locationOrder` is `14`&nbsp;

 * has a `progenyCenses` value of `1` just like every other location.&nbsp;  This is the core engine of my algorithm that figures out how to actually find the LCS which I will discuss later.&nbsp;

 * has a character value of `t`

When we speak of a descendant we mean to say that if the LCS were 'qwerty', then the 'r', 't', and 'y' are all descendants of 'e' because they all come after 'e' in the order of sequence.  Likewise, 't' and 'y' are descendants of 'r' for the same reason, and it goes without saying that everybody in 'qwerty' is a descendant of the 'q' except the 'q' itself which is an ancestor to all of the other characters.&nbsp;  This is a good place to point out that ***my solution here will not track child-parent relationships, and is only aware of descendant-ancestor relationships***.  This means there are fewer relationships to track which leads to better efficiency.&nbsp;

After creating JSON objects for each location my solution calls for a second iteration over the matrix, this time going in reverse order from the iteration we did in Figure 4 above.&nbsp;  As we can see from the zig-zagging fat arrow below in Figure 5, we need to start the iteration from the lower right-hand corner and work towards the upper left-hand corner.&nbsp;  when we arrive at our first location we see it has a `locationOrder` value of `14` and a `character` of `y`.&nbsp;  Now we're going to get to the mysterious `progenyCensus` value that I identified earlier as the core engine of this solution.&nbsp;  At this lower right-most location (location 14) we have a `progenyCensus` value of `1` and we are going to keep it that way.&nbsp; The reason is that this location has no descendants to call its own, and the `progenyCensus` is a way to add value to *locations who have descendants which in turn also have descendants*, but in this case, our location 14 only gets a `progenyCensus` value of `1` to represent itself.&nbsp;  

[
![fig.5 LCS diagram](https://i.imgur.com/sIpy10b.jpg)
](https://drive.google.com/file/d/14VaGzhsKr6yC5fkPm05oWnFMA4TDbEg6/view?usp=sharing){:target="_blank"}
Once we get to the location 13 above (the one highlighted in green)  we see it gets a `progenyCensus` value of `2` - this is because it gets one point for itself (just like location 14 did) but it also gets another point for location 14 (highlighted in orange) because location 14 is a descendant and it also has a `progenyCensus` value of `1` so we add those two 1's together and assign location 13 a final `progenyCensus` value of `2`.&nbsp;  

Below in Figure 6 we see this pattern repeating once the iteration arrives at location 10 (the one highlighted in green) - there we see a big pink 4 that represents the commensurate `progenyCensus` value.  We get this 4 by looking at the `progenyCensus` values of all of the descendants (highlighted in orange) - there we have a 1 (at location 14) and a 2 (at location 13) and when we give a 1 for the current location (10) we get (1 + 2 + 1) which equals 4.

[
![fig.6 LCS diagram](https://i.imgur.com/PCQlw8I.jpg)
](https://drive.google.com/file/d/1KUJe4xuWwTPO2pRB3OrUsn4G8Lgl04BA/view?usp=sharing){:target="_blank"}

We now repeat the pattern until we reach location 8 as shown below in Figure 7; here we have a `progenyCensus` value of `11` because we took the values of all descendants and added them up so that 4 + 2 + 2 + 1 + 1 = 10 plus, the value of 1 for representation of location 8 itself which yields  a total  `progenyCensus` value of `11` at location 8 which is highlighted in green.&nbsp;

[
![fig.7 LCS diagram](https://i.imgur.com/jYvBR02.jpg)
](https://drive.google.com/file/d/1BM9AJWY12b5zZoIym4XHhX-7SvzL9fvD/view?usp=sharing){:target="_blank"}

Once we keep going we get the `progenyCensus` values for all of the locations, even those not part of the LCS as shown below in Figure 8:

[
![fig.8 LCS diagram](https://i.imgur.com/t6QYPfq.jpg)
](https://drive.google.com/file/d/1o_I8Sj2pQkwoh8mIc3IMe2nC8r-qZCXH/view?usp=sharing){:target="_blank"}

Keep in mind that at this point, our algorithm still has no idea where the longest common subsequence (LCS) is or what locations are included in it.&nbsp;  In example, location 1 below (which has a `locationOrder` value of `1` if you still don't see the pattern) has a `progenyCensus` value of `14` and is highlighted in a blue border with a big blue 14 underneath it.&nbsp;  To be sure, this location has a lot of descendants and as far as the algorithm is concerned at this point, this location might be in the LCS.&nbsp;

[
![fig.9 LCS diagram](https://i.imgur.com/IGsGILE.jpg)
](https://drive.google.com/file/d/1XqRLS_EZbku4a-Bc3cLlb1RV5W72G1p3/view?usp=sharing){:target="_blank"}

Alright, here in Figure 10 we are going to find the first character in the LCS; it is the ***q*** in the upper left-hand corner because that location has the highest `progenyCensus` value (73) in the entire matrix, so the algorithm will at this point decide that this in in fact the first character of the LCS.&nbsp;  Next question: of all the descendants of ***q***, which one has the highest `progenyCensus` value?&nbsp;  It turns out the answer is the ***w*** with the `progenyCensus` value of 22.&nbsp;  Remember that descendants have to be to the right and below the current location, below they are highlighted with dark-red borders:

[
![fig.10 LCS diagram](https://i.imgur.com/0mU7Beb.jpg)
](https://drive.google.com/file/d/1LbZFt6yGt42RT8cRqaHtlKUA9iDaTpTg/view?usp=sharing){:target="_blank"}

In figure 11 below we just repeat the process; we've already determined that the ***q*** with a `progenyCensus` value of 73 must be the first character in the LCS and its descendent, the ***w*** with a `progenyCensus` value of `22` must be the second character.  Now we're going to look at the descendants of that ***w***  (that are highlighted with dark-red borders) and ask which of them has the highest `progenyCensus` value?&nbsp;  The answer is of course the ***e*** with a `progenyCensus` value of `11`.&nbsp;

[
![fig.11 LCS diagram](https://i.imgur.com/OJhZXfd.jpg)
](https://drive.google.com/file/d/1Qn_sG8WZSlS77DSuB9IaY2mynqxHjWkE/view?usp=sharing){:target="_blank"}

And then we repeat the process...
[
![fig.12 LCS diagram](https://i.imgur.com/IhWcQza.jpg)
](https://drive.google.com/file/d/1ClrXo3vPvz2J5_y-PwBrP064bGag0_Ox/view?usp=sharing){:target="_blank"}

...until we get to the end!
[
![fig.13 LCS diagram](https://i.imgur.com/FKAKIA6.jpg)
](https://drive.google.com/file/d/1xeF6EmWcfDym6lQAptg7h6rEO6UnFzm2/view?usp=sharing){:target="_blank"}

I discovered this algorithm by accident while starring at a diagram I made that looks very similar to Figure 8 above.&nbsp; I noticed that the LCS had to have some sort of census value that weighed not only descendants, but the *descendants of descendants*  in such a way that gave more credit to descendant branches with a greater number of generations.&nbsp;  Now to be sure, this solution is not as fast as the [Dynamic Programming](https://rosettacode.org/wiki/Longest_common_subsequence#Dynamic_Programming_4){:target="_blank"} example I was trying to replicate, and it also breaks when the `string1` and `string2` input values get too large.&nbsp; The reason is that it is possible to have two `progenyCensus` values that are exactly the same, with one location having fewer generations than the other.&nbsp;

To prevent the breaking, I can simply add a multiplier to the `progenyCensus` calculation such that each number in that algorithm will be multiplied by ***x*** wherein ***x*** represents a value that must increase as `string1` and `string2` increase in size.&nbsp; This multiplier can be found on line 82 of [this REPL](https://repl.it/@Richard_Burd/Longest-Common-Subsequence#index.js){:target="_blank"} where it is currently set to a value of `8`.&nbsp; This will produce `progenyCensus` values that are much larger then the ones shown in the figures above, and thus, the chances of any two locations having the same `progenyCensus` value will be greatly reduced.&nbsp;

In the end, the value this algorithm brings to the table is the fact that it is object oriented and can therefore be expanded upon to include extended functionality.&nbsp;  For example, we could add a ***z*** axis to this thing and find the LCS between three strings instead of just 2.&nbsp;  We could also extend the functionality to exclude certain characters from the LCS, so for example we could say we want the LCS that does ***not*** include a letter ***'q'*** for example.&nbsp;  This could have all sorts of use cases for finding things like DNA sequences or searching for signal patterns while defining certain inputs as noise up front that should be excluded from the return value(s).&nbsp;  

Finally, to close up I have one last diagram that gives a comprehensive overview of everything discussed in this blog post.&nbsp;  The code being illustrated here is the exact same code as what is in the [REPL](https://repl.it/@Richard_Burd/Longest-Common-Subsequence#index.js){:target="_blank"}.&nbsp;
[
![Complete LCS diagram](https://i.imgur.com/pOI0lvk.jpg)
](https://drive.google.com/file/d/1VgipZbzKHnayMyBrFDpEqJ-kJwSb-tx1/view?usp=sharing){:target="_blank"}
