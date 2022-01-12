### Computing: Graphics and Games 
### Fall 2021 
### Class 53

# Directions

In this exploration, you'll make lots of bubble objects.  Read through everything and then try the challenges at the bottom of the page.  This counts as "classwork" so we are grading you on effort.  Try as many of the coding challenges, but you are NOT required to do them all.  Submit a link with any work that you are able to do. 

We ESPECIALLY encourage you to complete all challenges, if you are planning to take Object-Oriented Programming next semester. 


# Attribution

This material is adapted from [Upperline Code](https://raw.githubusercontent.com/upperlinecode/06-p5.js-readings/master/05d-arrays-and-loops.md).  They offer good [summer programs](https://www.upperlinecode.com/); they cost money, but there is financial aid available.  


# Reminder

The keywords `let` and `var` are very similar in Javascript.  They both introduce a new variable into the computer's memory.  For our purposes, you can use them interchangeably.  It is currently the convention to use `let` whenever possible, but many of these gif animations were made five years ago when `var` was used extensively.  The [slight difference](https://www.geeksforgeeks.org/difference-between-var-and-let-in-javascript/) between `let` and `var` is in something known as variable scope. 


# Arrays and Loops
Between arrays, loops, and objects, we're starting to really have some powerful tools at our disposal.

![tools](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/tools.gif)

# Back to the Bubbles

### Step 1: Click and `push`
The idea is that every time we click we'll add a bubble to the canvas.

To start, let's just `push` some value onto an array every time the mouse is clicked and confirm that the array grows larger.

Here's the starter code-- Notice `bubbles` begins as an empty array:

```javascript
let bubbles = [];
let bubbleSize = 40;

function setup() {
  createCanvas(500,400);
}

function draw() {
  background(0);
}

function mouseClicked() {
  // let's add code here
}
```

![push something](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/push-something.gif)

So cool! Every time we click we add an element to the array and we can see that it's happening. Right now that element is just an arbitrary value.  Let's go ahead and push on a real bubble object that has the correct properties.

Change the variable `bubble` to this:

```javascript
let bubble = {
   x: random(width),
   y: random(height)
 };
```

That's closer, but we're still basically at the same place. We have an array with elements in it, but nothing on the canvas.

### Step 2: `for` every bubble in the array

What if inside of `draw` we were constantly looping over the `bubbles` array.  **For** every item we should call the `ellipse` function to draw the bubble.  Let's give it a shot, we need 3 pieces of information for the `for` loop.

- **Where to start:** well array indexes start at `0` so that seems like a good place to me.
- **When to end:** We don't want to keep looping if we're past the end of the array so how about up to `bubbles.length`, *whatever that value is currently*.
- **How to count:** Definitely wouldn't want to skip over anything in the array so by `1` works fine.

All together that's something like:

```javascript
for(let i = 0; i < bubbles.length; i++) {

  ellipse(___, ___, bubbleSize, bubbleSize);
}
```

**Q:** How to fill in those blanks?  How do we access the value of a single item from an array?

**A:** With the index.

**Q:** Do we have any variables lying around that represent the *index we are currently on as we loop through the array*?

**A:** Why of course, `i`!

`bubbles[i]`, or, in english, the value of the `bubbles` array at the index `i`, will be the first bubble object the first pass of the loop. Then the second time it will be the second bubble, then the third, then the next all the way until the last bubble.  That's just what we want because we want to call `ellipse` with the values from each bubble object.

*Inside* the loop, we'll use whatever the current value of `i` is to make a variable called `currentBubble`.

![current bubble](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/currentBubble.gif)

Amazing! Every time we click a random bubble appears. It's not moving though.  Think for a second about *where* we need to add to the code to do this.

If you answered *inside the loop* you are 100% correct. That's the only place where we're able to change, for example, the third bubble's speed or fourth bubble's speed, or any individual bubble's speed-- inside the loop.

The `for` loop should look like this:

```javascript
for(let i = 0; i < bubbles.length; i++) {
  let currentBubble = bubbles[i];
  ellipse( currentBubble.x, currentBubble.y, bubbleSize, bubbleSize);

  currentBubble.x += random(-2, 2);
  currentBubble.y += random(-2, 2);
}
```

![cool, but kind of creepy](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/kind-of-creepy.gif)

We just put together in a few minutes what would have taken us an hour or more before, good work!

## Popping Bubbles

I want to make it so clicking anywhere on the canvas creates a new bubble, but clicking on a specific bubble pops it (in p5-world that means removes it from the array).

In the `mouseClicked` function we can loop over `bubbles` and see if `mouseX` and `mouseY` are inside of a bubble.

#### 🔔🔑💡 Tip 💡🔑🔔
> A brief note, when looping over an array and *also potentially removing items* from it, things can get a little of weird because the array's `length` will be changing. We may not run into problems here, but it's best in these circumstances to loop over the array backwards. It will ensure that no items are missed in the loop.  It's fine to just take my word for it for the time being, but feel free to consider the problem more in-depth later. Our loop will look like this:
 ```javascript
 // the 3 parts of the for loop have not changed:
 // where to start, when to stop, how to count.
 for(let i = bubbles.length - 1; i >= 0; i--) {
   // ...code
 }
 ```
We should be able to come up with code similar to this:

```javascript
function mouseClicked() {

  for(let i = bubbles.length - 1; i >= 0; i--) {
    let currentBubble = bubbles[i];

    if (mouseX and mouseY are inside of currentBubble) {

    }
  }
  //...previous code
}
```

Take a look at the [`dist()` function](https://p5js.org/reference/#/p5/dist). It takes two `(x,y)` coordinates and returns the distance between them.  We want to see if the distance between the center of the circle and `(mouseX, mouseY)` is less than the radius of the circle (`bubbleSize/2`).

```javascript
function mouseClicked() {

  for(let i = bubbles.length - 1; i >= 0; i--) {
    let currentBubble = bubbles[i];

    let distance = dist(mouseX, mouseY, currentBubble.x, currentBubble.y)

    if (distance <= 20) {
      // remove the bubble
    }
  }
  //...previous code
}
```

Now, take a look at the [`splice` method](https://www.freecodecamp.org/news/javascript-splice-how-to-use-the-splice-js-array-method/).  It is built into Javascript and removes items from a list. To remove a bubble, `splice` will need the index to remove (for us that's `i`) and the number of elements to remove (for us that is `1`).

![pop and add](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/pop-and-add.gif)

Our removal actually works! It just seems sort of weird that we still add a bubble on every click even if that click was supposed to pop a bubble.

To me, the easiest way to do this is to say, "if any bubbles popped, don't add a bubble".  The way we can know in our code if any bubbles popped is to see if the array is any smaller at the end of the function than it was at the beginning.  

We'll store the length in a variable called `startingLength` and only add a bubble if *after* the `for` loop `startingLength == bubbles.length`.

Here's the total final code:

```javascript
let bubbles = [];
let bubbleSize = 40;

function setup() {
  createCanvas(500,400);
}

function draw() {
  background(0);

  for(let i = 0; i < bubbles.length; i++) {
    let currentBubble = bubbles[i];
    ellipse( currentBubble.x, currentBubble.y, bubbleSize, bubbleSize);

    currentBubble.x += random(-2, 2);
    currentBubble.y += random(-2, 2);
  }

}

function mouseClicked() {
  let startingLength = bubbles.length;

  for(let i = bubbles.length - 1; i >= 0; i--) {
    let currentBubble = bubbles[i];
    let distance = dist(mouseX, mouseY, currentBubble.x, currentBubble.y)

    if (distance <= 20) {
      bubbles.splice(i, 1);
    }
  }

  if (startingLength == bubbles.length) {
    let bubble = {
      x: random(width),
      y: random(height)
    };

    bubbles.push(bubble);
  }
}
```

And the final product:
![popping off](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/popping-off.gif)

Have fun popping bubbles!

## Coding Challenges - Do As Many As You Can 

1. Instead of each bubble popping immediately on the first click, make the bubble grow larger with each click until it reaches some maximum size. Then, on the next click, it will pop.

 ![three-strikes](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/three-strikes.gif)

 You will probably need to add an additional property to each bubble object to track it's size.

2. Add a `lifespan` property to each bubble object that has a value of `0` when it is pushed into the `bubbles` array.  Every time `draw` is called `lifespan` should increment by `1`. If `lifespan` is greater than `300` the bubble should automatically pop.
3. Automatically generate a lot of bubbles when you click your mouse.  Then when you move your mouse through the sea of bubbles have them move out of the way of your mouse: 

![part the bubbles](https://s3.amazonaws.com/upperline/curriculum-assets/p5js/bubble-part.gif)
