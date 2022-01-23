---
title: A Journey into λCalculus
date: 2019-04-23 02:20:00 -0800
modified: 2022-01-22 12:00:59 -0700
permalink: /a-journey-into-lambda-calculus/
category: Programming
blags: [explained, maths, programming language, studying]
tags: writing/blog/published
---

I'm playing around in [Minetest](https://www.minetest.net/), and I have an idea. In order to execute this idea, I'm going to need a simple programming language. Asking Google… [_implementing a simple programming language_](https://www.google.com/search?q=implementing+a+simple+programming+language)…

[**7 lines of code, 3 minutes: Implement a programming language from scratch**](http://matt.might.net/articles/implementing-a-programming-language/)  
Sounds good! Ridiculously simple, fast, and gives us a fully usable language. _(I would've understood [brainfuck](https://esolangs.org/wiki/brainfuck) better..)_ Let’s see what this language looks like:

```
(λ v . e)   anonymous function with argument v and returning e
(f v)       call function f with argument v
(λ a . a)   example: identity function (returns its argument)

And the scary one:
(((λ f . (λ x . (f x))) (λ a . a)) (λ b . b))
```

Seems okay until I get to understanding that last example. If you’re curious about the steps I went through before I finally figured it out, [here are my notes](https://pastebin.com/u/TangentFox/1/n12kaCgm). I'm gonna skip to the good part:

```
(((λ f . (λ x . (f x))) (λ a . a)) (λ b . b))
two identity functions, let's name them I, & remove excess parenthesis
(λ f . (λ x . (f x))) I I
the syntax is still confusing me, let's make an "F" function
F(x) -> return (λ x . (f x))
F I I                          equivalent to ((F I) I)
substituting the function (identity) into our definition gives us
(λ x . (I x))                  which..is actually the same as the identity function
I(I)                           ..it all comes to returning the identity function

λ x . x
```

Now, at this point I've learned a few small tricks for my understanding, as well as how lambda calculus works in general.

## Reduction

Solving a lambda calculus program is made of three (or 2.5) steps called reductions:

- η-conversion (eta): Replace equivalent functions with simpler forms **(λ x . f x) -> f**
- β-reduction (beta): Substitution **(λ a . a) x -> x** _(essentially, THIS is solving it)_
- α-conversion (alpha): Rename conflicting names **(λ a . a b) (λ a . a) -> (λ a . a b) (λ c . c)**

## References

This is where my journey ends for now. I started studying lambda calculus because of a desire to implement a simple programming language, but this will likely not satisfy my needs..at least not in this form. Here are additional resources:

- [Lambda calculus on Wikipedia](https://en.wikipedia.org/wiki/Lambda_calculus)
- [What does (((λ f . (λ x . (f x))) (λ a . a)) (λ b . b)) mean?](http://patshaughnessy.net/2014/1/30/what-does-f-x-f-x-a-a-b-b-mean) _(literally googled this after solving it, because I couldn’t believe I spent hours solving for a series of identity functions)_
- [Lambda Calculus Reduction steps on Stack Overflow](https://stackoverflow.com/questions/34140819/lambda-calculus-reduction-steps)
