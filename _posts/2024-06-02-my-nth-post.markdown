---
layout: post
title:  "Dependently Typed Sequential Decision Problems"
date:   2024-09-12 07:08:43 +0300
categories: dependent-types decision-problems formal-system dynamical-systems
---
The following post was made while exploring a construction of a Sequential Decision Problem using [AlgebraicJulia](https://www.algebraicjulia.org/). AlgebraicJulia
gives a collection of various applied category theoretic notions in the Julia programming language. The motivation for this is that Sequential Decision Problems are
a very interesting object of study as they describe various problems using the same structure.? In the first part we explore what SDPs are and an implementation
in the Agda, and in the second part we look at an implementation using algebraicJulia.

## Sequential Decision Problems

To begin with we'll first give a primer to Sequential Decision Problems (SDPs) as formalized using dependent types. If you are not familiar with dependent types a good
introduction is provided [in this text](https://golem.ph.utexas.edu/category/2010/03/in_praise_of_dependent_types.html).We won't go into any details pertaining the type theory for dependent types here. A good one liner description of dependent types is
"A dependent type system is a type system that increases the expressiveness of a programming language". Programming languages that make use of dependent types are much
more expressive than ones that use simple type systems, so much so that one can use them to write mathematical proofs. Some well know examples of dependently typed
languages include [Agda](https://agda.readthedocs.io/en/v2.6.4.3-r1/getting-started/what-is-agda.html), [Lean](https://lean-lang.org/) and [Idris](https://www.idris-lang.org/). We'll use Agda in this post to give a formal description of Sequential Decision Problems.

The following is essentially a summary of this [paper](https://arxiv.org/abs/1610.07145v5) giving a comprehensive look at SDPs. SDPs, as given in the publication are problems in which an actor is
required to make choices of actions in a sequential manner upon observing a particular state of the world. To sufficiently give the data of a SDP one needs to give the
following:

- A state
- An Action
- A Policy

Getting solutions to Sequential Decision Problems is slightly out of scope of this brief introduction to SDPs

### State

A state of SDP simply describes the information available to an actor for decision making. In a dependently typed language a representation of state is given by a Type.
In agda this is given by `State : Set`
You can think of `Set` as a general Type, the colon can be read as "of type".

### Actions

An action is the set of controls an actor has at any particular state. Controls are anything that can be applied to a state to yield a new state. A good way to
visualize what an action is an edge in a directed graph where the source node is a state and the target node is the next state. To give a description of an Action in
agda we give the following postulate `postulate Action : State -> State`. It essentially says that given an action is the type of functions from State to State.

### A policy

In most real world situations there is an element of uncertainty when taking actions(making decision), the next state after a control is applied is not exactly know
this could include a list of possible states, or a probability weighted list of next possible states. In order to account for this in decision making, it is prudent to
consider that actions may not always be optimal for a given state given the uncertainty of the outcome. In order to surpass this we, instead of giving a list of
actions to be applied at each state, use a Policy, which is described as a function that takes a given state as input and gives an action that is applied to that
particular state, this implies that actions are determined per state and not given at the "start" of the decision making process as a plan. We use the following type
to represent policies in agda `Policy : State -> Action`

### PolicySequence

Given a policy we can always make a policy sequence that traverses the "state space" using a set of actions. The resulting trajectory can be represented in agda
as `XYSeq` which is a sequence of states and actions at a particular state. This construction is important in solving the Sequential Decision problem as one can
easily compute the optimal sequence of Policies from this. To do this one needs to map the value of each policy using the given reward function and the reward unit.

`PolicySequence`s are crucial in solving SDPs as it is in using them that we can find the solution of a Sequential Decision Problem. This means for instance that
given a policySequence and a suitable value function we have that a given policySequence is the optimal one if the value of all other policySequences is less than
the value of the optimal PolicySequence, this is given by the following type and associated function

```agda
OptPolicySeq : {t n : ℕ} → PolicySeq t n → Set
OptPolicySeq { t } { n } ps = ∀ (ps' : PolicySeq t n) → val ps' ≤ₗ val ps
```

With the above we are now able to solve SDPs using bellman induction, this method given and SDP, a value function of the form `val : {t n : ℕ} → (ps : PolicySeq t n) → (x : X t) → Val` which is used to evaluate the measure of rewards along a trajectory (`XYSeq`) that is given with by the Policy Sequence given by `ps`.

To be able to compute the bellman induction we need this Equality to be true `BellmanEq : (t n : ℕ) → (p : Policy t) → (ps : PolicySeq (suc t) n) → (x : X t) →
            val (p ∷ ps) x ≡ measure (fmapM (reward t x (p x) ⊕ₗ val ps) (next t x (p x)))`,
This is referred to as the Bellman's Equality.

With bellman's principle and a suitable value function a solution to a Sequential Decision problem is the optimal Policy Sequence given by the type
`OptPolicySeq`. Bellman induction is one of the computations we can do in order to "derive" this sequence.

In the second part of this post we shall look at how all of this is implemented using AlgebraicJulia. See you cyber-space cowboy.
