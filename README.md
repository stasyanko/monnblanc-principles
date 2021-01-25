# MONBLANC principles for OOP

Modern OOP is actually not what it was meant to be. 

Let's call it "mainstream OOP". 

There are lots of problems in that. The main of them are:

- getters/setters (it breaks encapsulation very hard)
- static methods
- mutable objects

Some developers even move away from OOP to functional programming as they think that OOP is not good enough as objects are mutable and unpredictable.

But who forbids you to design objects with immutability in mind?

You will see later why these are problems. 

First of all let's define what an object is.

It is interesting, that many people who use OOP daily have never thought of what an object actually is.

There are lots of misconceptions about what an object is.

So, the first definition is by Alan Kay who is considered to be a father of OOP.

> I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages
So, the central idea of OOP is messaging.

The second definition is by Uncle Bob Martin:

> “The difference between a data structure and an object is that data structures have visible data and no behavior. Objects have behavior and no visible data.”
> ~ <a href="https://twitter.com/unclebobmartin/status/1107740352516157441" rel="nofollow" target="_blank">Uncle Bob Martin</a>

***So let's conclude what objects should be:***

- objects are like biological cells and/or individual computers
- objects have behavior
- objects have no visible data

The purposes of MONBLANC principles are:
- to be simple to understand
- to be precise and straightforward
- to be beginner friendly
- to help to write maintainable OOP code

**Disclaimer**

*All examples are written in pseudo language that is understandable to most programmers who know Java, Python, PHP, Javascript and most modern OOP languages.*

*The pronciples are explained as a story of a worker Alan from Jsweety factory.*

*He is a financist in the financial department.*

*Jsweety produces candies and chocolate.*

*We will automate the business processes of Jsweety factory using MONBLANC principles.*

**MONBLANC principles are:**

**M** - [messaging](#messaging)

**O** - [object immutability](#object-immutability)

**N** - [no null](#no-null)

**B** - [black box object](#black-box-object)

**L** - [limited services](#limited-services)

**A** - [abstract dependencies](#abstract-dependencies)

**N** - [no static methods](#no-static-methods)

**C** - [composition only](#composition-only)

## Messaging

> “I’m sorry that I long ago coined the term “objects” for this topic because it gets many people to focus on the lesser idea. The big idea is messaging.”
> ~ Alan Kay

Objects must be like small computers that talk to each other via messaging.

Imagine, that you work in a company's accounting department. 

Alan got married recently and he needs to change data in his personal card of a worker. 

This personal card is stored in an HR (human resources) department. 

How does he do it? 

He goes to a room with a filing cabinet and changes his marital status on his own?

Nope. 

He just notifies the HR department on that and only this departmant has "write" access to a filing cabinet with his personal card.

<p align="center">
  <img src="/assets/filing-cabinet.png" width="256" title="Filing cabinet">
</p>

## Object immutability

All objects must be immutable. Almost every real life object is immutable. 

Programmers model real life objects with code. 

The main idea of OOP is - build an object in its constructor and use it. 

We can not change theinternal organization of any real life object. 

Once a car was produced in a car fcatory, we can not change its producer, engine, body, color while we drive it.

When an HR manager in your company changes your marital status in your personal card, he/she doesn't cross out text with your marital status, in fact an HR creates a new personal card with new data. 

That's why, getters/setters approach is a hard antipattern, though it is widely used today. 

Getters/setters allow you to mutate an object's state without an object itself knowing anything about that.

## No null

## Black box object

Let's get back to our company and the way its departments communicate.

In fact, every department in a company is a black box.

If we conclude the quote above we can say that **an object is not a data structure**.

Every object is supposed to have some behavior. 

What are getters and setters for every property of an object?

Yeah, you are right - it is making our data visible to anyone!

Having a getter and a setter for every property is actually turning our object into a data structure!

## Limited services

## Abstract dependencies

## No static methods

## Composition only

***List of used resources:***

