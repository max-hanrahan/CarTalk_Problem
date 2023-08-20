# The "Car Talk" Problem

## with no elegant solution

notes:

Do you guys know the show Car Talk? If you grew up listening to public radio between the 80s and the 2010s, you probably do. It was a call-in radio show that ran weekly on NatPubRad for over 30 years. Listeners would call in, asking for help with whatever car-related problem they were trying to solve. The hosts, two MIT engineers who specialized in auto mechanics, would offer their humorous, semi-serious guidance on how to solve the listener's issues. 

The show would usually end with a "puzzler": a little one-minute riddle whose solution would be presented in the next episode. They were usually fairly abstract problems that would have a nice, satisfying resolution. 

This is not one one of them. In fact, it's not a puzzler at all, but a very practical problem featured on the show that has distracted me for about a year now. I want to go over what the problem is, how to solve it, and why it's been bothering me for so long. 

---

![[Pasted image 20230804110312.png]]

Episode 1045: "[Pi Over Two Dopes](https://www.cartalk.com/radio/show/1045-pi-over-two-dopes)"
notes:



In episode 1045, which I'll link in the description, a trucker called in to explain that his fuel gauge was busted. He drove an 18-wheeler on long cross-country trips, and needed to use a dip-stick to determine how much gas was left in his tank. There were a few markers that were particularly useful to know, for instance, he could easily use the stick to measure when he was halfway out of gas. But it is less straightforward to know when he had 1/4, or 3/4 of the tank left. So, the question is this: how do you mark 1/4 tank using only the dipstick?

I think this is a really interesting problem with a really nice physical motivation, and I've seen a few articles online answering the question (in particular a great blog post from Wired Magazine, which I'll link in the description and reference a few times in this talk). The Wired article in particular points out that this would make a great test question. However, every answer I've seen online has only gone so far as to set up the problem, and then give an approximate answer, rather than an exact one. In this talk, I'd like to arrive at an exact solution.

---

[![car_talk](https://user-images.githubusercontent.com/43153157/178158721-457f888d-d174-480d-8cc6-60078ac61592.gif)](https://user-images.githubusercontent.com/43153157/178158721-457f888d-d174-480d-8cc6-60078ac61592.gif)

When is the cylinder $\frac{1}{4}$ full?
notes:

It's hard to get started without a visual aid, so here's something I threw together in Desmos: it's a cross section of the fuel tank, gradually being filled and emptied, and we want to figure out where to position the line such that we have 1/4 of the circle shaded.

In a perfect world, I'd give you audio snippets of the conversation, so we could all go through this question together. But of course that isn't fair use, so instead I'll summarize the insights from the episode.

---
## Insights from the episode

1. It's **not** $\frac{1}{4}$.
2. This is a 2D problem. 
3. This is an area under a curve (i.e., an integral)
notes:

The first insight that the trucker offers is that the position of the vertical line is "probably not 1/4 of the way up", and the brothers agree. If that's not obvious, think about what would happen if we filled up a cube, rather than a cylinder. If it were a cube, the width of the container would not change as the gas level rose, but in our case, it does, so we have to be a little bit more careful. 

Next, the brothers realize that the height of the cylinder doesn't matter. This is an area problem, not a volume problem, so "you can do this in two dimensions". This is indicated in the visual aid I showed earlier, but the brothers didn't have one, so this is another important insight. And at this point, it is abundantly clear that we need to compute the area under a curve, so we know for a fact this is an integral calculus problem.

---
### Setting up the Integral

[![r/askmath - The Car Talk cylindrical fuel problem: how to analytically solve?](https://preview.redd.it/jg9suuscme991.jpg?width=320&format=pjpg&auto=webp&s=d70e73171fd0bed4b5de2863a5413315f3c0a029)](https://preview.redd.it/jg9suuscme991.jpg?width=320&format=pjpg&auto=webp&s=d70e73171fd0bed4b5de2863a5413315f3c0a029)

##### Credit: [WIRED Magazine](https://www.wired.com/2010/11/car-talk-cylindrical-fuel-tank-problem/)

$$ dA = \text{length} \times \text{width}$$


$$dA = 2x \times dy$$


$$ = 2\sqrt{R^{2} - y^{2}}dy$$
notes:
To restate this problem in more calculus terms, we're really asking "at what height above the bottom of a circle do you position a horizontal line, such that the area below the horizontal line is 1/4 the area of the total circle?" Again, it's useful to have a visual aid here, and frankly, I couldn't come up with a better illustration referenced in the wired magazine article, so I've posted that here. We can imagine our area differential as these tiny, infinitesimal rectangles that go from the bottom of the circle all the way to the location of this line. 

Now what is the area of one of these rectangles? It will be the length times the width, where I have width labeled as dy. So, how do we get length times width in terms of one variable, so we can do our integral? We can use the equation of a circle, x^2 + y^2 = R^2, to find the x-value corresponding to an arbitrary y-value on the circle. We can solve this for x, and then notice that since our x-solution has a square root. This means there are two possible solutions, one positive root and one negative root. This makes sense, because for every y-value (or height) we pick, there will be two points on the circle (the left point and the right point) who correspond to that height. At that height, we can treat the length as two times the positive solution, where the factor of two comes from us accounting for both sides of the circle. 

Thus, we have our equation for area with respect to one variable, the height of the line. We just have set the integral's bounds, set the expression equal to 1/4 of the circle's area, and solve for that unknown height. 


---

## Solving the integral


<video controls autoplay>
  <source src="equations.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


notes:

For simplicity's sake, let's assume the circle has radius 1 and is centered at the origin. Then in terms of y, our area differential is given by dA = 2*sqrt(1-y^2)* dy. If y' is the y-coordinate of the gas line, then we can integrate to solve for y' like so:

```
 y'    ________          π
∫   2 √ 1 - (y')²  dy = ———
 -1                      4
```

I'll cancel off the factor of two just for clarity's sake:

```
 y'    ________          π
∫     √ 1 - (y')²  dy = ———
 -1                      8
```

Okay, now the result of this indefinite integral is 1/2 (y sqrt(1 - y^2) + arcsin(y)). So if we plug in our bounds and set that equal to pi/8, we have:

```
1                           π   π
_ (1-(y')^2 + arcsin(y')) + _ = _
2                           4   8
```

and a more simplified version of this would be

```
4 sqrt(1 - (y')^2) y' + 4 arcsin(y') + π = 0
```
This is a transcendental equation, the answer to which is about -.404.  Putting that in terms of the trucker's original problem, where the tank was 20 inches in diameter, we have that the dip stick should be marked 5.96 inches up.

Now there are a few ways to evaluate this last line. I could put it into Mathematica and use it's solve function, or write a script to approximate the answer, or ask WolframAlpha to do it. But none of those are particularly satisfying for us. We want an _analytical_ answer, something exact that we can express in pure numbers, like the square root of 2, or pi, or some combination of those. But the fact remains that this line is transcendental, and so the closed-form, analytic solution that we've been trained so hard as good calculus students to look for doesn't exist. 

---
## More practical solutions
* Find someone with a quarter tank
* Use a household cylinder and scale to tank
* Numerically solve like so:

```Mathematica
FindRoot[4 Sqrt[1 - (y)^2] * y + 4 ArcSin[y] + \[Pi], {y, 0}]
```
notes:
I want to emphasize that there are many more practical ways of solving this problem. The hosts of Car Talk, when they realize the mess they're in, urge the trucker to find a fellow trucker, say, at a truck stop, who had a quarter tank of gas, and then measure using the dip stick to draw the mark. This is probably what you or I would do if we had this real problem to solve. In the absence of a fellow trucker, you could also find some cylindrical object at home, like a water bottle. Fill it up 1/4 of the way and then turn it on its side to measure the line: you just need to solve the problem for your mini-cylinder and scale it up to the size of the gas tank. If you're like me and still want to approach this problem from a numbers angle, I've included this snippet of Mathematica code to solve that transcendental line numerically .

---

<video controls autoplay>
  <source src="numerical.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


Code for finding the height of the line numerically
notes:

You could also do as the wired article suggested, and write your own python script to approximate the answer numerically. Here's a screen recording of me working on this, and it still gets you the right answer of -.404. So there's many ways to skin a cat here, but none of them have that satisfying oomph that I'd normally present in a video. 

That's why I've sat on this for a year without ever making a video. It's a weird story to tell. We try working for a result and we hit a wall. And if you get nothing else out of this video, I want you to understand that this is _frustrating_, but true about the mathematical world. There are so many physical problems like this, that start off promising a pretty solution but have to be solved in a more practical manner. For instance, The Kepler Problem, widely considered to be the founding problem of Analytical Mechanics, doesn't have an analytical solution. And honestly, I wasn't totally comfortable with making this video until I learned how many problems have to be solved in exactly the same way. 

---

> "The mathematicians always want that their mathematics should be pure, that is, strict and provable, wherever possible. However, the most interesting and realistic problems could not usually be solved in that manner. Therefore, it is very important that the mathematician should be able to find the approximative (not necessarily strict but effective) ways of solving such problems".  
> -A. Kolmogorov

notes:
I'll conclude with this quote from Andrey Kolmogorov, a mathematician notable for his contributions to such problems. 

So the next time you run into a problem that you can't solve with an elegant solution, don't feel so bad! Sometimes that's just how the universe works -- or at least, how the math works out. 

