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
- MicroProfile https://microprofile.io/
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
| **Mandrel**    | Native image for Quarkus       | Stable native builds, Red Hat supported |


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
