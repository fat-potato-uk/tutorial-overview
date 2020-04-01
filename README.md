## Java Spring Boot 101

So, before we start, why do we Java? Surely a language that has been around
for so long has been superseded by newer and much more cutting edge technologies?

Well, in this developers humble opinion, it still has a prominent place in modern
day software development.

Reasons I include for this point of view are:

* Great support for quick to market heavy business logic applications
* Good support for web-based applications
* Powerful collection manipulation (streams)
* Great testing support (especially with Springboot), including mocks, spys and trivial cucumber (BDD)
  integration.
* Frameworks that help with common patterns/approaches (e.g. database support)

For this 101, we are going to be using Spring Boot. Spring Boot can be seen as an iteration on the
Spring framework of yore. It still uses the Spring framework "underneath the hood", but it provides
a lot default configuration/setup allowing for the developer to get into developing the business 
logic very quickly. You could call it a boot strap of sorts for developing Spring apps.

Some of the benefits of Spring Boot include:

* One of the best ready to use the micro services platform.
* Use of an intelligent and convention over configuration approach that reduces the startup and configuration phase of your project significantly.
* Powerful and flexible configuration management using the application.properties or yml file.
* Spring Boot starters to offer ready-to-use auto-configuration for your application.
* Production ready actuator module.
* It simplifies Spring dependencies by taking the opinionated view.
* Built in web-container/stand alone Jars for web apps.

More generic Spring benefits include:

* IoC
* MVC support
* Spring Data JPA

Anyway, enough of the sales pitch, lets get started:

### Download these
 
*Intellij community edition*

https://www.jetbrains.com/idea/download
 
*Lombok Plugin*

https://plugins.jetbrains.com/plugin/6317-lombok-plugin (This can be acquired from the plugins
menu in intelliJ itself)
 
*Java 13*

http://jdk.java.net/13/ (GENERAL RELEASE!)

Save to a location where you want to store Java and you will link to it later

*Alternative IDE Option: Visual Studio Code*

If you wish to use VS Code instead of IntelliJ, there is a brief guide [here](https://github.com/fat-potato-uk/vscode-setup) on how to set it up. There are also some additional notes on how the challenges may differ subtly using this IDE.

#### Whats been going on then?

So, many people have used Java before, but often not for many years. So, whats it been up to?

_Java 6_
* Support for pluggable annotations

_Java 7_
* Strings in switch
* Automatic resource management in try-statement
* Improved type inference for generic instance creation, aka the diamond operator <>
* Allowing underscores in numeric literals
* Catching multiple exception types and rethrowing exceptions with improved type checking

_Java 8_
* Lamda Expressions
* Using Lamda Expression to sort a collection
* Functional Interfaces (java.util.function)
* Stream Collection Types (java.util.stream)
* Method References
* Optional<T>

_Java 9_
* JShell
* Modules
* Collection factory methods (`List.of()`)
* Private interface methods

_Java 10_
* Local-Variable Type Inference
* _copyof()_ in popular collections
* _Optional*.orElseThrow()_
* Container Awareness

_Java 11_
* API improvements (String, File, Optional)
* Single file source/script-able java

_Java 12_
* Switch statement changes (preview)
* API improvements (Collector, String)

_Java 13_
* Switch statement changes (preview)
* Text blocks (preview)

### The tutorials

In order to familiarise yourself with Spring Boot and new Java features, there are various tutorials
available at https://github.com/fat-potato-uk. These are meant to be completed in an interactive 
classroom/hackathon type setting. Below lists some of the tutorials and what they aim to provide:

* Challenge 1: [An introduction to Spring Boot controllers](https://github.com/fat-potato-uk/rest-demo-1.git)
    * Create your first MVC/RESTful service
    * Intro to `Lombok`
    * `MockMvc` and testing controllers
* Challenge 2: [An introduction to Spring JPA](https://github.com/fat-potato-uk/rest-demo-2a.git)
    * Spring JPA
    * IoC
    * Spring Beans
* Challenge 3: [Providing a REST service over a database](https://github.com/fat-potato-uk/rest-demo-2b.git)
    * Multi-endpoint controllers
    * Optionals
    * Controller advice
    * Custom exceptions
* Challenge 4: [Testing a REST/DB service](https://github.com/fat-potato-uk/rest-demo-2c.git)
    * End-2-end testing with `MockMvc` and `jsonPath`
* Challenge 5: [JUnit 5 and better testing](https://github.com/fat-potato-uk/rest-demo-2d.git)
    * Intro to `JUnit 5`
    * Mocks
    * Improving test scope
* Challenge 6: [Spies and Argument Captors](https://github.com/fat-potato-uk/rest-demo-2e.git)
    * Spies
    * Argument Captors
* Challenge 7: [Metrics](https://github.com/fat-potato-uk/rest-demo-2f.git)
    * `Spring Actuator` and metrics
    * `Prometheus` endpoints
    * `@DirtiesContex` dangers and trickier tests
* Challenge 8: [Java streams](https://github.com/fat-potato-uk/streamstutorial.git)
    * Optionals
    * Streams
* Challenge 9: [Cucumber and Docker](https://github.com/fat-potato-uk/cuke-docker-demo)
    * Cucumber and Java
    * How to Dockerfile with Maven
    * Integration testing approach
* Challenge 10: [Test containers and Cucumber](https://github.com/fat-potato-uk/cuke-test-containers-demo)
    * Test containers
    * System testing approach
* Challenge 11: [Documentation with Swagger](https://github.com/fat-potato-uk/rest-demo-3-swagger)
    * Documenting Restful APIs with Swagger
    * Testing through the Swagger interface

There are also some examples for common patterns that do not have any explicit challenges associated with them but
provide a good starting point for further investigation/devlelopment:

* Tracing: [Open Trace and Jaeger](https://github.com/fat-potato-uk/rest-demo-open-trace)
* Polymorphic Json: [Polymorphic Json and Freemarker](https://github.com/fat-potato-uk/rest-polymorphic-json-and-freemarker)
* Grpc: [Grpc](https://github.com/fat-potato-uk/grpc) and [Streaming Grpc](https://github.com/fat-potato-uk/grpc-streaming)

These ideally should be completed in the order suggested. Each has a README that provides details 
on the challenge and should be preferably read and completed without peeking at the answer (cloning
the repo) first!

For challenges 2->7, each builds upon the last. The best way to complete these is to retain the 
"answer" from the previous challenge on build upon it for the next.

There may be a few principles worth running through beforehand too, the main being IoC. Hopefully
I have covered this by now, otherwise, shout!

Enjoy!

#### The ULTIMATE challenge

If you find yourself at a loose end and have completed all the exercises, you can try constructing an example
prescription service! This will be a RESTFul application that serves tailored prescriptions for each patient.

You will need:

* An endpoint for a doctor to submit a prescription with an authorisation token in the `@RequestHeader`
* An endpoint for a nurse that can make alterations to the dosage (!)
* A endpoint for a patient to receive the prescription (with the name of the authorising doctor, medication and boiler
plate safety information)
* A suite of cucumber tests that verify various interactions
* A persisted store to an external database housing the information
* A trace span that tags the authorising medical professional that created the prescription
* A Dockerfile to deliver the product
* A cucumber "smoke test" to verify that the e2e system works as intended!
 
