---
layout: post
title:      "Update on Algorithm Illustrations"
date:       2020-12-02 9:00:00 -0400
permalink:  update_on_algorithm_illustrations
---
Let's have a look at something weird and fun I call a 'Zig-Zag-O-Gram'
[
![zig-zag-o-gram](https://i.imgur.com/jXRbayE.jpg)
](https://camo.githubusercontent.com/bc041b44c2c12d1dc333df9451d2365bd7a6b6e9/68747470733a2f2f692e696d6775722e636f6d2f6a5852626179452e6a7067){:target="_blank"}

Lately I've been working on exploring new ways to illustrate individual algorithms as opposed to stack architecture.&nbsp;	Above we have what I am calling a 'Zig-Zag-O-Gram' illustration for the 'chunked array problem discussed [here](https://youtu.be/cL1HB_IC9Fc){:target="_blank"}

This function takes in two variables: an array and a number.&nbsp;  The function in turn must return a value of the array, with the original elements 'chunked' into nested arrays that are the length of the second variable.&nbsp;  Thus, given these two variables: `[1, 4, 12, 3, 2, 6, -9, 0], n=3` the function must return: `[[1, 4, 12], [3, 2, 6], [-9, 0]]`&nbsp;  Here is the solution illustrated above:
```javascript
const chunks = ((arr, n) => {
  const chunked = [];
   for(let elem of arr) {
     let last = chunked[chunked.length-1];
     if (!last || last.length === n)
       chunked.push([elem])
     else
       last.push(elem)
    }
    return chunked;
})([1, 4, 12, 3, 2, 6, -9, 0], 3)

console.log({
  chunks //=> [[1, 4, 12], [3, 2, 6], [-9, 0]]
})
```

While the Zig-Zag-O-Gram approach might be useful for educational purposes, it is time consuming to draw and difficult to alter.&nbsp;  Students that are new to coding might find this sort of thing useful for seeing how iterations handle conditional statements, but using something like this to develop an algorithm is difficult because of all the separate iterations that must be represented.&nbsp;  

This got me thinking about a different approach that I call the *'gate'* method, in this next approach we'll use the classic *Fizz-Buzz* problem where you must write a program that prints the numbers from 1 to 15, but for multiples of 3 the program must print `"Fizz"` instead of the number and for multiples of five print `"Buzz"` - and finally, for numbers which are multiples of both 3 and 5 the program must print `"FizzBuzz"`  The textbook solution will look something like this:
```javascript
function fizzy(){
  for(i = 0; i <= 15; i++) {
    if(i % 15 == 0) {
      console.log("FizzBuzz")
    } else if (i % 3 == 0) {
      console.log("Fizz")
    } else if (i % 5 == 0) {
      console.log("Buzz")
    } else {
      console.log(i)
    }
  }
}
fizzy()
```
Here is how I would illustrate something like this:

![fizz-buzz shown with the gate method](https://i.imgur.com/svVw4gT.jpg)

The basic idea here is that we now have a series of traces, or *'gates'* that link different outputs to different conditions.&nbsp; While this looks clean in our example above, the gate will become increasingly complex once we have nested conditions within our primary looping body.&nbsp;  Additionally, we have an incredibly simple sequencing in which we are returning a single string value to the console, but imagine  if we had subsequences instead, things would get messy quick!&nbsp;

Now let's look at our original ***Chunked Array*** problem that we started with at the beginning of this blog post:

![chunked-array shown with the gate method](https://i.imgur.com/GWzF4UW.jpg)

Here the gates get messy as we try & color-coat too many processes; we now have a sequence map whose last line is the final output, and we want to color-coat each line with some neon blue to match it with the `chunked = []` definition in the upper right.&nbsp; We also want to use neon yellow (in the sequence map) to link the nested array with our `last = chunked[chunked.length-1]` line of code  in the upper right as well.



Once again we have something that might help beginner students to see ***how*** functions work in diagrammatical form, but this isn't something that is readably usable for professional developers.&nbsp;  Aside from the messiness, the format isn't scalable to large problems where a visual aid might be helpful for finding a solution.&nbsp;  My search for the *panacea-algorithm-illustration-methodology* continues!
