

# Fundamental Module 3: When a Monolith Is the Right Choice and the Cost of Distributing a System Prematurely

## 1. Introduction

When building a software application, developers need to decide how the system should be structured. Two common architectural approaches are monolithic architecture and microservices architecture.

A monolith keeps most of the application's functionality within a single application, while microservices divide the system into smaller, independently running services.

Although microservices are popular in modern software development, they are not always the best choice for every project. Sometimes, starting with a monolith is simpler, easier to manage and more practical, especially when the project is still small or the requirements are not yet fully understood.

## 2. What is Monolithic Architecture?

Monolithic architecture is an approach where the main parts of an application are developed and deployed together as a single application.

The frontend, backend logic and different modules may be organized separately within the codebase, but they usually run and deploy as one application.

For example, a college management system could have different modules such as:

- Student management
- Login and authentication
- Attendance
- Report generation
- Database management

These modules can all be part of one application without requiring separate servers or independent deployments.

### Advantages of a Monolith

- Easier to develop and understand when starting a project.
- Simpler deployment because the application is deployed as one unit.
- Easier debugging because different parts of the application are within the same system.
- Less operational complexity.
- Communication between modules can happen directly without network requests.
- Usually easier and cheaper to manage for small teams.

### Disadvantages of a Monolith

- As the application grows, the codebase can become difficult to manage.
- Changes in one module may affect other modules if the code is poorly organized.
- Scaling individual modules independently is more difficult.
- A poorly structured monolith can become tightly coupled.

## 3. What is Microservices Architecture?

Microservices architecture divides an application into smaller, independent services. Each service is responsible for a particular function and can often be developed, deployed and scaled independently.

For example, a college management system could have separate services for:

- Student management
- Authentication
- Attendance
- Notifications
- Reporting

These services communicate with one another through APIs, messages or other communication mechanisms.

### Advantages of Microservices

- Services can be deployed independently.
- Different services can be scaled based on their needs.
- Teams can work on different services independently.
- One service can use a different technology when there is a justified need.
- Smaller services can be easier to maintain when boundaries are well designed.

### Disadvantages of Microservices

- Communication between services depends on networks.
- Network failures and timeouts can occur.
- Managing multiple services requires more infrastructure and operational work.
- Data consistency becomes more difficult when data is spread across services.
- Monitoring, logging and debugging become more complicated.
- Deployment, security and testing require additional effort.

## 4. Monolith vs. Microservices

| Monolithic Architecture | Microservices Architecture |
|---|---|
| Application is deployed as one unit. | Application is divided into independently deployable services. |
| Easier to set up for smaller projects. | Requires more infrastructure and setup. |
| Modules communicate directly within the application. | Services communicate through networks, APIs or messaging. |
| Simpler debugging and testing in many small projects. | Debugging may involve multiple services. |
| Less operational overhead. | More operational overhead. |
| Scaling usually involves scaling the whole application. | Individual services can be scaled independently. |
| Suitable for small teams and evolving projects. | Useful for larger systems with clear service boundaries and independent needs. |

Neither architecture is always better. The decision depends on the size of the project, team experience, requirements, complexity and future needs.

## 5. What is Premature Distribution?

Premature distribution happens when developers divide an application into multiple independent services before there is a clear need to do so.

Instead of first understanding the application and its requirements, developers may introduce microservices because they seem modern, scalable or more professional.

However, distributing a system too early can introduce problems that could have been avoided by starting with a simpler architecture.

## 6. The Cost of Distributing a System Prematurely

### 6.1 Network Failures

In a monolith, different modules can communicate directly within the same application. In a distributed system, services often need to communicate over a network.

Network communication introduces problems such as:

- Connection failures.
- Timeouts.
- Slow responses.
- Requests being lost or repeated.
- Services becoming temporarily unavailable.

This means developers need to handle failures that may not exist in the same way when modules communicate within a single application.

### 6.2 Data Consistency

In a monolith, different modules may access the same database and use transactions to maintain consistency.

In microservices, different services may own separate databases. When one service updates data, another service may not immediately receive the updated information.

This can lead to eventual consistency, where data becomes consistent after some time rather than immediately.

Developers may need to implement additional mechanisms such as events, retries, compensating actions or synchronization processes.

### 6.3 Extra Operational Work

Running multiple services requires additional work compared to running a single application.

Developers may need to manage:

- Multiple deployments.
- Service configurations.
- Monitoring and logging.
- Network communication.
- Security between services.
- Container management.
- Service discovery.
- CI/CD pipelines.

These tasks can consume time and resources that could otherwise be spent developing the actual features of the application.

### 6.4 Wrong Service Boundaries

When a system is divided into services too early, developers may not yet understand which parts of the application should be separated.

For example, the authentication module and student module may initially seem like separate services. However, if they frequently depend on one another and share many operations, separating them may introduce unnecessary communication and complexity.

As the requirements become clearer, the original service boundaries may turn out to be incorrect, leading to restructuring and additional development work.

## 7. What is a Modular Monolith?

A modular monolith is an application that is deployed as a single unit but organized into separate modules with clear responsibilities.

Instead of placing all code together without structure, developers organize the application into modules that handle specific areas of functionality.

For example:

```text
Application
│
├── Authentication Module
│
├── Student Module
│
├── Attendance Module
│
├── Report Module
│
└── Database
```

Each module should have its own responsibilities and avoid unnecessary dependencies on other modules.

A modular monolith allows developers to maintain a simpler deployment structure while keeping the code organized. If a particular module later needs to become an independent service, its separation may be easier if the boundaries were designed properly from the beginning.

### Advantages of a Modular Monolith

- Keeps the application organized.
- Reduces unnecessary complexity.
- Makes development and testing easier.
- Allows modules to have clear responsibilities.
- Avoids unnecessary network communication.
- Makes future architectural changes easier when modules are well separated.

## 8. When Should We Choose a Monolith?

A monolith is often a reasonable choice when:

- The project is small or medium-sized.
- The team is small.
- Requirements are still changing.
- The application does not need independent scaling for different modules.
- Developers want to focus on building and delivering features.
- There is no strong reason to introduce distributed infrastructure.

Microservices may become more appropriate when the system has clear boundaries, different components need independent scaling or deployment, teams need greater autonomy, or there are other specific technical or organizational requirements.

## 9. Architecture Decision Record (ADR)

An Architecture Decision Record (ADR) is a document used to record an important architectural decision, including the problem, the options considered, the decision made and the reasons behind it.

### Example ADR: Choosing a Modular Monolith

**Title:** Choosing a Modular Monolith for the Application

**Context:**

The application is still under development, and the team is relatively small. The requirements may change as new features are added and feedback is received. Introducing microservices at this stage would require additional infrastructure, service communication, monitoring and deployment management.

**Options considered:**

1. Monolithic architecture.
2. Microservices architecture.
3. Modular monolithic architecture.

**Decision:**

We decided to use a modular monolith because it allows us to develop and maintain the application more easily while keeping the code organized into separate modules.

**Reasons for the decision:**

- The project does not currently require independently deployed services.
- The team can manage a single application more easily.
- It reduces network-related problems and operational overhead.
- Modules can be separated by responsibility.
- The architecture can be reconsidered when the application's requirements grow.

**Consequences:**

- The application will be simpler to develop, deploy and test.
- The team will have fewer infrastructure responsibilities.
- Modules must be designed carefully to avoid tight coupling.
- If the application grows significantly, some modules may need to be separated into independent services in the future.

## 10. Conclusion

After comparing monolithic architecture and microservices, I learned that distributing a system too early can introduce unnecessary complexity. Although microservices offer benefits such as independent scaling and deployment, they also bring additional challenges related to network failures, data consistency, operational work and service boundaries.

I concluded that a modular monolith is often a better starting point when the project is still small and its requirements are evolving. It allows developers to keep the system organized without introducing unnecessary distributed-system complexity. Microservices should be considered when there is a real need for them rather than choosing them simply because they are popular.

