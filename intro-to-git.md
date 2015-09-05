---
title: Introduction to Git
author: Alexey Shiklomanov
---

# Why version control?

> An essential aspect of creativity is not being afraid to fail.
> --- Edwin Land

How often do you use the "undo" function on your computer? If you're anything 
like me, it's multiple times a *minute*. In other words, I make mistakes or 
second-guess my decisions almost constantly while working. The fact that my 
computer keeps a history of every action I perform and allows me to instantly 
revert them has not only saved me countless hours but also given me the 
courage to try new things without worrying about causing lingering damage.

Now, imagine if you had finer control over the "undo" feature. For instance, 
what if you want to see a history of everything you've done without actually 
reverting?  Or, what if you wanted to try something new but have quick and 
easy access to an older, working version in case you broke something?  
Moreover, what if you wanted to do any of these things while collaborating on 
a project with multiple people?

Enter **version control**. At its core, version control is a combination of a 
more advanced "undo" feature and a dairy or lab notebook. Whenever you make a 
significant change to whatever you're working on, you save it through your 
version control system along with a note describing what you did and why.  
Eventually, you end up with an annotated history of everything you did to a 
file along with the capability to instantly go back to any point in that 
history. If you're working on a project with multiple people, version control 
also keeps track of who did what and when, so that if something breaks, you 
can quickly and easily follow the paper trail and figure out whom to blame.

If all of this sounds appealing to you, read on! The rest of this page is 
devoted to introducing Git--one of the most popular and powerful version 
control systems in use today.

# What is Git?


