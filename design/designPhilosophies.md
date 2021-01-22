### Design Philosophies 

### 12-factor app
set of twelve best practices to develop applications

Codebase 
- Use Version Control

Dependencies
- Explicitly declare all dependencies. Example - POM

Configuration 
- externalize all such configurations that vary between deployments. 

Logs
- logs are nothing but a time-ordered stream of events

Backing Service
- Backing services are services that the application depends on for operation. Ex - database or a message broker. 
- Treat all such backing services as attached resources. means - it shouldn't require any code change to swap a compatible backing service. The only change should be in configurations.

Processes
-  expected to run in an execution environment as stateless processes
-  They may generate persistent data which is required to be stored in one or more stateful backing services.

Build, Release and Run
- Separates the process of converting codebase into a running application as three distinct stages

Port Binding 
- Tradition java app is developed as WAR (Collection of servlets with dependencies)
- A twelve-factor app, on the contrary, expects no such runtime dependency. It's completely self-contained and only requires an execution runtime like Java.
- Spring Boot - default embedded application server

Dev/Prod Parity
- keeping the gap between development and production environment as minimal as possible

Concurrancy 
- The twelve-factor methodology suggests apps to rely on processes for scaling. What this effectively means is that applications should be designed to distribute workload across multiple processes. Individual processes are, however, free to leverage a concurrency model like Thread internally.

Disposability
- Application processes can be shut down on purpose or through an unexpected event. In either case, a twelve-factor app is supposed to handle it gracefully. In other words, an application process should be completely disposable without any unwanted side-effects. Moreover, processes should start quickly
- For instance, in our application, one of the endpoints is to create a new database record for a movie. Now, an application handling such a request may crash unexpectedly. This should, however, not impact the state of the application. When a client sends the same request again, it shouldn't result in duplicate records.



Admin Process
- Often we need to perform some one-off tasks or routine procedure with our application state. For instance, fixing bad records. Now, there are various ways in which we can achieve this. Since we may not often require it, we can write a small script to run it separately from another environment.
Now, the twelve-factor methodology strongly suggests keeping such admin scripts together with the application codebase. 
 
     
### SOLID
Single Responsibility
- A class should only have one responsibility. Furthermore, it should only have one reason to change.

Open/Closed
- classes should be open for extension, but closed for modification. In doing so, we stop ourselves from modifying existing code and causing potential new bugs

Liskov Substitution
-  if class A is a subtype of class B, then we should be able to replace B with A without disrupting the behavior of our program.

Interface Segregation
- larger interfaces should be split into smaller ones. By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.

Dependency Inversion
- Decoupling of software modules. This way, instead of high-level modules depending on low-level modules, both will depend on abstractions.
- Example :- Violation - Car implements - Volkswagen (Implements turnOnEngine) & Tesla (Don't have an engine)

### YAGNI
- You Aren’t Gonna Need It
- Sometimes, as developers, we try to think way ahead, into the future of the project, coding some extra features “just in case we need them” or thinking“we will eventually need them”. WRONG - YAGNI 

### KISS
- Keep it simple stupid
- Simpler the code is, simple to maintain & understand 

### DRY
- Do not Repeat Yourself
- Similar code in different part of system

### Conway’s law
- “Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization’s communication structure.” – Mel Conway

### Domain Driven Design
### Event Driven Design

### Which design patterns have you used in project ?
- We follow 12-Factor app
- Event driven ?
- Domain design 




