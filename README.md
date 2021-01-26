# MONNBLANC principles for OOP

SOLID pricinples are great...

But there are some problems with them:

- they are too academic and are hard to understand for beginners
- people in a team of developers often understand them in a different way (even single responsibility principle is often understood in a different manner)

Also let me say at once: MONNBLANC is not a replacement of SOLID principles, it is an addition to them.

Besides, modern OOP is actually not what it was meant to be. 

Let's call it "mainstream OOP". 

There are lots of problems in that. 

The main of them are:

- getters/setters (it breaks encapsulation very hard)
- static methods
- mutable objects

Some developers even move away from OOP to functional programming as they think that OOP is not good enough as objects are mutable and unpredictable.

But who forbids you to design objects with immutability in mind?

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
- to collect main ***OOP antipatterns*** in one place to avoid them

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
    private final string clientFullName;
    private final string clientAddress;

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
    private final OrderRepositoryInterface orderRepository;

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

We can not change the internal organization of any real life object. 

Once a car was produced in a car fcatory, we can not change its producer, engine, body, color while we drive it.

When an HR manager in your company changes your marital status in your personal card, he/she doesn't cross out text with your marital status, in fact an HR creates a new personal card with new data. 

*Let's get back to Alan's pizzeria.*

As you could have noticed, clientFullName and clientAddress properties of Order are marked as final:

```
private final string clientFullName;
private final string clientAddress;
```

It means that we can assign their values only in the constructor which makes them immutable.

To change their value we have to create a new instance of Order.

Why should objects be immutable?

The answer is simple: we can be sure that an object's internal state is not mutated (changed) by other objects only on condition that this object is designed as immutable object.

The Order looks like this:

```
class Order {
    private final string clientFullName;
    private final string clientAddress;

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

But what if we designed this class like this?

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

    public getClientFullName(): string {
        return this.clientFullName;
    }
    
    public setClientFullName(string clientFullName): Order {
        this.clientFullName = clientFullName;
        return this;
    }

    public getClientAddress(): string {
        return this.clientAddress;
    }
    
    public setClientAddress(string clientAddress): Order {
        this.clientAddress = clientAddress;
        return this;
    }
}
```

In this case we have a getters and a setter for every field and ```clientFullName``` and ```clientAddress``` may be changed easily by any object that **is no supposed to work with Order object**:

```
var order = new Order('Alan Kay', '909-1/2 E 49th St Los Angeles, California(CA), 90011');
// !!! a setter for clientAddress is used here
// !!! and we can not be sure that Order goes to OrderStorage 
// !!! with the right internal state
order.setClientAddress('98168 Carroll Parkways, Apt. 753, 91212-4157, South Penelope, New Mexico, United States');

var orderStorage = new OrderStorage(new OrderRepository());
orderStorage.store(order);
``` 

So let's sum up:

- mutable objects cause bugs that are hard to find
- objects must be designed as immutable to be sure their internal state is not mutated by other objects

The next section of MONNBLANC principles shows you why getters and setters is a severe OOP antipattern.

## No getters and setters

This section is united with [black box object](#black-box-object) section as it is related to the same topic - encapsulation. See [black box object](#black-box-object).

## No static methods

This section is united with [black box object](#black-box-object) section as it is related to the same topic - encapsulation. See [black box object](#black-box-object).

## Black box object

This section will explain three principles at once:

- N - no getters and setters
- N - no static methods
- B - black box object

It is for a reason - all of them concern ***encapsulation***.

Let's unite them in an abbreviation ***NNB*** (No getters and setters, No static methods, Black box object).

Let's rewrite OrderStorage like this:

```
class OrderStorage {
    private OrderRepositoryInterface orderRepository;
    
    public function getOrderRepository(): OrderRepositoryInterface {
        return this.orderRepository;
    }
    
    public function setOrderRepository(OrderRepositoryInterface orderRepository): OrderStorage {
        this.orderRepository = orderRepository;
        return this.orderRepository;
    }
    
    public static function removeOrder(Order order): bool {
        // some code to remove an order from database
    }
    
    public function store(Order order): boolean {
        return this.orderRepository.insert(order);
    }
}
```

Well, maybe from the modern point of view this code is good enough.

*But it is not, it is terrible.*

First, there is a setter and a getter for ```orderRepository```.

We can replace it with anything in runtime.

This fact turns our object into a datastructure without behavior.

That's why, getters/setters approach is a hard antipattern, though it is widely used today. 

Getters/setters allow you to mutate an object's state without an object itself knowing anything about that.

Let's remember Uncle's Bob quote from above:

> “The difference between a data structure and an object is that data structures have visible data and no behavior. Objects have behavior and no visible data.”
> ~ <a href="https://twitter.com/unclebobmartin/status/1107740352516157441" rel="nofollow" target="_blank">Uncle Bob Martin</a>

If we conclude the quote above we can say that **an object is not a data structure**.

Every object is supposed to have some behavior. 

What are getters and setters for every property of an object?

Yeah, you are right - it is making our data visible to anyone!

So, let's get rid of getters/setters and pass ```OrderRepository``` to the constructor of ```OrderStorage```:

```
class OrderStorage {
    private OrderRepositoryInterface orderRepository;
    
    public constructor(OrderRepositoryInterface orderRepository) {
        this.orderRepository = orderRepository;
    }
    
    public static function removeOrder(Order order): bool {
        // some code to remove an order from database
    }
    
    public function store(Order order): boolean {
        return this.orderRepository.insert(order);
    }
}
```

Awesome! But there is one more problem: a static method ```removeOrder(Order order)```.

Why is it a problem?

Static methods break encapsulation - we can call static methods without creating an instance of ```OrderStorage```.

***Static methods break encapsulation***. Period.

Let's get rid of the static method:

```
class OrderStorage {
    private OrderRepositoryInterface orderRepository;
    
    public constructor(OrderRepositoryInterface orderRepository) {
        this.orderRepository = orderRepository;
    }
    
    public function removeOrder(Order order): bool {
        // some code to remove an order from database
    }
    
    public function store(Order order): boolean {
        return this.orderRepository.insert(order);
    }
}
```

Good, we have two principles covered from ***NNB***:

- No getters and setters
- No static methods

One more left - **Black box object**.

Black box object means that objects **must** hide their behavior and data from other objects.

In other words, it is encapsulation.

If you pass all dependencies in the constructor and stop using getters/setters and static methods, your objects are likely to become ***black boxes***!

If you order a pizza online, a pizzeria is a black box for you.

You don't care how and where a pizzeria buys tomatoes, how many cooks there are in their kitchen, what ovens they use.

You care about only one thing: tell them what pizza you want and get this pizza in 30 minutes near your door.

So the same thing should happen when you design your objects: every object must do only things it is supposed to do and other objects should know nothing what this object does under the hood.

So let's sum up:

- getters/setters is a severe atipattern for OOP
- static methods are an atipattern for OOP
- every object must be a black box for other objects

The next section of MONNBLANC principles shows you why every object should provide limited set of services.

## Limited services

## Abstract dependencies

## No null

> “I call it my billion-dollar mistake…At that time, I was designing the first comprehensive type system for references in an object-oriented language. My goal was to ensure that all use of references should be absolutely safe, with checking performed automatically by the compiler.
But I couldn’t resist the temptation to put in a null reference, simply because it was so easy to implement. This has led to innumerable errors, vulnerabilities, and system crashes, which have probably caused a billion dollars of pain and damage in the last forty years.”
> ~ Tony Hoare, inventor of ALGOL W.

## Composition only

***List of used resources:***

- <a href="https://octoperf.com/blog/2016/04/07/why-objects-must-be-immutable" rel="nofollow">Why objects must be Immutable [By YJérôme Loisel]</a>
- <a href="https://www.yegor256.com/2014/09/16/getters-and-setters-are-evil.html" rel="nofollow">Getters/Setters. Evil. Period. [By Yegor Bugayenko]</a>
- <a href="https://youtu.be/GMrjuuczZkQ" rel="nofollow">Yegor Bugayenko - What's Wrong with Object-Oriented Programming?
</a>
