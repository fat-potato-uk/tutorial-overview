## Java Spring Boot 101

So, before we start, why do why we Java? Surely a language that has been around
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
 
*Java 12*

http://jdk.java.net/12/ (GENERAL RELEASE!)

Save to a location where you want to store Java and you will link to it later

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

### The tutorials

In order to familiarise yourself with Spring Boot and new Java features, there are various tutorials
available at https://github.com/fat-potato-uk. These are meant to be completed in an interactive 
classroom/hackathon type setting. Below lists some of the tutorials and what they aim to provide:

* Challenge 1: [An introduction to Spring Boot controllers](https://github.com/fat-potato-uk/rest-demo-1.git)
* Challenge 2: [An introduction to Spring JPA](https://github.com/fat-potato-uk/rest-demo-2a.git)
* Challenge 3: [Providing a REST service over a database](https://github.com/fat-potato-uk/rest-demo-2b.git)
* Challenge 4: [Testing a REST/DB service](https://github.com/fat-potato-uk/rest-demo-2c.git)
* Challenge 5: [JUnit 5 and better testing](https://github.com/fat-potato-uk/rest-demo-2d.git)
* Challenge 6: [Spies and Argument Captors](https://github.com/fat-potato-uk/rest-demo-2e.git)
* Challenge 7: [Metrics](https://github.com/fat-potato-uk/rest-demo-2f.git)
* Challenge 8: [Java streams](https://github.com/fat-potato-uk/streamstutorial.git)
* Challenge 9: [Cucumber and Docker](https://github.com/fat-potato-uk/cuke-docker-demo)
* Challenge 10: [Test containers and Cucumber](https://github.com/fat-potato-uk/cuke-test-containers-demo)

There are also some examples for common patterns that do not have any explicit challenges associated with them but
provide a good starting point for further investigation/devlelopment:

* Tracing: [Open Trace and Jaeger](https://github.com/fat-potato-uk/rest-demo-open-trace)
* Polymorphic Json: [Polymorphic Json and Freemarker](https://github.com/fat-potato-uk/rest-polymorphic-json-and-freemarker)

These ideally should be completed in the order suggested. Each has a README that provides details 
on the challenge and should be preferably read and completed without peeking at the answer (cloning
the repo) first!

For challenges 2->7, each builds upon the last. The best way to complete these is to retain the 
"answer" from the previous challenge on build upon it for the next.

There may be a few principles worth running through beforehand too, the main being IoC. Hopefully
I have covered this by now, otherwise, shout!

Enjoy!


 
