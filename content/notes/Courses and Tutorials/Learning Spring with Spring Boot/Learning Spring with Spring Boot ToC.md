JDK 17

Spring supports Maven and Gradle

Will be using Maven

Postgres database will be used


**lot more notes to add for section 1**

# Introduction to Spring

POJO - Plain Old Java Object

Java Beans - Simple objects with only getters and setters

Spring beans - POJOs configured in the application context

DTO - Bean used to move state between layers

## Inversion of Control

IoC provides a mechanism of dependency injection

Application Context wraps the Bean Factory which serves the beans at the runtime of the application

Spring Boots provides auto-configuration of the application context

# Introduction to Spring Boot

- SB supports rapid development
- Removes boilerplate of application setup

## Key Aspects

- Embedded tomcat
- Auto-configuration of Application Context
- Automatic Servlet Mappings
- Automatic Controller Mappings

# Create a Project with Spring Initializr

mvn package

`java -jar target\learning-spring-0.0.1-SNAPSHOT.jar`

# Inversion of Control

- Container maintains your class dependencies
- Objects injected at runtime or start-up time
- An object accepts the dependencies for construction instead of constructing them

## Traditional Dependency Management

![[Images/Pasted image 20240928202155.png|400]]

## IoC Dependency Management

![[Images/Pasted image 20240928202236.png|600]]

## Spring IoC

# Annotations Everywhere

## What are Annotations

- Native to Java
- Metadata for your code
- Often used for compiler or runtime instructions
- Great leverage point for point cuts (aspect oriented programming model, spring is)

## Proxies

- Beans in the Bean Factory are proxied
- Annotations drive proxies
- Annotations are easy extension points, for your own abstracts too
- Method calling order matters

---

Data Access in Spring

---

# Welcome to Spring Data

## What is Spring Data?

- Provides a common set of interfaces
- Provides a common naming convention
- Provides inspected behaviour
- Provides repository and Data Mapping convention

## Benefits of Spring Data

- Remove boilerplate code
- Allows for swapping data sources easier
- Allows to focus on business logic

## Key Components

- Repository interface
- Entity object
- DataSource

# Embedded Databases with Spring Boot

`logging.level.org.springframework.jdbc.datasource.init.ScriptUtils=debug`

# Repositories with Spring Data

