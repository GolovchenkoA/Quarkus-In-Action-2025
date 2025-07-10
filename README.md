# quarkus


## Links:
- https://quarkus.io/
- https://quarkus.io/guides/
- https://code.quarkus.io/
- https://github.com/quarkusio
- https://github.com/quarkiverse
- https://quarkusio.zulipchat.com/
- https://groups.google.com/g/quarkus-dev?pli=1
  

- Book Quarkus in Action 2025 https://learning.oreilly.com/library/view/quarkus-in-action/9781633438958/
- Book Quarkus in Action Video Edition 2025 https://learning.oreilly.com/videos/quarkus-in-action/9781633438958VE/
- How to generate a quarkus application https://github.com/agoncal/agoncal-course-quarkus-starting/blob/master/bootstrap.sh



## Quarkus in Action 2025 links
- Code https://github.com/xstefank/quarkus-in-action
- Quick Starts repositories https://github.com/quarkusio/quarkus-quickstarts
- Quarkus Security https://quarkus.io/guides/security-overview
- MicroProfile https://microprofile.io/
- [Reactive System Architecture](https://medium.com/big-data-cloud-computing-and-distributed-systems/reactive-architecture-i-5652f944f8fb)
- Migration Toolkit for Applications 7.3 https://docs.redhat.com/en/documentation/migration_toolkit_for_applications/7.3
- Micronaut and Helidon (helidon.io)
- HTTPIe https://httpie.io/download
- Quarkiverse. Quarkus user community extensions https://hub.quarkiverse.io/
- Quarkus all configs https://quarkus.io/guides/all-config
- Optimize a Native Executable with Profile-Guided Optimization https://www.graalvm.org/latest/reference-manual/native-image/guides/optimize-native-executable-with-pgo/
- 3 types of docker images: JVM, Native and Native Micro: https://github.com/xstefank/quarkus-in-action/tree/main/chapter-02/2_1_1/quarkus-in-action/src/main/docker


### How to update Quarkus version
supports LTS https://github.com/quarkusio/quarkus/releases)
- Maven ./mvn quarkus:update
- Gradle ./gradlew quarkusUpdate
- CLI quarkus update

### Quarkus provides built-in support for generating Dockerfiles (and Kubernetes resources) using its container image extensions, particularly:
quarkus-container-image-docker

quarkus-container-image-jib

quarkus-container-image-buildpack

You can configure Quarkus to automatically generate Dockerfiles when you build your application

```bash
quarkus extension add quarkus-container-image-docker
```

### Wways to generate a Quarkus application:

1. Using the Quarkus CLI
quarkus create app com.example:my-app

2. Using the Quarkus Web Code Generator
https://code.quarkus.io

3. Using the Maven Plugin
Add -DbuildTool=gradle system propery if a project should be generated with Gradle
```bash
mvn io.quarkus:quarkus-maven-plugin:<version>:create
```


### 🚀 Running the Application in Dev Mode

Quarkus supports live coding with dev mode. Use the following command based on your build tool:

- **Maven**  
  ```bash
  ./mvnw quarkus:dev
  ```
- **Gradle**  
  ```bash
  ./gradlew quarkusDev
  ```
- **Quarkus CLI**  
  ```bash
  quarkus dev
  ```


 ### Build Commands
 Quarkus uses GraalVM and that means an image should be generated for every platform our application will be run on.
Use docker or podman (Linux-native only) to cross-compile native images using containers.

For example, here's how you would build 2 platforms for each of the 3 environments (6 total images):

 ```bash
# Enable container build and specify target platform
# Dev build (x86_64)
./mvnw package -Dquarkus.profile=dev \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.builder-image=quay.io/quarkus/ubi-quarkus-native-image:latest \
  -Dquarkus.native.additional-build-args="--target=linux-amd64"

# Dev build (arm64)
./mvnw package -Dquarkus.profile=dev \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.additional-build-args="--target=windows-amd64"

# Staging build (x86_64)
./mvnw package -Dquarkus.profile=staging \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.additional-build-args="--target=linux-amd64"

# Staging build (arm64)
./mvnw package -Dquarkus.profile=staging \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.additional-build-args="--target=windows-amd64"

# Prod build (x86_64)
./mvnw package -Dquarkus.profile=prod \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.additional-build-args="--target=linux-amd64"

# Prod build (arm64)
./mvnw package -Dquarkus.profile=prod \
  -Dquarkus.native.container-build=true \
  -Dquarkus.native.additional-build-args="--target=windows-amd64"
Each command produces a native binary like:
 ```


 ```bash
target/*-runner
 ```

### GraalVM Distributions
| Distribution   | Focus                         | Usage                                 |
|----------------|-------------------------------|---------------------------------------|
| GraalVM CE     | Full polyglot VM + native image | General purpose, research, polyglot apps |
| GraalVM EE     | Enterprise with optimizations  | High-performance, commercial support  |
| Mandrel        | Native image for Quarkus       | Stable native builds, Red Hat supported |


### Native images generation
Quarkus provides out-of-the-box support for generating native images on Linux using its container-based build mode, which means you do not need to have GraalVM installed locally. Quarkus leverages official GraalVM container images to build native executables seamlessly.

However, when targeting Windows native images, Quarkus requires a local GraalVM installation on a Windows machine because container-based builds only support Linux platforms. This means you need to install and configure GraalVM on your Windows system to generate native Windows executables.


### 🧊 Building a Native Image

Quarkus supports native image generation out of the box using GraalVM (or containerized builds). Use one of the following commands based on your build tool:

- **Maven**
```bash
  ./mvnw package -Pnative
```

- **Gradle**
```bash
./gradlew build -Dquarkus.package.type=native
```
- **CLI**
```bash
quarkus build --native
```


### How to list installed extensions
List extension for quarkus app if run from the app's directory or list all available quarkus extensions if run from any other directory
```bash
quarkus extension list
quarkus ext list
quarkus extension list --full
quarkus extension --installable
quarkus extension categories
```

## Chatper 3. Enchansing developer productivity with Quarkus

### Quarkus Dev Services 
[Dev Services Docs](https://quarkus.io/guides/dev-services)
[Dev Services For Databases Docs](https://quarkus.io/guides/databases-dev-services) 
[Dev Services for Databases Zero Config](https://quarkus.io/guides/datasource)
is a feature that automatically provisions and configures required services (like databases, Kafka, Redis, etc.) during development and testing—without needing you to manually start them.
It’s designed to improve developer productivity by reducing setup time.

### Live reload
search quarkus.live-reload on https://quarkus.io/guides/all-config
Pay attention to [the #quarkus-core_quarkus-live-reload-instrumentation](https://quarkus.io/guides/all-config#quarkus-core_quarkus-live-reload-instrumentation)

### MicroProfile Config support
https://microprofile.io/specifications/microprofile-config/

### Property priorities
https://quarkus.io/guides/config-reference#:~:text=The%20loading%20starts%20from%20the%20config%20folder%20and,loading%20order%29.%20This%20is%20a%20user-defined%20configuration%20property.

### Quarkus Dev UI
https://quarkus.io/guides/dev-ui
Quarkus Dev UI is a developer-friendly user interface that comes to life when you run your application in development mode (./mvnw quarkus:dev). It serves as a powerful portal for exploring, debugging, and interacting with your application - all while it’s running - with zero code changes or restarts.

### Dev Services
https://quarkus.io/guides/dev-services

### Keycloak and OpneID integration 
https://quarkus.io/guides/security-keycloak-authorization#:~:text=The%20Keycloak%20Authorization%20extension%2C%20quarkus-keycloak-authorization%2C%20extends%20the%20OpenID,enforcer%20that%20dynamically%20manages%20access%20to%20secured%20resources.


### Continuous testing
https://quarkus.io/guides/continuous-testing
If you want continuous testing to start automatically you can set quarkus.test.continuous-testing=enabled in application.properties. If you don’t want it at all you can change this to disabled.


## Chapter 4

### Quarkus CLI app creating
```
quarkus create app com.example:openapi-app  --extensions=quarkus-smallrye-openapi

# We don't need to provide the full name of the extension (in this case quarkus-rest-jackson), it's long enough for Quarkus to understand which extention should be used
quarkus create app com.example:openapi-app -P 3.15.1 \
  --extensions="quarkus-smallrye-openapi, quarkus-rest"

#  use quarkus-rest-client-jackson if you need to call downstream services
quarkus create app com.example:openapi-app \
  --extensions quarkus-smallrye-openapi, quarkus-rest-jackson, quarkus-rest-client-jackson \
  --no-code
```


### GraphQL Smallrye
Code First approach. QraphQL schema is generated from Java code
https://quarkus.io/guides/smallrye-graphql


### Dynamic GraphQL Client
The Quarkus Dynamic GraphQL Client is a runtime-based, flexible client for making GraphQL requests without needing to generate or predefine Java classes or interfaces.

🧠 In short: You build and send GraphQL queries dynamically using a fluent Java API — no code generation, no strongly typed stubs.

✅ When to Use It
Use the dynamic client when:

You want to build GraphQL queries at runtime (e.g., based on user input or conditions)

The GraphQL schema is too large or changes frequently

You don't want to generate Java models for all types

You need to interact with remote GraphQL APIs flexibly

### gRPC Support
```
quarkus extension add grpc
```

### gRPC CURL
https://github.com/fullstorydev/grpcurl

### Smallrye Mutiny
https://smallrye.io/smallrye-mutiny/latest/
Intuitive Event-Driven Reactive Programming Library. Is a replacement for StreamObserver that's used by protoc by default.

### Developing Quarkus CLI applications
Simple example: https://quarkus.io/guides/command-mode-reference
PicoCLI (advanced ???) https://quarkus.io/guides/picocli


## Chapter 5 Testing

Quarkus supports testing in both JVM mode and native mode, and encourage you to test in both — especially if you're building native executables with GraalVM.
Tests annotated with @QuarkusIntegrationTest are disabled by default in JVM mode. They are only executed when running tests in native or container mode, such as:

```
./mvnw verify -Dnative
./mvnw verify -Dquarkus.package.type=fast-jar -Dquarkus.test.integration-test=true

```

### @DisableOnIntegrationTest
The annotation @DisableOnIntegrationTest is a Quarkus testing utility annotation that allows you to skip specific tests when running in integration test mode (i.e., tests annotated with @QuarkusIntegrationTest or @NativeImageTest).
Example:
```
@DisabledOnIntegrationTest(forArtifactTypes = {"native"})
```

✅ Use Cases:
- A test only makes sense in JVM mode
- A test uses mocking, in-memory DB, or features not supported in native mode
- You're writing unit or fast tests that shouldn’t run during full integration testing

### JVM tests vs Native tests
- **./mvnw test** Runs tests in JVM mode Does not execute @QuarkusIntegrationTest or @NativeImageTest
- **./mvnw verify** -Pnative Runs the full Maven lifecycle, including compile, test, package, and verify, Builds a native executable using GraalVM, Executes tests annotated with @QuarkusIntegrationTest and/or @NativeImageTest


### Mocks
There are 2 approaches described in this book:
1. Mocking with CDI beans

When you use @io.quarkus.test.Mock it applies @Alternative and @Priority(1) annotations to a mock bean 
```
import io.quarkus.test.Mock


@Mock
public class MockRestApiClient implements RestApiClient {

    @Override
    public List<Car> allCars() {
        Car peugeot = new Car(1L, "ABC123", "Peugeot", "406");
        return List.of(peugeot);
    }
}
```
2. Mockito Framework.
Mocking with Mockito, as opposed to using CDI alternatives, is not limited to using only CDI beans. 
Any object can be replaced with a mock. When used with CDI, the bean has to be of a normal scope, 
which means @Singleton and @Dependent beans can't be mocked out (because Mockito needs to use proxies for such beans,
and these to scopes a non-proxyable). All other built-in CDI scopes will work.


!!! In most cases the recommended pattern is to use @QuarkusTest for test in JVM mode and @QuarkusIntegrationTest for tests in native mode, where the integration test case can inherit the test case and can disable some tests it they are not compatible with native mode by using @DisabledOnIntegrationTest(forArtifactTypes = {"native"})


### QuarkusMock.installMockForType()
QuarkusMock.installMockForType() is a test-time utility method provided by Quarkus to dynamically replace a CDI bean with a mock programmatically, instead of using the @Mock annotation.
see example: https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-05/5_3_2/reservation-service/src/test/java/org/acme/reservation/ReservationResourceTest.java#L64


### QuarkusTestResourceLifecycleManager 
Responsible for controlling the lifecycle of external resources during Quarkus tests.

It’s most commonly used to:
- Start and stop Docker containers (via Testcontainers)
- Launch embedded services (like Kafka, Redis, databases)
- Set system properties or configuration values used by the app
- Perform setup/teardown before and after tests

```
@QuarkusTest
@QuarkusTestResource(PostgresTestResource.class)
public class MyDatabaseTest {
    // Will run with a real Postgres container
}

public class PostgresTestResource implements QuarkusTestResourceLifecycleManager {

    private PostgreSQLContainer<?> postgres;

    @Override
    public Map<String, String> start() {
        postgres = new PostgreSQLContainer<>("postgres:15")
                .withDatabaseName("testdb")
                .withUsername("test")
                .withPassword("test");
        postgres.start();

        // Return properties to override application config
        return Map.of(
            "quarkus.datasource.jdbc.url", postgres.getJdbcUrl(),
            "quarkus.datasource.username", postgres.getUsername(),
            "quarkus.datasource.password", postgres.getPassword()
        );
    }

    @Override
    public void stop() {
        if (postgres != null) {
            postgres.stop();
        }
    }
}

```

### Test Profiles and tags
Use quarkus.test.profile.tags parameter to run specific tests (tests should have tags in this case)
@QuarkusTestProfile is a powerful Quarkus testing feature that allows you to create custom test configurations — essentially, test profiles — to control how your Quarkus application behaves during testing.

```
public class StaggingProfile implements QuarkusTestProfile {
    @Override
    public Map<String, String> getConfigOverrides() {
        return Map.of(
            "path.to.service", "http://stagging.my.service.com/"
        );
    }

    @Override
    public String getConfigProfile() {
        return "stagging";
    }
}

----------------------
@QuarkusTest
@TestProfile(StaggingProfile.class)
public class MyServiceStaggingTest {

    @Test
    void testWithStaggingService() {
        // Will run with  "path.to.service", "http://stagging.my.service.com/"
    }
}
```

### Mocking. Important!!!!
- Native mode isn't supported for tests that use mocks or CDI injections into the test itself because the application under test runs in a different OS process that the testing logic.
- Mocking is achieved either by replacing a CDI bean with an alternative implementation or by describing the mock's behavior using Mockito DSL
- Testing Profiles ogranize test into groups that run with a separate application instance and might with a different configuration
- Dev Servies manages databases, messages, etc instances when we run the application in Dev mode.


## Chapter 6. Exposing and Security Web Applications

In this chapter they use:
1. HTML\AJAX
2. Qute is the server-side templating engine used in Quarkus. It's designed to be:
- Fast (both at runtime and compile time)
- Type-safe
- Lightweight and GraalVM native-image friendly
- Inspired by popular engines like Mustache and Thymeleaf, but more Quarkus-optimized


Quarkus CLI app generation:
```
quarkus create app org.acme:users-service -P 3.15.1 \
--extension qute,rest-qute,oidc,rest-client-jackson, \
quarkus-rest-client-oidc-token-propagation --no-code
```

### Docker Compose example
https://github.com/xstefank/quarkus-in-action/tree/0a7e10d43fd36a2f29104900418b91941b814233/chapter-06/production

### Qute Checked Templates
Different approach with type-save templates by using @CheckedTemplate annotation. The annotation is applied to static classes


### Security Doc
https://quarkus.io/guides/security-overview


## Chapter 7 DB Access
Panache https://quarkus.io/guides/hibernate-orm-panache 
Extension implements Active Record pattern and Repository pattern.
Active record pattern allows to call DB actions directly from Entity class using static methods. Example:
```
User.findById(user.id)
```

### DB Zero-config in DEV mode
[Zero-config setup in development mode](https://quarkus.io/guides/datasource#dev-services)

### Fixed DB port for DEV mode
https://quarkus.io/guides/datasource#quarkus-datasource_quarkus-datasource-devservices-port

### Persistence Test example
https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-07/7_4/reservation-service/src/test/java/org/acme/reservation/ReservationPersistenceTest.java#L13

### Panache supports sql scripts for DB initialization
import.sql can be created in `src/main/resources/`. This feature is disabled for PROD by default.  See https://quarkus.io/guides/hibernate-orm-panache

### GraphQL @Transacrional annotation
The annotation should be used when we make calls to a DB. [GraphQLInventoryService](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-07/7_2_2/inventory-service/src/main/java/org/acme/inventory/service/GraphQLInventoryService.java) and [GrpcInventoryService](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-07/7_2_2/inventory-service/src/main/java/org/acme/inventory/grpc/GrpcInventoryService.java)
`GrpcInventoryService add()` method could have @Transactiona annotation as well instead of `QuarkusTransaction.requiringNew().run(..)`, but in this way the whol method call would be executed as a single transactio. We know that a single gRPC connection might take a lot of time at it can lead to different problems.

### REST Data support
https://quarkus.io/guides/rest-data-panache
Panache adds transactions out of the box
If you have Swagger dependency you will see new endpoints once a REST Data repository is created.

`quarkus-hibernate-orm-rest-data-panache` - JDBC with Hibernate ORM
`quarkus-monodb-rest-data-panache` - MongoDB with Hibernate ORM
`qurkus-hibernate-reactive-rest-data-panache` - reactive database driver with Hibernate Reactive

Adding REST Data extensions
```
quarkus ext add quarkus-hibernate-orm-rest-data-panache qurkust-jdbc-postgresql quarkus-rest-jackson
```

### Transactions
https://quarkus.io/guides/transaction
Quarkus does not support distributed transactions. See additional information following the link above.
There are different approaches:
- Declarative approach
- Programmatic approach (more user-friendly). You can use static methods on QuarkusTransaction to define transaction boundaries. This provides two different options, a functional approach that allows you to run a lambda within the scope of a transaction, or by using explicit begin, commit and rollback methods.
- Legacy API approach


### Quarkus and MongoDB
https://quarkus.io/guides/mongodb-panache
`mongosh` is a Node.js-based shell that lets you connect to MongoDB, run queries, execute admin operations, and explore documents, all from the command line.

### MongoDB Numeric ID Support
In java application the default ObjectId can be both: ObjectId or String
| Aspect               | Default (`ObjectId`)   | Custom Numeric ID                 |
| -------------------- | ---------------------- | --------------------------------- |
| Generated by MongoDB | ✅ Yes                  | ❌ No (you must assign it)         |
| Sortable by time     | ✅ Yes                  | ⚠️ Only if you design it that way |
| Guaranteed unique    | ✅ Yes                  | ✅ Yes (if you manage it)          |
| Type safety in code  | May require conversion | Often easier in typed languages   |


### Reactive Data access
Required changes:
```
quarkus-hibernate-orm-panache -> quarkus-hibernate-reactive-panache
quarkus-jdbc-postgresql -> quarkus-jdbc-reactive-pg-client
quarkus-hibernate-orm-rest-data-panache -> quarkus-hibernate-reactive-rest-data-panache
xxx -> quarkus-test-hibernate-reactive-panache
```

### Reactive DB Testing
Requires quarkus-test-hibernate-reactive-panache.
See also:
- https://quarkus.io/guides/hibernate-reactive-panache
- https://quarkus.io/guides/hibernate-reactive#testing


### Reactive Programming
Reactive programming is harder then Imperative programming. However, the performance of the reactive programming (eventloops) outperforms imperative programming in systems with high level of concurrency and I/O operations.

Quarkus uses [SmallRye Mutiny](https://smallrye.io/smallrye-mutiny/latest/) as its reactive API. Quarkus also supports Kotlin Corutines, but it's out of the scope of this book.
[Reactive Streams specification](https://www.reactive-streams.org/) directly integrated with `java.util.concurrent.Flow` class

Quarkus can detect and throw an exception (or log a warning) when you perform blocking operations (like JDBC, file IO, or thread sleep) on the event loop — especially in dev and test modes.
Quarkus provides  `@Blocking` and `@NonBlocking` annotation that can be used in your reactive application

There are 2 programming styles: Imperative and Declarative. See [From sequential to continuation style](https://quarkus.io/guides/getting-started-reactive#from-sequential-to-continuation-style)

[public Multi<CarResponse> add(Multi<InsertCarRequest> requests)](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-07/7_4/inventory-service/src/main/java/org/acme/inventory/grpc/GrpcInventoryService.java#L27) you can fine how to use both @Blocking and non-blocking (QuarkusTransaction.requiringNew().run(..)) calls. !!!! Pay attantion it was for demo purposes only, because in a real world application you would use reactive DB programming to save all the entities in the DB.


## Chapter 8 Virtual Threads (Project Loom)
Reactive programming is harder then imperative programming. ⚠️ However, the performance of the reactive programming (eventloops) is much better then imperative programming in systems with high level of concurrency and I/O operations!!!!. Project Loom allows to write code in imperative style and have reactive application at the same time. Apart of that the project aims to enhance Java’s concurrency model by introducing fibers, which are lightweight threads managed by the JVM. Apart of that Virtual threads have its problems (see the description below). So it's always good to understnad how every technology works behind the scene before use it. ⚠️ Because Quarkus allows you to switch between virtual threads and reactive flawlessly, you can always start with virtual threads and move to reactive programming if you need it

**When to use Virtual threads**
|Task Type  |	Thread Type  |
| -------------------- | ----------------------|
|I/O-bound  |	✅ Virtual threads  |
|CPU-bound  |	✅ Platform threads, ForkJoinPool, or ExecutorService with bounded pools|  

❌ Overusing Virtual Threads for Computation
⚠️ Using too many virtual threads for CPU-bound (compute-heavy) tasks can degrade performance.

Why?
🧵 Virtual threads still need CPU
Even though they’re lightweight, virtual threads compete for CPU just like regular threads when doing CPU work.

⚖️ CPU saturation
On a machine with N cores, only N threads can compute in parallel. If you launch 10,000 compute-bound virtual threads, they’ll thrash the CPU, and the OS/Java scheduler will suffer.

🧭 No preemption
Virtual threads aren’t preemptively scheduled. If one runs a tight compute loop:

Code example. it can starve others — because the JVM relies on cooperative scheduling for virtual threads.
```
while (true) { /* burn CPU */ }
```

😬 Latency impact
Overloading with CPU-bound tasks can lead to higher latency, scheduling contention, and even heap pressure due to retained call stacks.



### Quarkus Virtual Threads
Quarkus supports [Virtual Threads](https://quarkus.io/guides/virtual-threads) and provides `@RunOnVirtualThread` annotation.

## Project Loom
Project Loom has known problems, for example, with [Pinning Virtual Threads](https://medium.com/@rakeshkpandit/resolving-virtual-thread-pinning-issues-in-java-442d0b55b603) and [Vitrual thread monopolizing](https://todd.ginsberg.com/post/java/virtual-thread-pinning/)


## Chapter 9 Messaging
Quarkus follows [MicroProfile messaging specification](https://microprofile.io/specifications/reactive-messaging/) and relies on [SmallRye Reactive Messaging library](https://smallrye.io/smallrye-reactive-messaging/smallrye-reactive-messaging/3.4/index.html) which implements the specification

The MicroProfile messaging specification allows only `@ApplicationSocped` and `@Dependent` CDI scopes for CDI beans to be used in reactive messaging.
The API conceptually consists of two main annotations: `@Outgoing` and `@Incoming`, which are used to either produce or consume messages.

Examples:

Producer:
```
@ApplicationScoped
public class NumberProducer {

    @Outgoing("ticks-out")
    public Multi<Long> produceTicks() {
        return Multi.createFrom()
                    .ticks()
                    .every(Duration.ofSeconds(1))
                    .select()
                    .first(5)
                    .onItem().transform(tick -> System.currentTimeMillis()); // emit current time
    }
}
```

Processor:
```
@ApplicationScoped
public class NumberProcessor {

    @Incoming("ticks-out")
    @Outgoing("processed-ticks")
    public Multi<String> process(Multi<Long> ticks) {
        return ticks.map(Instant::now::toString)
    }
}
```

Consumer:
```
@ApplicationScoped
public class NumberLogger {

    @Incoming("processed-ticks")
    public void consume(String message) {
        System.out.println("[Received] " + message);
    }
}
```



[Reactive System Architecture](https://medium.com/big-data-cloud-computing-and-distributed-systems/reactive-architecture-i-5652f944f8fb)
MicroProfile Reactive Messaging is a specification within the [Eclipse MicroProfile project](https://microprofile.io/) designed to enable reactive stream-based communication between microservices and messaging systems like Kafka, AMQP, MQTT, etc.

Service Provider Interface (SPI) in MicroProfile Reactive Messaging absolutely allows you to plug in external services — that's one of its core purposes.

✅ SPI: Gateway to External Integration
The SPI lets you create custom connectors that can:
- Consume data from external services (e.g., REST APIs, WebSockets, gRPC, Redis)
- Publish data to external services
- Be plugged into MicroProfile Reactive Messaging pipelines just like Kafka or MQTT

🔌 Real Use Cases
| External Service|	What You Can Do With SPI|
| -------------------- | ----------------------|
| REST/HTTP APIs  |	Pull or push data periodically or on-demand|
| Redis  |	Subscribe to pub/sub channels or streams|
| WebSocket  |	Stream messages to/from a WebSocket server|
| gRPC  |	Pipe reactive calls into channels|
| Custom TCP socket  |	Bridge low-level networking into reactive channels|
| Legacy JMS system  |	Wrap and adapt into a reactive model|


### Acknowledgment strategies
In Quarkus Reactive Messaging, when consuming messages, you can control what happens after processing a message using acknowledgment strategies. There are two main strategies for handling positive (ack) and negative (nack) acknowledgment:

| Strategy            | How It Works                                                   | When to Use                    |
| ------------------- | -------------------------------------------------------------- | ------------------------------ |
| **Manual ack/nack** | Use `Message<T>` and call `msg.ack()` or `msg.nack(Throwable)` | For async or error-prone flows |
| **Automatic ack**   | Quarkus handles ack/nack based on method completion/exception  | For simple processing          |


### Acknowledgment Strategies
Quarkus Reactive Messaging, the annotation @Acknowledgment allows you to control how and when message acknowledgments happen — especially useful when consuming messages from a broker like [Kafka](https://smallrye.io/smallrye-reactive-messaging/latest/kafka/receiving-kafka-records/#acknowledgement), MQTT, etc.

✅ `@Acknowledgment(Acknowledgment.Strategy.XXX)` Summary Table
| Strategy          | Ack Timing                    | Throws Exception →   | Use Case                             |
| ----------------- | ----------------------------- | -------------------- | ------------------------------------ |
| `NONE`            | Never (you must ack manually) | ❌ No auto-nack       | Full control, advanced error flows   |
| `PRE_PROCESSING`  | Before method runs            | ✅ Already acked      | Fire-and-forget, no rollback needed  |
| `POST_PROCESSING` (default strategy) | After method completes        | ❌ Auto-nack on error | Safe default, balanced strategy      |
| `MANUAL`          | You call `ack()`/`nack()`     | ✅ You decide         | Same as `NONE`, but explicitly named |


### Imperative declaration (CDI injection)
You might not always be able to move to completely reactive code in all deployed system services. For this reason, MicroProfile Reactive Messaging provides a simple API to bridge the imperative and reactive worlds with the @Channel annotation. The @Channel annotation has two use cases: either to produce messages from imperative code or consume a channel into an instance of Publisher through a CDI injection.
The second use case of @Channel is particularly useful for applications working with server-sent events (SSEs), which push the events from server to clients through an HTTP connection. We can use the @Channel annotation to inject instances of Reactive Streams (or Flow) Publisher or its subclasses as in our case the Mutiny’s Multi


### Dependency conflicts
 If you run into import conflicts, always use classes from the `org.eclipse.microprofile.reactive.messaging` package.

### Connectors
[Quarkus Messaging Extensions](https://quarkus.io/guides/messaging)

```
mp.messaging.incoming.{channel-name}.{attribute-name}=attribute-value
mp.messaging.outgoing.{channel-name}.{attribute-name}=attribute-value
mp.messaging.connector.{connector-name}.{attribute-name}=attribute-value
```

⚠️ The configuration of channels (channel-name) overrides the global configuration of connectors (connector-name). It is important to point out that all configuration for channels is specific to either the incoming or the outgoing direction. This means that if we use the same channel (channel-name) for both producing and consuming of messages (i.e., reactive streams’ processor), we need to configure each direction separately, even if they use the same connector.




## Chapter 10 Cloud-native application patterns
Health, Tracing, Metrics, and Fault Tolerance are part of [MicroProfile Specifications](https://microprofile.io/specifications/). Service Discovery is not part of it at the time of writing but may well be in the future.
⚠️ Health, metrics, and tracing (and also logging) are very often together called observability.
 
- Health—Applications should expose information about their health so that various kinds of their problems can be detected (either by a human operator or automatically). An application is unhealthy if some of its components or external connections don’t work as needed—for example, if a database connection isn’t working, a deadlock is detected, or the memory heap is full. Human operators or automated tools can then respond to this information and take appropriate action, such as restarting the application.
- Metrics—Metrics are similar to health checks in that they convey information about the status of an application. However, unlike health checks whose outcome is binary (good or bad), metrics are numeric values. They can tell how much memory is used, how many threads in a thread pool are usually busy, how many requests are being processed per minute, and so on. You may create automated alerts for metrics—for example, to receive an email when an application’s memory usage exceeds a certain threshold.
- Tracing—Tracing allows you to follow (visually) a request as it flows through multiple components and services. This is useful for troubleshooting purposes and can help to find performance bottlenecks.
- Fault tolerance—Fault tolerance allows applications to gracefully deal with failures. For example, they can retry a request to a failing external service instead of propagating the failure to the caller.
- Service discovery—Service discovery is a way of dynamically finding the location of services that your application needs to interact with, allowing you to decouple the location of those services from your configuration. This makes deployments more robust and adaptable to changes.

### SmallRye
SmallRye (https://smallrye.io) is a set of implementations of the MicroProfile specifications. We said that Quarkus is also a MicroProfile implementation, so this begs for a bit of explanation. Each SmallRye project implements one of the MicroProfile specifications. Quarkus then provides an extension per each SmallRye project that integrates the SmallRye implementation into Quarkus and allows you to use it in your applications.


### Monitoring application health

The implementation of MicroProfile Health in Quarkus is SmallRye Health (integrated in the smallrye-health extension).

There are 5 kinds of health checks in SmallRye Health:
- Liveness
- Readiness
- Startup
- Wellness (not a part of MicroProfile specification)
- Custom health group (defined by users and not a part of MicroProfile specification)

### Database connection health check
When your application uses a JDBC data source, Quarkus automatically adds a readiness health check that verifies that the database connection is working. When the database is unavailable, the `readiness check` fails, saying that the application can’t process requests right now. Let’s try it out with the Inventory service with its MySQL connection.

quarkus-smallrye-health extension:
```
$ quarkus extension add smallrye-health
```

[Custom Health Check example](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-10/10_4_2/inventory-service/src/main/java/org/acme/inventory/health/CarCountCheck.java#L10)

### Application metrics
Generally, there are two kinds of metrics: 
- framework metrics
- application-specific (business) metrics.

### Micrometer
[Micrometer extension](https://micrometer.io) is the recommended way to work with metrics in Quarkus. Micrometer is a library that provides a common API for working with metrics, and it supports submitting metrics to monitoring backends, such as Prometheus, Graphite, SignalFX, or Datadog and others.
⚠️ There is a built-in SmallRye Metrics extension that is compatible with MicroProfile Metrics 4.0, but it’s not recommended and it will be removed in a future release. Instead, the Micrometer extension is preferred as the way forward.


### Micrometer Metric types
More information can be found here https://docs.micrometer.io/micrometer/reference/concepts.html
- Timer — Measures the time that it takes to execute a certain operation and generates a histogram of the measured times.
- Counter — A simple counter that can only be incremented; it counts the number of occurrences of a particular event.
- Gauge — A single numeric value that can change in any direction over time. An example would be the heap memory usage of the application.
- Distribution summary — A histogram of numeric values, just like a timer but not necessarily tied to time-related measurements.

### Micrometer metrics approaches
2 approaches with the Micrometer library (https://quarkus.io/guides/telemetry-micrometer) and Quarkus: 
- imperative (programmatic) -  is more flexible and allows for some more advanced 
- declarative (using annotations) - is much easier and less verbose

### Prometheus & Grafana
- Prometheus is an engine for collecting, storing, and querying metrics. It periodically makes HTTP requests to an application’s endpoint.  In Quarkus, this endpoint is served by the micrometer extension and is available (by default) at `/q/metrics` (http://localhost:{port}/q/metrics)
- Grafana is a dashboarding tool that can query the metrics from Prometheus and display them in a dashboard.

How to add Prometheus library  https://quarkus.io/guides/telemetry-micrometer-tutorial
```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
</dependency>
```

Grafana and Prometheus can be run using a docker file to collect the app metrics. The file can be found in `chapter-10/docker-compose-files/docker-compose-metrics.yml`. 
```
docker compose -f docker-compose-metrics.yml up
```

### Tracing
**OpenTelemetry** (https://opentelemetry.io) was conceived by merging two former projects: OpenTracing and OpenCensus, is the most popular tracing library in the cloud-native world. Commonly referred to as OTel for short, is a collection of various tools and APIs that are used to collect and export telemetry data from applications. OpenTelemetry doesn’t only cover tracing. It also has capabilities for collecting metrics and logs, but these were not yet considered ready and stable, and thus not supported by Quarkus at the time of writing this book, so we will focus only on the tracing part.  It is a vendor-neutral and programming language-agnostic. It provides a common protocol (named OTLP) for exporting telemetry data from applications to a tool named OpenTelemetry Collector, which then centrally processes the data and forwards it to a backend (e.g., Jaeger).
Usage of an **OpenTelemetry Collector** (a part of OpenTelemetry) is in most cases optional. Application frameworks may support exporting telemetry data directly to a backend without going through an OpenTelemetry Collector. For smaller-scale deployments, this is easier to set up and maintain, but for larger deployments, it is advised to use an OpenTelemetry Collector, because it can centrally add features like filtering, batching, and retrying in case of failures calling the backend (Jeager).
**Jeager** is used for vizualization.

![image](https://github.com/user-attachments/assets/4d5c4eb3-5862-4f70-85c8-c55d8e57f653)


How to add OpenTelemetry [quarkus-opentelemetry library]((https://quarkus.io/guides/opentelemetry)) in a service that should send metrics:
```
quarkus extension add opentelemetry 
```

There are 2 options how to run Jeager:
Directlry
```
docker run --rm -p 16686:16686 -p 4317:4317 docker.io/jaegertracing/all-in-one:1.62.0
```

Or use the docker file `chapter-10/docker-compose-files/docker-compose-tracing.yml`

Both OpenTelemetry Collector and Jeager listen the port localhost:4317, so we do not need to configure anything in our application.

Links:
[Quarkus and OpenTelemetry](https://quarkus.io/guides/opentelemetry)
[Quarkus and OpenTelemetry Tracing](https://quarkus.io/guides/opentelemetry-tracing). Examples how to add custom traces

### Fault Tolerance
[SmallRye Fault Tolerance documentation](https://smallrye.io/docs/smallrye-fault-tolerance/6.5.0/index.html)
[MicroProfile Fault Tolerance Library](https://github.com/microprofile/microprofile-fault-tolerance)
For Quarkus, the implementation of these strategies is provided by the quarkus-smallrye-fault-tolerance extension that brings in the SmallRye Fault Tolerance library.

Fault tolerance patterns:

- Retry —If an operation fails, retry it a certain number of times before propagating the failure back to the client.
- Fallback - If an operation fails, execute a fallback instead—that is, an alternative operation that is less likely to fail.
- Bulkhead - Limit the number of concurrent invocations of a certain operation. This prevents overloading the system.
- Circuit breaker - If an operation fails a certain number of times, stop reattempting it for some amount of time (instead, throw an error when the operation is requested). This helps to prevent cascading failures.
- Timeout - If an operation takes too long, abort it. This prevents the system from getting stuck and unresponsive.


Adding the smallrye-fault-tolerance extension to a service:
```
$ quarkus extension add smallrye-fault-tolerance
```

`@Retry` and `@FallBack` examples can be found [here](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-10/10_5_1/reservation-service/src/main/java/org/acme/reservation/rest/ReservationResource.java)


### Service discovery

if you can’t or don’t want to use the Kubernetes service discovery mechanism, Quarkus provides [SmallRye Stork](https://smallrye.io/smallrye-stork.), a library that implements an abstraction over different service discovery mechanisms, allowing you to easily swap between them. Kubernetes is one of the supported underlying mechanisms too, so you can use it together with Stork if you want the flexibility of switching to a different mechanism (for example, Consul).

Stork supports the following mechanisms:
- Consul
- DNS
- Kubernetes
- KNative
- Eureka
- Composite (a combination of multiple mechanisms)
- Static list (a hardcoded list of URLs)
- Custom mechanism implemented as a Java class


## Chapter 11 Quarkus in the cloud

![image](https://github.com/user-attachments/assets/a689817d-13b3-4f7c-9aba-097d6c8618d0)


### Running the application in Dev mode
Run Jaeger, Prometheus, and Grafana
```
$ docker compose -f docker-compose-files/docker-compose-observability
.yml up
```

Run the rest services:
- User Service and Keycloak container
```
cd chapter-11/11_1/users-service
quarkus dev
```
- Reservation service and PostgreSQL and RabbitMQ containers.
 ```
cd chapter-11/11_1/reservation-service
quarkus dev
```
- Rental service and  MongoDB and Redpanda containers.
 ```
cd chapter-11/11_1/chapter-11/11_1/rental-service
quarkus dev
```
- Inventory Service and MySQL
```
cd chapter-11/11_1/chapter-11/11_1/inventory-service
quarkus dev
```
- Billing Service and MongoDB
```
cd chapter-11/11_1/chapter-11/11_1/billing-service
quarkus dev
```

## Running the application in production

![image](https://github.com/user-attachments/assets/ce393508-45a1-454b-a57a-452a094fc305)
Pay attention that KeyCloak now has a separate PostgreSQL DB and RedPanda is replaced by Kafka



There are 2 MongoDB instances. They should be run on differen ports.

To support Graphql UI in prod add the property below. UI also will be available in Dev environment (http://localhost:8083/q/graphql-ui)
```
quarkus.smallrye-graphql.ui.always-include=true
```

 In prod mode, loading SQL scripts is disabled by default. To enable it use 
```
quarkus.hibernate-orm.sql-load-script=import.sql
```

To disable it in Dev mode set 
```
%dev.quarkus.hibernate-orm.sql-load-script=nonexistent-file
```

**Run the App in production**
1.Open the following directories, each in a new terminal, and run `quarkus build` (`./mvnw clean package`) followed by `java -jar target/quarkus-app/quarkus-run.jar`:
TODO: what the difference comparing to `quarkus build --native --container-image`
```
chapter-11/11_1_1/users-service
chapter-11/11_1_1/reservation-service
chapter-11/11_1_1/rental-service
chapter-11/11_1_1/inventory-service
chapter-11/11_1_1/billing-service
```
2.Use `chapter-11/docker-compose-files/docker-compose-infra.yml` to run all supported containers like KeyCloak, MongoDB, MySQL, Kafka, etc..
```
$ docker compose -f docker-compose-files/docker-compose-infra.yml up
$ docker compose -f docker-compose-files/docker-compose-infra.yml down
```
3. Run the builded docker images
``
docker compose -f docker-compose-files/docker-compose-car-rental.yml up
docker compose -f docker-compose-files/docker-compose-car-rental.yml down
``

### Removing hardcoded URLs
We going to get rid of hardcoded URLs like  `@RegisterRestClient(baseUri = "http://localhost:8081")`
There are 2 ways:
- `@RegisterRestClient(configKey = "reservations")` + updating application.properties `quarkus.rest-client.reservations.url=http://localhost:8081`
- It’s also possible to override the REST client’s URL without specifying a custom config key—the default config key is the fully qualified name of the interface. In that case, the property would be `quarkus.rest-client."org .acme.users.ReservationsClient".url=http://localhost:8081`

### Credentials in the application.properties 
Is not the best idea. However, it is the easiest for our use case. In the real production deployment, you could externalize this configuration in many ways (different config locations, environment variables, system properties, Kubernetes secrets).


### Building and pushing container images
https://quarkus.io/guides/container-image
Quarkus also provides [five extensions](https://quarkus.io/guides/container-image) that provide automation of the image building and pushing:
- Jib - quarkus-container-image-jib
- Docker - quarkus-container-image-docker
- Buildpack - quarkus-container-image-buildpack
- Podman - quarkus-container-image-podman
- OpenShift - quarkus-container-image-openshift. This extension uses OpenShift-specific binary builds. Such a build takes your built artifact (and dependencies) and uploads it to the OpenShift cluster. OpenShift then builds the application image automatically in the OpenShift build system. This is also called s2i (source to image). From the user’s point of view, you don’t need to do anything. The extension generates everything required for your s2i build to complete successfully.

### Building images with Quarkus without extensions
We don’t need to add the extensions mentioned previously to our Quarkus application to start building images. Quarkus CLI quarkus already ships with built-in commands that we can use. For instance, to create an image with Jib, you can use the command in the following listing that we can test—for example, in the Reservation service.

Note  This functionality also works with the Maven plugin (./mvnw quarkus :image-build) but not with Gradle. Maven supports adding dynamic dependencies, but Gradle doesn’t. The CLI works in both cases because it implements a workaround for Gradle (which is not applicable when running a Gradle task directly).

How to build an image. Command accepts `jib, docker, podman, buildpack, and openshift` parameters. openshift requires a connection to the OpenShift cluster and the manifests (that are generated by either openshift or kubernetes extensions)
```
quarkus image build jib
```

Pushing the image:
```
quarkus image push
```


### Generating Kubernetes resources
Since writing long YAML is a tedious and error-prone task, Quarkus provides extensions to do this work for us in the background. It utilizes a library called [Dekorate](https://dekorate.io) that generates Kubernetes manifests. It generates sensible defaults for modern Java applications and provides easy customization options (e.g., with properties or annotations). Additionally, the generated manifests can be combined with predefined ones (if you have resources you need to deploy together).

Quarkus generates Kubernetes manifests with the following extensions that target three leading platforms:
- [quarkus-kubernetes](https://quarkus.io/guides/deploying-to-kubernetes) — Original Kubernetes
- [quarkus-openshift](https://quarkus.io/guides/deploying-to-openshift) — OpenShift-specific manifests
- [quarkus-knative](https://quarkus.io/kubernetes-native/) — Serverless platform (section 11.5)

  Apart of the guides for every platform you can use [All Config](https://quarkus.io/guides/all-config) to find all the parameters that can be customized

The generated manifest can also be enhanced by already-existing manifests that you, as the application developer, provide. This is useful if you already have some manifests you must base on or apply for your application to function correctly. An example can be a database that deploys together with the Quarkus application (which we will see in the next section). We can do this by placing a file named `kubernetes.yml` (or `openshift.yml`, `knative.yml`, or their JSON variants) to the src/main/ kubernetes directory. When such file is detected during build, Quarkus combines it with the manifest generated by the relevant extension.

Kubernetes\OpenShift cluster setup is not covered in this book. But if you would like to experiment, you can use lightweight clusters like :
- Kind (https://kind.sigs.k8s.io)
- K3s (https://k3s.io)
- Minikube (https://minikube.sigs.k8s.io/docs)
- Some online (often paid) Kubernetes platform is also an option.


## Chapter 11 Kubernetes and OpenShift integration
In [Kubernetes extension manual](https://quarkus.io/guides/deploying-to-kubernetes) you can find how to deply Quarkus apps on Kubernetes. There are different features including [Service Binding](https://quarkus.io/guides/deploying-to-kubernetes#service_binding) that allows not only generate a kubernetes manifest and deploy your application, but also includ configuration for an additional service that your app required, for example, a DB.
⚠️ In this course they say there is a simpler way to deploy a DB with the application. we just need to copy `mysql.yaml` config into `chapter-11/11_3_3/inventory-service/src/main/kubernetes/kubernetes.yml` and that't it. There is no need to apply `quarkus-kubernetes-service-binding` extension.

There is a db URL in our `application.properties`, if we want to override this property for kubernetes we should provide both properties: 
```
%prod.quarkus.datasource.jdbc.url=jdbc:mysql://localhost:3306/quarkus
quarkus.kubernetes.env.vars.quarkus-datasource-jdbc-url=jdbc:mysql://mysql:3306/inventory # where 'mysql' is name from kubernetes manifest ??
```

Also Kubernetes requires a namespace property
```
quarkus.kubernetes.namespace=default
```

Applying the manifest
```
kubectl apply -f inventory-service/target/kubernetes/kubernetes.yml
```

Inventory service logs available at http://localhost:8083/q/graphql-ui or check its logs with `kubectl logs deployment/inventory-service`.

### Automating Kubernetes deployments
With a single build time flag `quarkus.kubernetes.deploy=true`, we can, in one command,

- Build our Quarkus application and its image.
- Push the built image to the registry.
- Apply/reapply the generated manifest to the Kubernetes cluster.

Example:
```
./mvnw clean package -Dquarkus.kubernetes.deploy=true
```

### Openshift
[Openshift](https://www.redhat.com/en/technologies/cloud-computing/openshift) is a Red Hat-branded version fork of Kubernetes that provides additional features, easier management, and (opinionated) better usability. Most of the features we covered for Kubernetes in the previous sections apply also to OpenShift. We decided to focus on OpenShift because  it comes with:
- ⚠️ new resources, intuitive UI,
- ⚠️ and most importantly, a free public OpenShift instance called Sandbox that you can use for your testing.

You don’t need to install almost anything (besides the client-side tool, oc) on your local systems to experiment with Quarkus on OpenShift!
Ff you would like to try OpenShift on your local system, you can use the [OpenShift Local](https://developers.redhat.com/products/openshift-local/overview). OpenShift Local provides functionality similar to Minikube for Kubernetes.
Link: [Deploying Quarkus applications to OpenShift](https://quarkus.io/guides/deploying-to-openshift)

### Apply OpenShift
- remove Kubernetes extension `$ quarkus ext remove kubernetes`
- remove Docker extension of set OpenShift as a default image builder
```
quarkus.container-image.builder=openshift
```
Once you build the application `openshift.yml` and `openshift.json` files will be generated

To include the MySQL configuratio to deployment put it in `src/main/kubernetes directory/openshift.yml`
Examples can be found [here](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-11/openshift/openshift-default.yml)
After building the application and manifests, we can now directly apply the generated openshift.yml (remember that you first need to log in the same terminal where you run these commands), which produces several resources with the `oc` tool, as follows:
```
$ oc apply -f inventory-service/target/kubernetes/openshift.yml
$ oc get pods
$ oc get routes
$ oc whoami --show-console
```

We can navigate to the exposed Inventory service route URL by going to `<your-url>` or clicking the route button as shown in figure 11.5. Change the path to `http:// <your-url>/q/graphql-ui`, and you will see the familiar UI of the Inventory service now running in OpenShift! 

### Automating OpenShift deployment with s2i
We’ve prepared the BuildConfig resource to trigger application redeploy when the s2i build finishes. However, because we configured `quarkus.container-image.* properties`, Quarkus automatically picks them to align generated manifests to point to the deployed image. If we want to utilize the image built with s2i, we need to remove them. To remove the need to have them specified whenever we build or push images (if we decide to do so again), we can define a custom s2i configuration profile that removes these properties (listing 11.16).

Listing 11.16 The s2i profile removing container image properties
```
%s2i.quarkus.container-image.registry=
%s2i.quarkus.container-image.group=
%s2i.quarkus.container-image.tag=
```
If you now regenerate openshift.yml with the s2i profile active, it points to the `inventory-service:1.0.0-SNAPSHOT` image, which corresponds to the ImageStreamTag produced by our BuildConfig. To trigger the s2i build, we can run the following command that sets the required flags to use our new config profile (in addition to the prod profile) and to trigger an s2i build:
```
$ ./mvnw clean package -Dquarkus.profile=prod,s2i -Dquarkus.openshift.deploy=true
```

### Kubernetes and OpenShift clients
We have utilized various management tools (kubectl or oc) that have allowed us to manage our Kubernetes or OpenShift platforms.
While there are other ways to deploy Quarkus applications (e.g., `OpenShift UI` or `oc new-app` command), they all require manual steps.
Quarkus also allows us to define our deployment workflow in Java directly in the Quarkus application. For this reason, ⚠️ Quarkus provides 
- `extensions—quarkus-kubernetes-client`
-  `quarkus-openshift-client`
  that integrate [Fabric8 client](https://github.com/fabric8io/kubernetes-client). The Fabric8 library provides programmatic access to the Kubernetes and OpenShift REST API. See [example](https://github.com/xstefank/quarkus-in-action/blob/0a7e10d43fd36a2f29104900418b91941b814233/chapter-11/11_4/openshift-client-example/src/main/java/org/acme/PodResource.java)

### Serverless application with Quarkus
There are several serverless platforms (aka FaaS, Function as a Service) on the market (e.g., Knative, AWS Lambda, Google Cloud Functions, Azure Functions).

### Funqy library
[Quarkus Funqy Docs](https://quarkus.io/guides/funqy)
Each provides its own Java API that can be utilized in your Quarkus application. But each API is different, meaning using such API locks your application to a particular platform.

Quarkus’s serverless strategy is based on the library called `Funqy`. The library provides a unified API that abstracts all FaaS platforms mentioned earlier. It represents a very simple API that we can use to develop Quarkus serverless applications.

Example use of the Funqy API
 ```
import io.quarkus.funqy.Funq;

public class Function {
    @Funq
    public String process(String input) {
        return "Processed: " + input;
    }
}
```

### Car statistics application with Knative
In this section, we develop a new but totally optional service called `car-statistics` that we deploy as a serverless function with Knative. We chose Knative as the easiest platform to utilize since it is preinstalled already in the OpenShift Sandbox (refer to 11.6.1 for setup instructions) in its Red Hat-branded product version called OpenShift Serverless. It calls our deployed Inventory service using GraphQL to return some statistics of currently tracked cars. Since a service like this doesn’t need to run all the time, it’s a perfect target for serverless because at times when we don’t need the data, we don’t need to keep the application running.

⚠️If you’re using the OpenShift Sandbox, you can start right away. If you’re using custom OpenShift or Kubernetes, you must install [Knative](https://knative.dev/docs/install/) manually .

Create a new Quarkus car-statistics application:
```
quarkus create app org.acme:car-statistics -P 3.15.1 --extension \
funqy-http,smallrye-graphql-client,openshift --no-code
```
Full application example can be found here [Car-statistics](https://github.com/xstefank/quarkus-in-action/tree/0a7e10d43fd36a2f29104900418b91941b814233/chapter-11/11_5_3/car-statistics)

⚠️If you’re using the prepared solution from the book’s resources, don’t forget to change the quarkus.container-image.group to your OpenShift namespace.

The `quarkus.kubernetes.deployment-target` comes from the underlying Kubernetes extension (since Knative is not specific to OpenShift). It specifies what resources Quarkus generates. The possible values include `kubernetes`, `openshift`, `knative`, `minikube`, and `kind` or any combination of these values. 

Deployment:
```
$ ./mvnw clean package -Dquarkus.knative.deploy=true
```
This command triggers an s2i build of our `car-statistics` application that we configured our Knative function to point to in listing 11.19. You can verify this in the generated `knative.yml/json` files in the `target/kubernetes` directory.
The app is availabe by the following URL `http http://<your-route>/getCarStatistics`

For more information read [Quarkus Funqy Docs](https://quarkus.io/guides/funqy)

### Setting up OpenShift Sandbox
The Sandbox is a free (30 days⚠️), testing, development-targeted, and shared OpenShift cluster with 14 GB of RAM and 40 GB storage for 30 days.
To start with OpenShift Sandbox, navigate to [sandbox](https://dn.dev/rhd-sandbox) and click the Start your sandbox for free button.
we always log in with the DevSandbox account into the <your-username>-dev project (namespace). After you log in (by clicking the DevSandbox button),

How to download [OC CLI Tool](https://docs.redhat.com/en/documentation/openshift_container_platform/4.7/html/cli_tools/openshift-cli-oc#cli-getting-started)
[How to access the OpenShift from local system](https://www.ibm.com/support/pages/how-access-openshift-local-system)

### Car rental infrastructure deployment with OpenShift Sandbox
```
 oc apply -f car-rental/car-rental-dependent-services.yml
 oc delete -f car-rental/car-rental-dependent-services.yml
```

Final settings for all the services can be found [here](https://github.com/xstefank/quarkus-in-action/tree/0a7e10d43fd36a2f29104900418b91941b814233/acme-car-rental)


## Chapter 12 Custom Quarkus extensions
If you ever decide to create a new Quarkus extension, and you believe that it might be useful for others, you can have it published in the Quarkiverse (https://quarkiverse.io, https://github.com/quarkiverse). We already discussed this at the end of chapter 2. That also means that before you actually decide to write a new extension, you should check the Quarkiverse to see if someone has already created a similar one!

[Writing your own extension](https://quarkus.io/guides/writing-extensions)
[Building my first extension](https://quarkus.io/guides/building-my-first-extension)

### Modules
Some Quarkus extensions also generate new bytecode or modify existing bytecode directly, without using a recorder. For that, they make use of a tool called Gizmo. Gizmo (https://github.com/quarkusio/gizmo) is a project that provides an API for generating and manipulating JVM bytecode. A typical use case for this is reducing runtime usage of Java reflection by generating bytecode that directly invokes a method instead of using reflection to find and invoke it.

### Kotlin Support
[Kotlin Support Docs](https://quarkus.io/guides/kotlin)


### Quarkus FE Tools
### Quinoa
Quinoa is a Quarkus extension whose goal is to ease development, building, and deploying of single-page web applications. It is compatible with any framework that uses NodeJS for building (React, Angular, Vue, etc.). You quickly get a full-stack Quarkus single-page application and benefit from all the Quarkus eco-system (full-stack dev mode, GraphQL, REST endpoints, messaging, etc.).


More information [here](https://docs.quarkiverse.io/quarkus-quinoa/dev/index.html).

### Renarde
Quarkus Renarde is a new server-side rendered Web Application framework based on Quarkus. Its main role is to bind together Qute, Hibernate, and RESTEasy Reactive by creating a concise MVC (Model-View-Controller) layer over them.

More information [here](https://docs.quarkiverse.io/quarkus-renarde/dev/index.html)
