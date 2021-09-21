# microservices-in-action
Microservices promise a better way to sustainably deliver business impact. Rather than a single monolithic unit, applications built using microservices are made up of loosely coupled, autonomous services. By building services that do one thing well, you can avoid the inertia and entropy of large applications.

When we started working with microservices, we quickly realized that building smaller and more self-contained services was only one part of running a stable and business-critical application

Classical software engineering practice advocates high cohesion and loose coupling as desirable properties of a well-engineered system. A system that has these properties will be easier to maintain and more malleable in the face of change.

Gather together the things that change for the same reasons. Separate those things that change for different reasons.


1
Designing and running microservices
This chapter covers

Defining a microservice application
The challenges of a microservices approach
Approaches to designing a microservice application
Approaches to running microservices successfully
Software developers strive to craft effective and timely solutions to complex problems. The first problem you usually try to solve is: What does your customer want? If you’re skilled (or lucky), you get that right. But your efforts rarely stop there. Your successful application continues to grow: you debug issues; you build new features; you keep it available and running smoothly.

Even the most disciplined teams can struggle to sustain their early pace and agility in the face of a growing application. At worst, your once simple and stable product becomes both intractable and delicate. Instead of sustainably delivering more value to your customers, you’re fatigued from outages, anxious about releasing, and too slow to deliver new features or fixes. Neither your customers nor your developers are happy.

Microservices promise a better way to sustainably deliver business impact. Rather than a single monolithic unit, applications built using microservices are made up of loosely coupled, autonomous services. By building services that do one thing well, you can avoid the inertia and entropy of large applications. Even in existing applications, you can progressively extract functionality into independent services to make your whole system more maintainable.

When we started working with microservices, we quickly realized that building smaller and more self-contained services was only one part of running a stable and business-critical application. After all, any successful application will spend much more of its life in production than in a code editor. To deliver value with microservices, our team couldn’t be focused on build alone. We needed to be skilled at operations: deployment, observation, and diagnosis.

1.1 What is a microservice application?
A microservice application is a collection of autonomous services, each of which does one thing well, that work together to perform more intricate operations. Instead of a single complex system, you build and manage a suite of relatively simple services that might interact in complex ways. These services collaborate with each other through technology-agnostic messaging protocols, either point-to-point or asynchronously.

This might seem like a simple idea, but it has striking implications for reducing friction in the development of complex systems. Classical software engineering practice advocates high cohesion and loose coupling as desirable properties of a well-engineered system. A system that has these properties will be easier to maintain and more malleable in the face of change.

Cohesion is the degree to which elements of a certain module belong together, whereas coupling is the degree to which one element knows about the inner workings of another. Robert C. Martin’s Single Responsibility Principle is a useful way to consider the former:

Gather together the things that change for the same reasons. Separate those things that change for different reasons.

In a monolithic application, you try to design for these properties at a class, module, or library level. In a microservice application, you aim instead to attain these properties at the level of independently deployable units of functionality. A single microservice should be highly cohesive: it should be responsible for some single capability within an application. Likewise, the less that each service knows about the inner workings of other services, the easier it is to make changes to one service — or capability — without forcing changes to others.

To get a better picture of how a microservice application fits together, let’s start by considering some of the features of an online investment tool:

Opening an account
Depositing and withdrawing money
Placing orders to buy or sell positions in financial products (for example, shares)
Modeling risk and making financial predictions
Let’s explore the process of selling shares:

A user creates an order to sell some shares of a stock from their account.
This position is reserved on their account, so it can’t be sold multiple times.
It costs money to place an order on the market — the account is charged a fee.
The system needs to communicate that order to the appropriate stock market.
Figure 1.1 shows how placing that sell order might look as part of a microservice application.

You can observe three key characteristics of microservices in figure 1.1:

- Each microservice is responsible for a single capability. This might be business related or represent a shared technical capability, such as integration with a third party (for example, the stock exchange).

- A microservice owns its data store, if it has one. This reduces coupling between services because other services can only access data they don’t own through the interface that a service provides.

- Microservices themselves, not the messaging mechanism that connects them nor another piece of software, are responsible for choreography and collaboration — the sequencing of messages and actions to perform some useful activity.

- Each microservice can be deployed independently. Without this, a microservice application would still be monolithic at the point of deployment.

- A microservice is replaceable. Having a single capability places natural bounds on size; likewise, it makes the individual responsibility, or role, of a service easy to comprehend.

SOA :- uses service bus or orchestrator . downside is a lot of logic goes in service bus and changing one system changes other

microservices :- they are responsible for messaging not external software

Monolithic applications typically scale through horizontal duplication: deploying multiple, identical instances of the application. This is also known as cookie-cutter, or X-axis, scaling. Conversely, microservice applications are an example of Y-axis scaling, where you decompose a system to address the unique scaling needs of different functionality.


The Z axis refers to horizontal data partitions: sharding. You can apply sharding to either approach — microservices or monolithic applications — but we won’t be exploring that topic in this book.


1.1.2 Key principles
Five cultural and architectural principles underpin microservices development:

Autonomy
Resilience
Transparency
Automation
Alignment




