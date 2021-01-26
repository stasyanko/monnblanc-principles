# MONNBLANC principles for OOP

SOLID pricinples are great...

But there are some problems with them:

- they are too academic and are hard to understand for beginners
- people in a team of developers often understand them in a different way (even single responsibility principle is often understood in a different manner)

Besides, modern OOP is actually not what it was meant to be. 

Let's call it "mainstream OOP". 

There are lots of problems in that. 

The main of them are:

- getters/setters (it breaks encapsulation very hard)
- static methods
- mutable objects

Some developers even move away from OOP to functional programming as they think that OOP is not good enough as objects are mutable and unpredictable.

But who forbids you to design objects with immutability in mind?

You will see later why these are problems. 

First of all let's define ***what an object is.***

It is interesting, that many people who use OOP daily have never thought of what an object actually is.

There are lots of misconceptions about that.

So, the first definition is by ***Alan Kay*** who is considered to be a father of OOP.

> I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages
So, the central idea of OOP is messaging.

The second definition is by ***Uncle Bob Martin:***

> “The difference between a data structure and an object is that data structures have visible data and no behavior. Objects have behavior and no visible data.”
> ~ <a href="https://twitter.com/unclebobmartin/status/1107740352516157441" rel="nofollow" target="_blank">Uncle Bob Martin</a>

***So let's conclude what objects are:***

- objects are similar to biological cells and/or individual computers
- objects have behavior
- objects have no visible data

***The purposes of MONNBLANC principles are:***

- to be ***simple*** to understand
- to be precise and straightforward
- to be ***beginner friendly***
- to help to write maintainable OOP code
- to collect main ***OOP antipatterns*** in one place

**Disclaimer**

*All examples are written in pseudo language that is understandable to most programmers who know Java, Python, PHP, Javascript and most modern OOP languages.*

*The pronciples are explained with practical examples.*

*Alan owns a pizzeria and he wants to make online ordering for his pizzeria.*

*We will develop online ordering of pizza using MONNBLANC principles.*

**MONNBLANC principles are:**

**M** - [messaging](#messaging)

**O** - [object immutability](#object-immutability)

**N** - [no getters and setters](#no-getters-and-setters)

**N** - [no static methods](#no-static-methods)

**B** - [black box object](#black-box-object)

**L** - [limited services](#limited-services)

**A** - [abstract dependencies](#abstract-dependencies)

**N** - [no null](#no-null)

**C** - [composition only](#composition-only)

## Messaging

> “I’m sorry that I long ago coined the term “objects” for this topic because it gets many people to focus on the lesser idea. The big idea is messaging.”
> ~ Alan Kay

Objects must be like small computers that talk to each other via messaging.

We see that the HR object has its unique behavior - it accepts a message of WorkerCard type and does something under the hood.

The class with Order looks like this:

```
class Order {
    private string clientFullName;
    private string clientAddress;

    public constructor(
        string clientFullName,
        string clientAddress
    ) {
        this.clientFullName = clientFullName;
        this.clientAddress = clientAddress;
    }

    public clientFullName(): string {
        return this.clientFullName;
    }

    public clientAddress(): string {
        return this.clientAddress;
    }
}
```

For storing a new order let's create OrderStorage:

```
class OrderStorage {
    private OrderRepositoryInterface orderRepository;

    public constructor(OrderRepositoryInterface orderRepository) {
        this.orderRepository = orderRepository;
    }

    public function store(Order order): boolean {
        return this.orderRepository.insert(order);
    }
}
```

To store a new Order we will write this code:

```
var order = new Order('Alan Kay', '909-1/2 E 49th St Los Angeles, California(CA), 90011');
var orderStorage = new OrderStorage(new OrderRepository());

orderStorage.store(order);
```

In terms of most languages (like Java, Javascript, PHP etc) sending a message to an object means calling a proper method which prodives some service to another object.

Calling store() method of OrderStorage is actually sending a message to this object to get a service of storing a new Order.

But you could say: "I already call methods of different objects. ***Why should I care about messaging?***"

Well, calling a method of an object is not always equal to messaging.
    
To be able to call a method call an act of messaging one principle must be kept for designing an object:

*"Every object should be a specialist only in its services and should know nothing of how things work under the hood in other objects"*

You will understand it better in the next sections of MONNBLANC principles.

So let's sum up:

- objects should communicate with each other by sending messages to each other
- in terms of modern OOP languages sending messages simply means calling a method of an object to get some service from it

## Object immutability

All objects must be immutable. Almost every real life object is immutable. 

Programmers model real life objects with code. 

The main idea of OOP is - build an object in its constructor and use it. 

We can not change theinternal organization of any real life object. 

Once a car was produced in a car fcatory, we can not change its producer, engine, body, color while we drive it.

When an HR manager in your company changes your marital status in your personal card, he/she doesn't cross out text with your marital status, in fact an HR creates a new personal card with new data. 

That's why, getters/setters approach is a hard antipattern, though it is widely used today. 

Getters/setters allow you to mutate an object's state without an object itself knowing anything about that.

## No getters and setters
## No static methods
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

## No null

## Composition only

***List of used resources:***

