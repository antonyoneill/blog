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
* **Infrastructure Layer**  
  Arguably the most fundamental layer, this layer is responsible for external services, such as persistence (database, search engines), mailers, loggers, third-party APIs.
  The Infrastructure layer usually has it's own Model of the application, often nested objects within the Domain Model must be separated out into individual tables, for a relational database for example. Or Elastic Search documents need to be modeled for easy insertion and retrieval.

Having clear boundaries facilitates several things, easier testing, more maintainable code, and most importantly it reduces vendor/technology "lock in". Consider a typical application, where there's a need to move from a relational database to a NoSQL one. This could be a huge undertaking, as in most systems these relations, and SQL concerns are baked into most classes. In DDD the persistence is isolated in the Infrastructure layer - provided you don't break the contract, this becomes a very easy peice of work.

A clear downside to DDD though is that you end up writing many many mappers of models. Remember that almost each layer contains it's own Model of the world.

A good example of DDD in the real world comes from a previous role: [`boclips/videos`](https://github.com/boclips/videos/tree/master/video-service/src/main/kotlin/com/boclips/videos/service). You can see the clear boundaries of the layers here. The project is written in Kotlin and uses Spring Boot and Aspect Oriented Programming to simplify a lot of the dependency injection.

## Clean Architecture

> This is a pattern that I am fairly new to, but will do my best to describe some of the key aspects of it that I have picked up over the last month.

> In general it seems to be a less regimented form of DDD. Layers exist but are not as clearly defined, and different terminology is used to describe some similar DDD concepts.

Using Clean Architecture, you are encouraged to move business logic into individual, well defined, usecases. You would typically follow the patterns for the framework you're using, but separate out the usecases from the boiler plate. This allows you to execute the same business logic from within a HTTP controller, a command line processor, or user entry points to your application.


* **Gateways**  
  Gateways provide access to third party services, APIs, databases, etc.

  Specifics related to these external services should be encapsulated within these gateways. The defined interfaces should be well designed to ensure that the implementation of the gateway is does not leak into the application.

  Consider a database gateway, that may have an interface such as
  
  ```typescript
  interface DatabaseGateway {
    insertTodo: (todo: Todo): Promise<void>;
    getTodo: (id: number): Promise<Todo>;
  }
  ```
  
  Provided the gateway encapsulates all implementation logic, it makes changing that implementation to a different technology very simple.

* **Usecases**  
  Usecases should provide an abstraction over business logic. They may use other usecases (composite usecases), or interact with Gateways etc.
  
  Other usecases and gateways should be referenced using Dependency Injection. Some frameworks provide this out of the box (Spring Boot for example uses Annotations and Aspect Oriented Programming), sometimes a simple AppContainer can suffice.

  For example, if an application wants to create a Todo item then it may validate the item, then store it in the database for lookup later, then send an email alert that it has been created. This composite usecase may look something like

  ```typescript
  const createTodo = ({getValidateTodo, getDatabase, getMailer}) => async (todo: Todo): Promise<CreateTodoResponse> => {
      const validationResult = getValidateTodo()(todo);

      if (!validationResult.success) {
          return {
              success: false,
              error: {
                  message: "Validation errors occurred: " + validationResult.errors.join(', ')
              }
          }
      }

      const persistanceResult = await getDatabase().insertTodo(todo);

      if (!persistanceResult.success) {
          return {
              success: false,
              error: {
                  message: "Persistance failed: " + persistanceResult.errors.join(', ')
              }
          }
      }

      await getMailer().sendNewTodoEmail(todo)
      
      return {
          success: true,
          error: null
      }
  }
  ```

* **Helpers**  
  Helpers are an abstraction away from some of the usecases. The distinction between the two are very subtle. In my mind, helpers are a way of defining very simple matters, things like field level validators, regex patterns, time manipulation etc.

  In some projects, these helpers can be used on both the frontend and backend. In these scenarios it can make sense to produce two different AppContainers, one for web, and one for serverside.

### References

- [The Clean Architecture Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [Made Tech - Clean Architecture](https://github.com/madetech/clean-architecture)
- [lukemorton.co.uk source](https://github.com/lukemorton/lukemorton.co.uk/tree/a4343251f4540ea75d867e73b12309a65d62f186) 

# Todo

- [ ] Provide more detail on MVC, inc +/-ves
- [ ] Add references
