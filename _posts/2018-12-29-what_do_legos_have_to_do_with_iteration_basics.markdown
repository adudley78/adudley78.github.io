---
layout: post
title:      "What do Legos have to do with iteration basics?"
date:       2018-12-29 10:20:42 -0500
permalink:  what_do_legos_have_to_do_with_iteration_basics
---


**Initially, iteration was a difficult concept for me to grasp.** It wasn’t until I had practiced using iterators like #each and #collect in Ruby that I began to understand how these processes allow you to do interesting things with elements in an array or hash.

**Here’s how I think about it.**

**It all starts with a collection of objects.** These objects can represent things in the real world like songs or artists, apples or money, or even Legos. 

@@Legos = [piece_one, piece_two, piece_three]

**The iterative method you choose to use depends** on what you want to do with or to the stored objects. For example, if I’m fine with the original array or hash being returned after each element is operated on then I’ll use #each, however, if I want a new array or hash returned I might use #map or #collect. 

@@Legos.each

@@Legos.map

**In addition to using one of the aforementioned iterators** and depending on what I want to accomplish with my code, I might chain iterative and helper methods together in a way that does something to each object or returns true or false.

**Regardless of which methods I choose, the iterative process** will go into the collection and do something with or to each object or item in the collection. The element might just get looked at or it might be evaluated, manipulated, or assigned a property or attribute.

**Ok, now for the Lego example. I chose to use Legos** because almost everybody knows about Legos. Even if you didn’t have them or play with them as a child you probably know what they are and how they work. Plus, adults playing with Legos as a hobby seems to be a thing. So here we go.

**Imagine a big pile or box of Legos. It might be a pile of random pieces** (think array) or it might be a set where you have standard Lego types (think hash keys) with multiple pieces for each type (think hash values) that form a predetermined whole project. Whatever the setup, you have a collection of pieces but you can’t do anything with a random handful of them! You have to deal with each of them individually. If we were to apply this to the world of code, we might use an iterator like #each. 

**You might want to collect a particular piece or type of piece** and put that into a new pile of just that type of piece (#sort). Or you may want to find a particular piece (#find or #detect) or count (#count) how many pieces or types of pieces you have and add them to a new collection based on type as with key/value pairs of a hash. Maybe you want to remove duplicate pieces (#uniq). Either way, it’s only after you grab each item individually that you can do any of these interesting things with them. 

**Something else you can do that’s interesting is grab each** Lego piece and assign properties to it. You can assign it a color. You can assign it a size. You can assign it to a particular set that it belongs to. You can do all this in programming by assigning each new item to an instance variable that allows for attributes to be written to it.

**Again, these operations can only be achieved by performing** operations on each Lego piece individually. You have to grab each piece before you can do anything else with it. And that I think lines up perfectly with how iteration works. To do something to or with the collection as a whole you have to deal with each item in that collection individually.
