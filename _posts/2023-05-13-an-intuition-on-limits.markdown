---
layout: post
title:  "An intuition on Limits and Colimits"
date:   2023-05-13 07:08:43 +0300
categories: category-theory mathematics intuition limits colimits universal-constructions
title: An intuition on Limits and Colimits
author: King'oina
---

What is a good way to think about limits and how they are used in categorical constructions? This is a question
we found ourselves pondering on recently and the following question arose as a possible direction to probe the
essence of limits and possibly why they are so darn useful. Is a limit a fancy way of saying we know how to
relate all the objects in a category?

A good way to start looking into (find a more suitable word) is to start with giving a similarly motivated
intuition on functors. Essentially a functor is a way for one category to communicate with another category. Another
question that may arise when hearing such a statement is what does 'communication' between categories entail, in our
previous post we went on a rant on communication between people and that kind of communication is similar in certain
senses with the 'communication' between categories we are talking about here. When two categories interact what information
do they exchange? This exchange of information is what is facilitated by Functors where a category can describe it's 'contents'
in the language of another category, sometimes the other category also has a way to talk about it's content in the
'language' of the original category, in this case we say there is an adjunction between the categories. In human interaction
terminology we might say that the two categories are in sync(that was meant in jest). So what do Functors have to do with an
intuition of limits?

For starters; limits and colimits are formally defined with the help of Functors, so there is no escaping having to deal with
them. We are going to leave the formal definition of a limit and colimit to the end of this post to avoid too much information
overload which might cloud the message we want to pass across. Motivation for the necessity of the concept of limits and colimits
could have come from any problem solving endeavour in mathematics, this is because limits (colimits) are almost always present in
the discussion of non-trivial relations between objects. Given the fact that limits are characterized as universal constructions this
might give a hint to the reason of their ubiquity.

Let's imagine a situation where we are given a collection of items and we wanted to know about all the items in the collection. A
straightforward way to do this would be to inspect each item independently one by one until we go through the entire collection. This works
but what if the collection contained more items than the number of stars in the galaxy, this would take an overly dedicated person a good chunk of
their afterlife, so it's not a feasible way to discover information about the items in the collection especially if we don't know the size of the
collection before hand. Is there another way to do this or are we doomed. Obviously we wouldn't ask that rhetorical question if we didn't think
there was another way. Truly knowing about something entails having to know the thing in all perspectives that are available, maybe even discover
new perspectives. So a good think to have at the back of our minds is that all items in the collection are knowable in many various ways and that these
various ways of knowing are related somehow. How can we use this knowledge to find a clever way to know about all the items in a collection?

Enter the concept of a limit, essentially this mathematical construction enables one to know one 'object' that is related to all the other objects in some
way. Hence knowing that a particular category has a limit gives a mathematician a inkling that they can explore the category in an efficient way and hence
make certain conclusions about the entire category without necessarily having to know all the objects in the category. This is the intuition we have so far
and I'm sure this will change in the future as we continue to explore abstractions in the realm of category theory.

For a more formal definition for those that are ever so inclined this [wikipedia article](https://en.wikipedia.org/wiki/Limit_(category_theory)) provides a
somewhat gentle introduction to the concept. A more in-depth treatment of the same can be seen in this [page](https://ncatlab.org/nlab/show/limit). For an
even more nuanced look a look at some of the references in the above entries will prove insightful.

Thank you for your time and attention as we tried to intuit through a central notion in all of category theory and we bet in all of mathematics. See you in
the future.
