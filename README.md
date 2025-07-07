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
