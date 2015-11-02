---
layout: post
title: "Why you should refactoring your code?"
date: 2014-01-19 15:00:00 -0300
categories: development
permalink: why-you-should-refactoring-your-code
author: Peterson Santos
headline: "Write beautiful, clean and objective code like a boss"
---

Before start to justify why you should practice refactoring, i’ll put two definitions where the first is the default and everybody know and the second is my own definition:

1. Modifying a software system to improve the internal structure of code without changing its external behavior process.
2. Process to make your code easier to understand, easier to maintain without changing their behavior.

### But why?

If you had never heard of this technique, you should be asking: If refactoring code doesn’t change the behavior , why i should change it? For what?
Below are some reasons why you should refactor your code:

1. **Improve the design of your software:** without refactoring their software loses the structure. Many people work on it and before understood as a whole, need to make minor changes to meet a specific problem, and end up modifying the wrong way, in other words, the software loses shape and getting increasingly more complicated to modify and even add new features.
2. **Let your code easy to understand:** when your software loses the structure, it’s harder to understand, in other words, problemas it was easy to resolve and features that was easy to implement, now take hours because the time that you take to understand and make the change are so long.
3. **Find bugs easily:** refactoring your code will be easier to understand, and therefore, will be easier to find bugs! And it’s no use saying that your software don’t has bug, the truth is you don’t know.

![Refactoring cycle](https://d262ilb51hltx0.cloudfront.net/max/1600/1*Zc6KhpHoMKg2V9IahOokLQ.gif "Refactoring cycle")

After all the advantages not yet conviced? Few months ago i attended a dojo, where the problem was to refactor a bad code, [look the diference by yourself.](http://objetiva.co/blog/2011/04/17/gravao-do-kata-gilded-rose)

### Why a lot of people don’t do it?

But if refactoring is so advantageous why programmers don’t practice it? It’s simple, most programmers write software without tests and refactor without test coverage is the same thing as giving a shot in the dark, because the tests that ensure the behavior of their software, but that’s a topic for another post.

But be careful, according to [Martin Fowler](http://martinfowler.com) exists a metaphor of two hats, which reads:

>While making the tests work, we can focus just on the problem of adding new functionality, without thinking about how this functionality should be best structured. Once things are working we can now concentrate on good design, while working in the safer refactoring mode of small steps on a green test base.

### Conclusion
After all of this we can only come to a conclusion, without software refactoring is more code, more trouble, more expensive, more headaches.

If you were interested to learn more and improve the quality of their software, i recommend this book: [Refactoring: Improving the Design of Existing Code.](http://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672)
