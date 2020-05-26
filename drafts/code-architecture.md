# Code Architecture

Modern software companies try to follow best practises, these come in terms of communications, workflow, testing, and architecture.

When it comes to architecture there are several types of concepts, from deployment architecture -- how will your application be deployed to end users -- to code architecture -- how do you write and organise your code.

There are many guides that talk about deployment architecture, and I think this is the most common discussion which perhaps most developers will have an opinion on.

Code architecture patterns seem to be something that few developers are familiar with, with exception to the Model-View-Controller pattern.

I'll outline some different patterns below and discuss some advantages and disadvantages of these:

## Model View Controller

One of the most popular design patterns, the Model View Controller pattern designates clear boundaries between the Model (some perisitance and type definition), View (the user interface, a web page, REST API, command line), and Controller (the business logic that performs actions on models)

Most web frameworks follow the MVC pattern, Ruby on Rails is a prime example where folder structure help define the boundaries.

_tbc_

## Domain Driven Design

A popular, although fringe design pattern is Domain Driven Design, affectionally known as DDD. This pattern takes boundaries to a higher level than MVC.

DDD maintains four layers, using a modern programming language you would typically use namespaces to ensure the concerns do not overlap.

* **Presentation Layer**
  Responsible for anything user facing -- a REST API, rendered web page, command line interface/interpretter -- this layer decides what Application command to run (based on routing/command parameters), maps incoming requests to a Domain model, and maps Application command responses to the relevant presentation response.
* **Application Layer**
  Responsible only for defining Application commands that the application can provide, such as creating a todo task, marking it complete, editing it, etc.
  These commands use Domain services to acheive the command goal. They should ideally be written in such a way that it is clear to a non-programmer what is going on, and what the purpose of the command is.
  In-depth concerns (i.e. how to create a todo task, ins and outs of validation) should not be raised here, instead these lower-level tasks should be refactored down into Domain services.
* **Domain Layer**
  This layer contains the Models of the application, using real world terms. A shared nomanculture is extremely important when using DDD as it helps build empathy with the users of the system, but also enables easier discussion with all stakeholders involved.
  Services are defined in this layer that operate in terms of Domain Models. They have access to Infrastructure services, and other Domain services. While these services have access to Infrastructure concerns, the lower-level details are abstracted away.
  For example, the Domain may wish to persist a Domain Model, it will be empowered to request the Infrastructure persistence service to store the model, but in terms of what and how that happens does not matter to the Domain Service.
* **Infrastructue Layer**
  Arguably the most fundamental layer, this layer is responsible for external services, such as persistence (database, search engines), mailers, loggers, third-party APIs.
  The Infrastructure layer usually has it's own Model of the application, often nested objects within the Domain Model must be separated out into individual tables, for a relational database for example. Or Elastic Search documents need to be modeled for easy insertion and retrieval.

Having clear boundaries facilitates several things, easier testing, more maintainable code, and most importantly it reduces vendor/technology "lock in". Consider a typical application, where there's a need to move from a relational database to a NoSQL one. This could be a huge undertaking, as in most systems these relations, and SQL concerns are baked into most classes. In DDD the persistence is isolated in the Infrastructure layer - provided you don't break the contract, this becomes a very easy peice of work.

A clear downside to DDD though is that you end up writing many many mappers of models. Remember that almost each layer contains it's own Model of the world.

## Clean Architecture

_tbc_
