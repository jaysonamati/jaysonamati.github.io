---
layout: post
title:  "What Rust's Ownership System can teach us about Property Rights"
date:   2023-10-20 07:08:43 +0300
categories: rust programming-language ownership property-rights
---

Recently, an interesting thought occurred to us on the connection between Rust's Ownership system and property rights in economic theory. It seems like one can
take the whole correspondence between programming languages and mathematical theories to another level. In Rust every value has an owner, a function or context
that is allowed to modify this value, hmm sounds familiar, doesn't it? For us plebs in the early 21st obviously. Yeah, it's a lot like what we currently use as
the a system of organizing resources. It's where economic actors have ownership rights to resources and they can use them however they want including changing the
resource. Now, it's not a one to one correspondence but it does give one reason to ponder and it's pretty close. Rust is a programming language and this ownership
system is crucial in making it versatile in building truly concurrent and safe programs. The system ensures that values are not mutated willy nilly and hence
every caller that uses a value has a guarantee that indeed the value they expect hasn't been changed without their explicit knowledge if they have the ownership
rights. This is useful in reasoning about the behaviour of programs and hence leads to system that perform without memory bugs in production. Another important
part of Rust's ownership system is lifetime, every value has a scope in which it's available to be used, both as a mutable and an immutable value. Once the value
is out of scope it's not available to be used. This makes Rust a memory efficient language and also enhances it's safety features.

Back to economics, the first correspondence is rather clear and there are a couple of things we can glean from it. Firstly values can only be mutated if ownership
is adhered to, this reduces conflict when it comes to what can use it and how they can use it. Of course, there is the closely related concept of borrowing
where a caller that doesn't own a value can temporarily have permission (a reference) to use it in any way, and return it when done. This is alot like how one
can borrow a cup but they have to return it once they are done using it. In Rust if a borrower doesn't return a reference, the program won't compile.
Wonder what the compiler would correspond to in the economic world? Do property rights help in the organization of resources in economics? Some would argue that
without them we (current human civilization) would result to savagery. What would support such a claim? What is savagery? Good resource organization in our case
means that resources are utilized in a way that benefits **all** participants. An argument could be made how the current model doesn't do this very well,
considering we are not including a large percentage of actual participants (that tree outside, etc), digress. In a savage world benefits are not shared equally,
if at all and the system is rampant with waste and unrealized potential (utilization is narrow and limited). This is what property rights aim to prevent. From our
point of view it seems that if implemented properly and all actors in an economy adhere to them then property rights do work up to a point. Why do we
still have resource organization problems in spite of the fact that we have in place decent property rights? We don't have a good answer to that now, so we can't
say much about it. Can Rust give us clues?

Imagine if you will, that a correct program (one that compiles without the unsafe feature) written in rust was an economy with the resources being values (or
even types, there is an interesting argument that can be made about the relationship between type theory and resource but that's for a later time), and functions
that use and produce those value as economic actors. These actors can exchange resources with each other. What does an exchange entail? One may ask, and an
answer to that lies in the semantics of any particular program or function. For instance, have that function A is one that requires a Vector input (you can think
of this as a list of values) and in turn gives a sorted list back. Function A can't produce lists by itself and hence would require another source of lists. This
is where function B comes in. Function B is a little interesting as it produces Vectors but only if you give it a sentence. For the sake of argument we are going
to imagine that IO operations are part of the economy and that they model a function that is all powerful but doesn't know how to produce a sorted list, only
sentences. So for an exchange to happen, the only thing that is trivially produced is a sentence, with this the IO function can exchange that sentence for a
vector with function B being the only other party to this exchange. Now that function B has a Vector they can exchange it for a sorted list and the only producer
of sorted list they are aware of is function A, so function A happily gets a Vector and produces a sorted list which they give its ownership to function B. Function B hasn't still given IO function what they required and since now they have possession of a sorted list they can give it to IO who is satisfied and the
exchange is complete. This is a lot like a barter system of organizing resources but it works, with a lot of waiting. All parties benefit and the system can keep
existing. As we follow the exchanges (while sweeping a lot of assumptions under the rug) we can see that ownership of values of interest changes so as to ensure
that no party can have a value they own abruptly changed (or taken) without their explicit permission or borrowing. If the real world worked like this, maybe it
did at a time, things would be swell. Every actor would get exactly what they need to produce what they can. Of course, it isn't as simple as this and we are not
necessarily advocating that we run the economy like the Rust compiler, but we found the parallels between the two to be uncanny and hence interesting.

The last part that doesn't have a direct correspondence to a real economy as of now, not one that we know of anyway. This is the lifetime property of Rust values.
After a value is no longer used by a function it is dropped out of scope and also from memory, hence sometimes we have to explicitly declare for how long a
specific function or value will live for and hence the compiler knows when to kill it, so to speak. This seems like a good idea to have in the actual economy,
when we are done with a resource we can simply destroy it, but it not so straightforward as in the real world nothing is every really destroyed. It is only
converted to another form. In a certain sense, current human civilization lives as if it is the case that things are destroyed once an economic agent is done
deriving utility from a resource when clearly it is not the case. This strategy is useful in the Rust universe but unfortunately it is proving to be unsavory for
other economic agents that are not humans or are not artifacts of our society. What lessons can we borrow from rusts lifetime system. To get a grasp on this we
need to investigate the utility this system has to programs written in Rust. Lifetimes are used to ensure the validity of borrows, so we can't borrow a value
whose lifetime has ended. For an economy to have this feature, we would need a way to describe formally when a resource's lifetime has ended in the context of
the economy, this is possible for local contexts but unconceivable globally (when we consider all possible entities). So is this futile? We don't know but we
can't rule out anything.

This was a fun excursion into the workings of rust and how they correspond to concepts in economic systems. Wonder what purely functional languages like haskell
have to say about 'real world' things such as resource coordination? Stay tuned!
