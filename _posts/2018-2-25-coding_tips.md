---
layout: post
title: Don't tell me how to code
date: 2019-2-28 06:00
description: Giving some advise on coding from a researcher perspective
published: true
---

Everyone has different coding styles. Whether you are a clean or messy coder, it is fine as long as the program runs, right? Well, not quite. This quick article serves as a summary of what I've observed and learned, from coursework and working with people of various background (engineering, CS, biomedical, neuroscience folks...) throughout the years. To me, writing code is similar to writing an article. There are certain elements that can make a a piece of code *good*. What are some tricks and tips that might benefit YOU?

<p class="caption">
    P.S. People write books on how to write nice code. I am not intended to condense their work here. This article is a my own short summary that will most benefit beginner coders.
</p>

## Quality of code

What is a good piece of code? Here are some criteria I believe are crucial:

* It **runs** - that's just a bottom line to be correct
* It's **time-efficient** - producing equal quality work that runs 10$\times$ faster than your friend
* It's **space-efficient** - saving a 10-dim matrix you won't use later to your memory space is completely unnecessary; reduce, reuse, and recycle (wait what?)
* It's **amenable** - it's easy to change value of some parameters or reuse your code for other projects
* It's **readable** - I once need to film a video of me explaining my code as per request by my colleague who will be using my code for his project... unnecessary if your code is self-explanatory. You, your colleagues, as well as the 10-years-later you will thank you later.

### What is readable?

Code is meant for human to read, machine to execute. I want to elaborate more on the idea of readable. To be readable, the code should be (1) simple and concise, (2) straightforward to understand what and why you're trying to do, (3) systematics by using the consistent conventions.

So if I put a lot of ```# comments``` in my code, will it be more readable?

A short answer is: sure, but not necessarily. In a beginner coding class, it is common that either the teacher use a lot of ```#``` to describe what the line does, or worst, your perfectly runnable code doesn't have enough ```#``` so your grader deducts some points and comments that it's not "readable" enough. Comments serve a purpose to explain, hence making the code more comprehensible. Yet, a readable piece of code need not have a ton of comment. In fact, a good coder would always include a few commenting sentence only at the beginning of the code to explain the purpose, introduce key features, and describle input variables of the program, but not quite within the body of the code. Writing explanation for each line of the code can be redundant and definitely not elegant.

## General tips

What are some good practice that every coder should bear in mind? In correspondence to the quality of code section, I offer some tips that might be insightful for you.

* It runs - write down pseudocode; use debugging tools as much as you can;print values and sizes of parameters, number of iterations and results to screen; test ideas with smaller matrices
* Time-efficient - Save your time writing your own function by using the built-in function that you can directly import and call.
* Time-efficient - Avoid nest loops; the chance is you can probably find a smarter and better way to replace it.
* Time-, space-efficient - Utilize lists, sets, and dictionaries appropriately and wisely. They are your friend.
* Amenable, readable - Write separate functions instead of cramping everything in a never-ending ```__main__``` body. It is clean and straightforward. Think of functions as LEGO bricks. They are building blocks that one can build on top of each other to synthesize new material. You can even reuse them to build various objects. What's even better is that you don't need modify either LEGO brick at all to build something new.
* Amenable - Initialize hyperparameters that you might want to play around at the top of the program, name it appropriately and reuse it. If it's fixed parameter, such as the number of samples or class, give it a simple variable name such as ```n, k``` and never use the actual value even if you know it.
* Readable - Just like writing a book, an article, or a letter, we write in sections and paragraph to make the passage easy to read. Try using ```%%``` in MATLAB to section, or call self-defined functions in your python ```__main__``` as if you're reading the pseudocode.

## I'm a beginner coder, how do I advance fast?

You can only learn so much from an intro to programming class. After learning the concepts, it's very important to put it in practice. Remember, there's no overnight piano prodigies, so there's no overnight coding genius. The most effective way to improve your code quality is to practice writing your own code on common problems. Unless you need to look up a certain function or to fix a bug, DO NOT search for answer or copy-paste from anyone. Once your code is up and running, compare it to solutions you find online. You will be surprise to see how much improvement can be done. Learn and absorb, write and repeat!


