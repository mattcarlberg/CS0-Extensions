### Computing: Graphics and Games 
### Fall 2021 
### Class 52


# Directions

This exploration includes a review of for loops and an introduction to while loops.  Read through everything and then try the challenges at the bottom of the page.  This counts as "classwork" so we are grading you on effort.  Try as many of the coding challenges, but you are NOT required to do them all.  Submit a link with any work that you are able to do. 

We ESPECIALLY encourage you to complete all challenges, if you are planning to take Object-Oriented Programming next semester. 


# Attribution

This material is adapted from [Upperline Code](https://github.com/upperlinecode/06-p5.js-readings/blob/master/05b-loops.md).  They offer good [summer programs](https://www.upperlinecode.com/); they cost money, but there is financial aid available.  


# Loops

![looping](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/loop.gif)

For the moment, let's set aside getting our bubbles to move and just focus on drawing ellipses on the screen.

```javascript
function setup() {
  createCanvas(500,400);
}

function draw() {
  let x = 50;

  background(0);
  fill(250);

  ellipse(x, height/2, 40, 40);
}
```

![one ellipse](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/one-ellipse.png)

Great, now let's add a few more bubbles to the right.

![copying and pasting](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/copy-paste.gif)

That works, but it's so repetitive. Notice the same code is copied and pasted over and over again. There must be a better way, doing things over and over again is actually exactly what computers are great at. Think about `draw`and how it's run over and over.

## Review of `for` loops

In the past, when we have wanted certain code to repeat, we would use a for loop:

```
for ( ____; ____; ____ ) {
  run the code we want to be repeated here...
}
```
There are 3 parts to what we put inside the parentheses, and yes, those are semi-colons in between each.

**The first is:**

```
for ( where to start counting; ____; ____ ) {
  ...
}
```

In practice that will look like making a new variable telling us where to start:

```javascript
for ( let count = 0; ____; ____ ) {
  //...
}
```

**Second:**
```
for ( ____; when to stop the loop; ____ ) {
  ...
}
```

This is a true/false statement.  When true, we repeat.  When false, we stop repeating

```javascript
for ( let count = 0; count < 4; ____ ) {
  //...
}
```

**And Third:**
```
for ( ____; ____; how to count ) {
  ...
}
```

What does `how to count` mean?  Well, are we counting up by one? Up by 10, like `10`, `20`, `30`..., backwards from 100, `99`, `98`

All together it looks like:

```javascript
for ( let count = 0; count < 4; count += 1 ) {
  //...
}
```

Here's one version of a for loop that draws ellipses:
```javascript
for ( let count = 0; count < 4; count += 1 ) {
  ellipse(50*count+ 50, height/2, 40, 40)
}
```

Tip: `count+=1` is a shortcut for `count = count + 1`.  You can do this to increment a variable by any amount.  For example, `count+=3` is a shortcut for `count = count + 3`.  Incrementing a variable by 1 is so common that you can also use the shortcut `count++`.

So here's another version of a for loop that works just as well:
```javascript
  let x = 50;
  for (let i = 0; i < 4; i++) {
    ellipse(x, height/2, 40, 40);
    x += 50;
  }
```


## `while` loops

Think back to conditionals

```
if (something is true) {
  run the code here...
}
```

Ok, but if the conditional is `true` the code only gets run once. There's another way to control the flow of our code that looks very similar. The difference is that as long as the conditional is true, the code inside will keep running. "while" the conditional is true, you might say. That's exactly what we'll write:

```
while (something is true) {
  run the code we want to be repeated here...
}
```

That's called a **while loop**.

🚫 **CAUTION:** read ahead before following exactly the code below 🚫

Delete all the repeated code

![deleting repetition](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/delete.gif)

Add in the while loop

![inifnite loop](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/crash.gif)

and..

![crash](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/comp-crash.gif)

That froze up my whole computer. What's going on??

The computer was stuck in an **infinite loop**. While `true` was `true` (a.k.a *forever*) we instructed our computer to run the code in the loop. The computer always does exactly what we tell it, we just happened to tell it to do a crazy thing!

We fix this by adding a condition on the while loop so that it is not `true` forever.  Here's one version of a while loop that draws ellipses:

```javascript
let count = 0
while(count < 4){
  ellipse(50*count+50, height/2, 40, 40)
  count+=1
}
```

Here's another version of a while loop that works just as well:
```javascript
  let x = 50;
  let i = 0
  while(i < 4) {
    ellipse(x, height/2, 40, 40);
    x += 50;
    i++
  }
```




## Coding Challenges - Do As Many As You Can 

1.  Use a `while` loop to make a target of concentric rings. Start with the colors randomized.

 ![target](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/target.gif)

 Can you make the rings alternate color? Gradually change color toward the center?

2. Use a `while` loop to build a random city sky line. Here's some of the randomized cities my code builds.

 ![city skyline](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/city-skyline.gif)

 What would it take to draw a random number of windows on each building?

3. Use a `for` loop to draw a chessboard. A standard chessboard has 8 * 8 squares (64 total squares).  

 This problem is surprisingly tricky, so let's break it down into several parts. For step 1, let's only worry about the first row of squares. Also, for the moment let's not be concerned about the alternating black and white colors.  In your loop count from 0 up to 8 and draw a square each time incrementing the `x` coordinate.

 ![one-row](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/one-row.png)

 Ok, now the colors need to alternate. To do this initialize a boolean variable outside of the loop. If it's `true` draw a black square, if it's `false` draw a white square. *Inside the loop* flip the boolean value so the next time it's the opposite color. Something like `blk = !blk` would work ;)

 ![one-row-alternate](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/one-row-alternate.png)

 Great, now we want to count from 0 up to 64. If your `x` value gets too big, that means you are at the end of a row. Reset `x` to 0 and increment the `y` value to start on the next row down. Otherwise just increment the `x` value like you did before.

 You'll need to play around with where exactly in that conditional you say to switch the color to achieve the alternating square effect of the chessboard.

 ![full-board](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/full-board.png)

 There is an alternate approach to this problem that would use *a loop inside of a loop*. This is a little tricky conceptually but is a common approach when you have a grid structure like this.  If you are up for a challenge, try to refactor the code using two loops.
