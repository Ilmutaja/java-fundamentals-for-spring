# Java Fundamentals for Spring — Core Concepts for Backend Devs

[![Releases](https://img.shields.io/badge/Releases-v1.0-blue?logo=github)](https://github.com/Ilmutaja/java-fundamentals-for-spring/releases)  [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://img.shields.io/badge/License-Apache%202.0-blue.svg)  [![Topics](https://img.shields.io/badge/Topics-java%2C%20spring-blue)](https://github.com/Ilmutaja/java-fundamentals-for-spring)

<img src="https://spring.io/images/blogs/spring-boot.png" alt="Spring Boot" width="220" style="margin:12px 0" />

A focused guide and code lab that brings core Java skills into the Spring ecosystem. The repo pairs clear theory with runnable examples. It covers OOP, collections, generics, functional APIs, concurrency, dependency injection, design patterns, testing, and more. Every module ties back to how Spring uses the concept.

Release artifacts: download and run the release asset from https://github.com/Ilmutaja/java-fundamentals-for-spring/releases. The release file must be downloaded and executed.

Table of contents
- About
- Who this is for
- What you get
- Quick links
- Modules
- How to run examples
- Mapping to Spring
- Exercises and practice tasks
- Testing strategy
- Contributing
- License
- Releases

About
- Focus: core Java for backend developers who want to master Spring.
- Format: 12 modules, each with theory, small code examples, exercises, and a mini-project.
- Deliverable: runnable Maven projects and single-file demos. Use the release artifact to run the packaged examples.

Who this is for
- Backend engineers new to Spring.
- Java devs who want a concise, hands-on review.
- Developers preparing for interviews or code reviews.
- Teams that want a baseline curriculum for onboarding.

What you get
- 12 modules with source code and tests.
- Clean, idiomatic examples that map to Spring patterns.
- Exercises with answers and test suites.
- Maven build for each module.
- One integrated sample app that shows concepts in a Spring Boot service.

Quick links
- Releases (download and run the included artifact): https://github.com/Ilmutaja/java-fundamentals-for-spring/releases
- Repo topics: collections-java, concurrency, dependency-injection, design-patterns, functional-programming-in-java, generics-in-java, java, oop-principles, programming-fundamentals, spring-boot, testing

Modules (overview)
1. Module 01 — Java and the JVM
   - Class loading, bytecode, memory model, GC basics.
   - javac, java, jars, classpath.
2. Module 02 — OOP and SOLID
   - Encapsulation, inheritance, polymorphism.
   - Interfaces, abstract classes, Liskov substitution.
3. Module 03 — Primitives and Object Types
   - Boxing, unboxing, equality, hashCode contract.
4. Module 04 — Generics and Type Safety
   - Wildcards, bounded types, type erasure.
   - How Spring uses generics for repositories and beans.
5. Module 05 — Collections and Streams
   - Lists, Sets, Maps, concurrent collections.
   - Streams, collectors, parallel streams and pitfalls.
6. Module 06 — Functional Java
   - Lambdas, functional interfaces, method refs.
   - Composable operations and side-effect control.
7. Module 07 — Concurrency and Threads
   - Thread lifecycle, ExecutorService, futures, synchronization.
   - Locks, CAS, ForkJoin.
8. Module 08 — Design Patterns
   - Factory, Singleton, Strategy, Observer, Adapter, Decorator.
   - How patterns appear in Spring (FactoryBean, AOP, etc.).
9. Module 09 — Dependency Injection & IoC
   - Constructor vs setter injection, bean scopes, lifecycle callbacks.
   - Testable design with DI.
10. Module 10 — I/O and Serialization
    - Files, NIO, JSON binding, Jackson basics.
11. Module 11 — Testing
    - Unit tests with JUnit 5, Mockito, Testcontainers intro.
    - Contract tests and integration tests with Spring.
12. Module 12 — Sample App
    - Small Spring Boot backend that uses the earlier modules.
    - Endpoint examples, service layer, repository layer, configuration.

Project layout (example)
- modules/
  - module-01-jvm/
  - module-02-oop/
  - ...
- sample-app/
  - src/main/java/...
  - pom.xml
- exercises/
  - solutions/
- docs/
  - cheatsheets.md
  - patterns.md

How to run examples (local)
Prerequisites
- JDK 11+ (JDK 17 recommended)
- Maven 3.6+
- Git

Quick start (local)
1. Clone the repo.
2. Build: mvn -T 1C -pl sample-app -am clean package
3. Run sample app: java -jar sample-app/target/sample-app-0.1.0.jar

Run a single module
- cd modules/module-05-collections
- mvn test
- mvn -q package
- java -jar target/module-05-collections.jar

Run the packaged release
- Download the release asset from https://github.com/Ilmutaja/java-fundamentals-for-spring/releases
- Unpack the archive
- Execute the launcher script or run the jar file provided in the release
- Example: java -jar java-fundamentals-for-spring-releases-1.0.jar
The release file must be downloaded and executed.

Mapping concepts to Spring
- DI: Use constructor injection in services. Favor immutability for thread safety.
- Beans: Use @Component and @Configuration for configuration classes. Use profiles for environment-specific beans.
- Collections and Streams: Use streams in service logic. Avoid parallel streams in request handling unless you control the thread pool.
- Concurrency: Use TaskExecutor in Spring for managed async tasks. Use @Transactional for DB consistency and thread boundaries.
- Generics: Use generics in repository interfaces. Spring Data leverages generics for type-safe repositories.
- Patterns: Use FactoryBean for complex bean creation. Use Strategy for pluggable algorithms. Use Adapter to translate external models.

Examples and snippets
- DI constructor
  - public class UserService {
      private final UserRepository repo;
      public UserService(UserRepository repo) { this.repo = repo; }
    }
- Stream chunk
  - List<String> names = users.stream()
        .map(User::getName)
        .filter(Objects::nonNull)
        .collect(Collectors.toList());
- Thread pool
  - ExecutorService exec = Executors.newFixedThreadPool(8);
  - var future = exec.submit(() -> fetchUserData(id));

Exercises and practice tasks
- Small tasks are in exercises/ numbered by module.
- Each task has tests. Run mvn test in the exercise module.
- Sample tasks:
  - Implement a thread-safe LRU cache with tests.
  - Write a generic Mapper that maps DTOs to entities.
  - Use CompletableFuture to parallelize two independent I/O calls and combine results.
- Solutions live in exercises/solutions. Try the tests before you open the solution.

Testing strategy
- Unit tests: JUnit 5. Keep tests small and deterministic.
- Mocking: Use Mockito with argument captors when needed.
- Integration: Use Spring Boot Test with @SpringBootTest for wiring checks.
- DB tests: Use Testcontainers for a repeatable DB runtime.
- CI: Use GitHub Actions to run mvn -T 1C -DskipTests=false verify.

Code style and conventions
- Follow Google Java Style or company standard.
- Use final for fields that do not change.
- Prefer small methods. One responsibility per method.
- Favor immutable value objects for thread safety.

Contributing
- Fork the repo.
- Create a feature branch for each module change.
- Open a pull request with tests and a short description.
- Keep changes focused to one module or task.
- Use clear commit messages.

Roadmap
- Add more advanced concurrency patterns and examples.
- Add a reactive module with Project Reactor and WebFlux.
- Add guided quizzes and certification path.

Badges and images
- Use the releases badge link above to fetch the release.
- Company and tool logos:
  - Java: https://www.oracle.com/a/tech/img/cb88-java-logo-001.jpg
  - Spring: https://spring.io/images/logo-spring.svg

License
- Apache 2.0

Contact
- Use GitHub issues for questions, bug reports, and feature requests.

Releases
- Download and run the release asset from https://github.com/Ilmutaja/java-fundamentals-for-spring/releases. The release file must be downloaded and executed. Check the Releases page for packaged jars, scripts, and a combined PDF guide.