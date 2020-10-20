# MONBLANC principles for OOP

The purposes of MONBLANC principles are:
- be simple to understand
- be precise and straightforward
- help to write maintainable OOP code

MONBLANC principles are:

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
Imagine, that you work in a company's accounting department. You got married recently and you need to change your data in your personal card of a worker. This personal card is stored in an HR (human resources) department. 
How do you do it? You go to a room with a filing cabinet and change your marital status yourself?
Nope. You just notify the HR department on that and only this departmant has "write" access to a filing cabinet with your personal card.

<p align="center">
  <img src="/assets/filing-cabinet.png" width="256" title="Filing cabinet">
</p>

## Object immutability

All objects must be immutable. Almost every real life object is immutable. Programmers model real life objects with code. The main idea of OOP is - build an object in its constructor and use it. We can not change theinternal organization of any real life object. Once a car was produced in a car fcatory, we can not change its producer, engine, body, color while we drive it.
When an HR manager in your company changes your marital status in your personal card, he/she doesn't cross out text with your marital status, in fact an HR creates a new personal card with new data. 
That's why, getters/setters approach is a hard antipattern, though it is widely used today. 

## No null

## Black box object

## Limited services

## Abstract dependencies

## No static methods

## Composition only
