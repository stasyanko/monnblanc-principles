# MONBLANC principles for OOP

Modern OOP is actually not what it was meant to be. Let's call it "mainstream OOP". There are lots of problems in that. The main of them are:
- getters/setters (it breaks encapsulation very hard)
- static methods
- mutable objects

You will see later why these are problems. 
To understand what OOP is, let's define what an object is.
Let's ask Alan Kay, one of the founders of OOP, what an object is:
> I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages
So, the central idea of OOP is messaging.

The purposes of MONBLANC principles are:
- be simple to understand
- be precise and straightforward
- help to write maintainable OOP code

**Disclaimer**

*All examples are written in pseudo language that is understandable to most programmers who know Java, Python, PHP, Javascript and most modern OOP languages.*

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

Imagine, that you work in a company's accounting department. You got married recently and you need to change your data in your personal card of a worker. 

This personal card is stored in an HR (human resources) department. 

How do you do it? You go to a room with a filing cabinet and change your marital status yourself?

Nope. You just notify the HR department on that and only this departmant has "write" access to a filing cabinet with your personal card.

<p align="center">
  <img src="/assets/filing-cabinet.png" width="256" title="Filing cabinet">
</p>

## Object immutability

All objects must be immutable. Almost every real life object is immutable. 

Programmers model real life objects with code. 

The main idea of OOP is - build an object in its constructor and use it. 

We can not change theinternal organization of any real life object. Once a car was produced in a car fcatory, we can not change its producer, engine, body, color while we drive it.

When an HR manager in your company changes your marital status in your personal card, he/she doesn't cross out text with your marital status, in fact an HR creates a new personal card with new data. 

That's why, getters/setters approach is a hard antipattern, though it is widely used today. 

Getters/setters allow you to mutate an object's state without an object itself knowing anything about that.

## No null

## Black box object

> “The difference between a data structure and an object is that data structures have visible data and no behavior. Objects have behavior and no visible data.”
> ~ [Uncle Bob Martin](https://twitter.com/unclebobmartin/status/1107740352516157441)

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

