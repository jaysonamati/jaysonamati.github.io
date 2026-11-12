---
layout: post
title:  "Common Side Effects"
date:   2026-11-12 11:11:44 +0300
categories: applied-category-theory category-theory formal-mathematics programs effect-systems ai ai-interaction
---

<!-- *Of AI Systems* -->

Often lauded for its elegance, one of my favourite feature of Haskell is its clean separation between pure and impure
code. With this one is able to read the intention of the program by studying the type signature of its component
functions. Those marked with Effect constructs stand out, it is often clear that such components are doing something
that might not be apparent in the body of the function. This warrants a programmer to have a second look and be more
careful with such functions. On the other hand, pure functions are what they say they are, one cannot expect surprises
that are outside the function signature let alone the function body.

One reason why I quite like this design choice is that it provides some computational grounding for some abstract
notions. It is easy to see why a [Monad](https://en.wikipedia.org/wiki/Monad_(functional_programming)) would be a good choice to describe effects. In the pure mathematics realm [Monads](https://ncatlab.org/nlab/show/monad)
play more abstract roles but this "abstractness" does provide the conceptual ladders to reason cheaply about complex
realities of computational environments. This play between the most abstract and the most concrete is one in which
haskell excels. Smuggling mathematical insights into web servers seems almost like overkill until you can read
an API specification and immediately "get" what this code can and can't do. The answer to a question such as
"Does this touch the database" is often just reading a function signature.

Other functional programming languages such as [unison](https://www.unison-lang.org/) provide fine grained effect 
declaration in the type signatures of functions. Compared to haskell [IO](https://wiki.haskell.org/index.php?title=IO_inside) which covers generalized effects, unison
gives a programmer the ability to specify explicitly what kind of effect a particular function is going to "exhibit".
Moreover, Haskell's conventional [IO](https://wiki.haskell.org/index.php?title=IO_inside) abstraction provides a broad distinction between pure
and externally effectful computation. Languages such as Unison make it possible to introduce finer-grained, user-defined abilities,
allowing the type signature to communicate more precisely which computational services a function requires.

Effect handling often goes hand in hand with effect specification, what we've mostly talked about above is specifying what kind of
effects a computation can have in a computational environment. Effect handling provides the *interpretation* of an operation
specified by an effect signature. Effect handling concerns how effectful operations are interpreted and how the computation
continues after those operations are encountered. For example, a database effect might be interpreted using PostgreSQL,
an in-memory database, or a remote service. The effect caller, in effect, doesn't need to specify all this. 
Only the effect handler does. More generally, handlers allow the same computational description to acquire 
different "meanings" under different "interpretations/contexts". Much has been said and written about effect
handling and it is still a hot research area. A read I find insightful on current research directions of effect handling is
this blog [post](https://topos.institute/blog/2024-01-03-algebraic-effect-handlers/).

Things get a little more interesting once we introduce LLM-based AI agents into the mix. Particularly this talk of
specifying what exactly a computation might do gets crucial. Given how powerful these AI systems are getting it is
paramount that we know exactly what parts of our computational world they might touch. The shape of effects and effect
handling in programming language design and implementation rhymes quite hard with the shape of specifying the computational
reach of an AI agent. The key distinction between functions and AI agents is that an AI agent is not merely some computational
artefact that can produce output. It is a system (increasingly complex) that can request actions, interact with resources,
delegate work, modify state, and influence other computational processes.

This makes the problem of reasoning about that reach in a clear manner that much more important. It is hard to unnotice
this link between computational effects and the computational reach of AI agents. Although the latter puts up a significantly
harder and more interesting challenge, partly due to the fact that AI agents can change, they can shift and gain new capabilities
ones which, using our effect systems analogy, were not specified in their original interface ("function signature"). Increasingly these AI agents and
swarms are also operating in different computational environments. For instance, they might start working in one sandboxed
environment without certain "effect handlers" if you like e.g network access and then jump to another environment with
network access, so reasoning about their capabilities in one system might not transfer accurately into other systems the AI
system might find itself operating in. The resulting problem is not simply specifying effects. It is tracking how the
space of possible effects evolves. While the mathematics and implementation of effects and effect handlers handles compositionality
of said effects, compositional behaviour in AI agents and systems seems to take a rather different flavour: An agent might not possess
a capability directly but combine two or more of these agents and who knows what they can get up to.

How can we solve this? This is one of the questions that has been on my mind lately. The connection to effect systems came as
something of a surprise. I was particularly struck by how obvious the connection seemed once I noticed it. This seems to provide
a rich conceptual and technical foundation from which to approach the problem. What makes this exciting is also the categorical underpinnings
of algebraic effects and adjacent computational concepts. The intuition is that there is a principled way to talk about the computational
and operational reach of an AI system. Whether that intuition is correct remains a subject of significant research.
