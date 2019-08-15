## Java Spring Boot 101

So, before we start, why do why we Java? Surely a language that has been around
for so long has been superseded by newer and much more cutting edge technologies?

Well, in this developers humble opinion, it still has a prominent place in modern
day software development.

Reasons I include for this point of view are:

* Great support for quick to market heavy business logic applications
* Good support for web-based applications
* Powerful collection manipulation (streams)
* Great testing support (especially with Springboot), including mocks, spys and trivial cucumber 
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
* Collection factory methods
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

### Challenge 1

You’ll build a service that will accept HTTP GET requests at: http://localhost:8080/greeting
and respond with a JSON representation of a greeting:

`{"id":1,"content":"Hello, World!"}`

You can customize the greeting with an optional name parameter in the query string:

http://localhost:8080/greeting?name=User

The name parameter value overrides the default value of "World" and is reflected in the response:

`{"id":1,"content":"Hello, User!"`

To start:

In intelliJ, go `File->New->Project..` and click on the `maven` icon in the left
hand pane. Click next and use `rest_demo_1` as the `artifact` and `groupId`.

You should be presented with a project with the following structure:

```
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       └── java
└── <project_name>.iml
```

As a starting point, replace the `pom.xml` contents with the following:

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>rest_demo_1</groupId>
    <artifactId>rest_demo_1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.6.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.jayway.jsonpath</groupId>
            <artifactId>json-path</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.2</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <properties>
        <java.version>12</java.version>
    </properties>


    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>

```

Don't worry too much for now what each bit is doing, but if you are curious feel free to ask.

Next, we need to create our return data, e.g.

```
{
    "id": 1,
    "content": "Hello, World!"
}
```

We do this by creating a class that mirrors this structure. Right click on the `java`
directory under main and create a new class called `demo.models.Greeting`. This
will present you with an empty class called `Greeting` in a `demo.models` package.

Replace the contents with this:

```
package demo.models;

import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Greeting {

    private long id;
    private String content;

    /* Replaced by Lombok */

    /*
    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }

    public void setId(long id) {
        this.id = id;
    }

    public void setContent(String content) {
        this.content = content;
    }
    */
}
```

You can remove the commented out code, but this serves as an illustration on 
what `Lombok` gives us. Ask more about this and I can go into more detail on 
what it provides.

Next, we need a controller to serve the `GET` request. Going through the same
process again create a new class called `demo.controllers.GreetingController`
and replace the content with:

```
package demo.controllers;


import demo.models.Greeting;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.concurrent.atomic.AtomicLong;

@RestController()
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @RequestMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
}
```

Finally, to run this, we need an entry point. Create a new class called `demo.Application`
with the following:

```
package demo;


import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

To run, click on the `Add Configuration...` drop down in the top right and then using
the `+` icon in the top left create a new `maven` deployment called run using the 
command: `spring-boot:run`.

Now navigate to `http://localhost:8080/greeting` and see the results!

As you can see, under the hood all of the `pojo` -> `Json` marshalling is done for us.
Just by defining an object with the appropriate structure, the standard conventions in
use mean that it will be converted when required into the appropriate (`Json`) type.

##### Challenge 1b

Lets add a test for this controller. In the `java` directory in `test`, create a new class
called `demo.controllers.GreetingControllerTest`. In there, paste the following:

```
package demo.controllers;


import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;

@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class GreetingControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void noParamGreetingShouldReturnDefaultMessage() throws Exception {
        this.mockMvc.perform(get("/greeting"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.content").value("Hello, World!"));
    }

    @Test
    public void paramGreetingShouldReturnTailoredMesage() throws Exception {
        this.mockMvc.perform(get("/greeting").param("name", "Java World"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.content").value("Hello, Java World!"));
    }
}
```

_Note: A downside it seems with the current version(s) of Spring Boot is that it defaults
 to Junit4 by default. This can be changed, but for now we'll go with the 
grain_

Take some time to have a play around with the tests and perhaps write a few of your own.

You can find a complete version of this tutorial at: https://github.com/hojomojo/rest-demo-1.git

### Challenge 2



 