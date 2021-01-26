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
- to collect main ***OOP antipatters*** in one place

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

This is the code for our worker's card:

```
class WorkerCard {
    private name: string;
    private secondName: string;
    private age: integer;
    private isMarried: boolean;

    constructor(
        name: string,
        secondName: string,
        age: integer,
        isMarried: boolean
    ) {
        this.name = name;
        this.secondName = secondName;
        this.age = age;
        this.isMarried = isMarried;
    }

    public function name(): string {
        return this.name;
    }

    public function secondName(): string {
        return this.secondName;
    }

    public function age(): integer {
        return this.age;
    }

    public function isMarried(): boolean {
        return this.isMarried;
    }
}
```

This is how we send a message about Alan's marital status to the HR department of Jsweety company:

```
// the fourth parameter here is a marital status
$workerData = new WorkerCard('Alan', 'May', 41, true);

$hr = new HR();
$hr.updateWorkerData($workerData);
```

Calling a method updateWorkerData() of HR object is actually passing a message.

We see that the HR object has its unique behavior - it accepts a message of WorkerCard type and does something under the hood.

Moreover, it is good if updateWorkerData() method could notify other objects that it updated worker data by emitting an event 'workerDataUpdated'.

It may be done like this:

```
class HR {
    // here some props of the class we don't care about now
    
    public function updateWorkerData(WorkerData $workerData): boolean {
        // here we update a worker's data, e.g. updating it in a database
        // ...
        
        // eventBus is a class injected in HR's constructor
        // which is able to notify other objects on some events
        this.eventBus.emit('workerDataUpdated', $workerData);
    }
}
```

So let's sum up:

- objects should communicate with each other by sending messages to each other
- in terms of modern OOP languages sending messages may mean two things:
  - calling a method of an object
  - sending an event if something happens (like in the example above with 'workerDataUpdated' event)
- the purpose of sending a message to another object is to get some service from that object (even calling a method name() of a WorkerCard object is actually sending a message to the WorkerCard object to get a service from this)

You can say: "I already call methods of different objects in my code so why should I care?"

But the main point here is that every object should provide only services it is supposed to.

We can hardly say that we send a message to HR object if this object has public data that can be changed by any other object without HR conrolling this process.

This situation can not be called 'message passing':

```
class HR {
    public workerRepository: WorkerRepository;
    
    // here some props of the class we don't care about now
    
    public function updateWorkerDataInDatabse(WorkerData $workerData, $databasePassword: string): boolean {
        this.workerRepository.updateWorkerData($workerData);
    }
}
```

Yeah, the method updateWorkerDataInDatabse() updates a worker's data too.

But other objects will know too much about how this work in HR object and it can hardly be called behavior as every object that calls updateWorkerDataInDatabse() must know databasePassword.

**One more example:** you wanna order a pizza.

You call a local pizzeria.

What do you need to do to get a pizza?

You need to pass a message to a pizzeria: 

"I want one pizza with tomatoes and cheese"

That's it.

You don't tell the pizzeria where they should buy products, how long to cook it, how to hire cooks.

You just send a message: "I want a pizza"

And the supposed behavior of the pizzeria is to cook a pizza.


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

