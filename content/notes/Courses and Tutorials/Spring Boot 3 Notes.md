# Quick Start

## Maven

**POM** - Project Object Model file

Contains a list of dependencies

### POM File Structure

![[Pasted image 20250228105511.png]]

### Simple POM File

![[Pasted image 20250228105552.png]]

### Project Coordinates

![[Pasted image 20250228110208.png]]

#### Elements

![[Pasted image 20250228110255.png]]

### Dependency Coordinates

![[Pasted image 20250228110440.png]]

## Spring Boot Project Files

![[Pasted image 20250228110716.png]]

### Maven Wrapper Files

![[Pasted image 20250228110858.png]]


### Maven POM File

![[Pasted image 20250402135153.png]]


### Application Properties

![[Pasted image 20250402135409.png]]

#### Reading Data from Application Properties

![[Pasted image 20250402135452.png]]

### Template Auto-configuration Files

![[Pasted image 20250402135627.png]]

### Unit Tests

![[Pasted image 20250402135706.png]]

## Spring Boot Starters

### Starter Web

![[Pasted image 20250402135906.png]]

#### Setup Through Spring Initializr

![[Pasted image 20250402140008.png]]

### Spring Initializr

![[Pasted image 20250402140103.png]]

## Parents for Starters

![[Pasted image 20250402140324.png]]

## `spring-boot-devtools`

Automatically restarts your application when code is updated

![[Pasted image 20250402140709.png]]

### IntelliJ Setup for DevTools

![[Pasted image 20250402141020.png]]

Then check `auto-make to start even if developed application is currently running`

![[Pasted image 20250402141408.png]]

Then to run the project

![[Pasted image 20250402141537.png]]

## Spring Boot Actuator

![[Pasted image 20250402141907.png]]

### Add Dependency

![[Pasted image 20250402141943.png]]

### Endpoints

Endpoints are prefixed with `/actuator`

#### Health

![[Pasted image 20250402142058.png]]

#### Exposing Endpoints

![[Pasted image 20250402142341.png]]

![[Pasted image 20250402142534.png]]

#### Info

![[Pasted image 20250402142425.png]]

#### Beans

![[Pasted image 20250402142644.png]]

#### Others

![[Pasted image 20250402142454.png]]

### Security

![[Pasted image 20250402143040.png]]

#### Secured Endpoints

![[Pasted image 20250402143143.png]]

#### Security Configuration

![[Pasted image 20250402143222.png]]

#### Excluding Endpoints

![[Pasted image 20250402143321.png]]

## Run From Command Line

![[Pasted image 20250402143452.png]]

### `java -jar`

![[Pasted image 20250402143533.png]]

1. `mvwn package`
2.  `java -jar target\myapp.jar`

### `mvnw`

![[Pasted image 20250402143619.png]]

![[Pasted image 20250402143649.png]]

If Spring Boot Plugin is used then can use:

1. `mvnw spring-boot:run`

## Injecting Custom Application Properties

![[Pasted image 20250402144305.png]]

### Define Custom Application Properties

![[Pasted image 20250402144346.png]]

### Inject Properties into Spring Boot App

![[Pasted image 20250402144420.png]]

## Configuring Spring Boot Properties

### Core Properties

![[Pasted image 20250402144611.png]]

### Web Properties

![[Pasted image 20250402144638.png]]

### Actuator Properties

![[Pasted image 20250402144704.png]]

### Security Properties

![[Pasted image 20250402144733.png]]

### Data Properties

![[Pasted image 20250402144757.png]]

# Spring Core

## Inversion of Control

**The approach of outsourcing the construction and management of objects**

![[Pasted image 20250402150501.png]]

Primary functions of the **Spring Container**
- Create and manage objects - **Inversion of Control**
- Inject object dependencies - **Dependency Injection**

## Dependency Injection

**Dependency Inversion Principle** - Client delegates the responsibility of providing its dependencies to another object

![[Pasted image 20250402150819.png]]

Injecting object's dependency's (Dependency Injection) is one of the Spring Containers' primary functions

### Injection Types

#### Constructor Injection

- Use when you have required dependencies
- Recommended as first choice

#### Setter Injection

- Use when you have optional dependencies
- If dependency is not provided, your app can provide reasonable default logic

### Spring AutoWiring

![[Pasted image 20250408110347.png]]

#### Example

![[Pasted image 20250408110419.png]]

### Constructor Injection Example

![[Pasted image 20250408110522.png]]

![[Pasted image 20250408110542.png]]

#### 1. Define Dependency Interface and Class

![[Pasted image 20250408110629.png]]

##### @Component Annotation

![[Pasted image 20250408110709.png]]

#### 2. Create Demo REST Controller

![[Pasted image 20250408110733.png]]

#### 3. Create  a Constructor in your Class for Injections

![[Pasted image 20250408110841.png]]

#### 4. Add @GetMapping for `/dailyworkout`

![[Pasted image 20250408110926.png]]

#### How Spring Processes your Application

![[Pasted image 20250408111836.png]]

## Component Scanning

![[Pasted image 20250408112000.png]]

![[Pasted image 20250408112122.png]]

![[Pasted image 20250408112202.png]]

![[Pasted image 20250408112248.png]]

![[Pasted image 20250408112335.png]]

### Explicit Scanning

![[Pasted image 20250408112427.png]]

## Setter Injection

Inject dependencies by calling setter methods on your class

### Autowiring Example

![[Pasted image 20250408164417.png]]

#### Development Process

![[Pasted image 20250408164452.png]]

#### 1. Create Setter Methods in your Class for Injections

![[Pasted image 20250408164533.png]]

#### 2. Configure the Dependency Injection with Autowired Annotation

![[Pasted image 20250408164604.png]]

### How Spring Processes your Application

![[Pasted image 20250408164644.png]]

## Field Injection

Generally makes the code harder to unit test

Not recommend but still used

### 1. Configure the Dependency Injection with Autowired Annotation

![[Pasted image 20250408165252.png]]

## @Qualifier

### Constructor Injection

![[Pasted image 20250408170349.png]]

### Setter Injection

![[Pasted image 20250408171811.png]]

## @Primary

![[Pasted image 20250408172357.png]]

Out of multiple classes - this is the primary class you should use

Can only use one `Primary`

![[Pasted image 20250408172553.png]]

## Lazy Initialization

By default, when your application starts, all beans are initialized

Spring will create an instance of each and make them available

Lazy Initialization, instead will:
- Only be initialized if needed for dependency injection
- Only be initialized if explicitly requested

Add `@Lazy` to the given class

![[Pasted image 20250408173200.png]]

### Global Configuration

![[Pasted image 20250408173420.png]]

### Advantages/Disadvantages

![[Pasted image 20250408173515.png]]

## Bean Scope

Default Scope is Singleton

![[Pasted image 20250408181204.png]]

![[Pasted image 20250408181238.png]]

### Explicitly Specify Bean Scope

![[Pasted image 20250408181328.png]]

### Additional Bean Scopes

![[Pasted image 20250408181405.png]]

### Prototype Scope Example

![[Pasted image 20250408181704.png]]

### Checking Scope

![[Pasted image 20250408181738.png]]

## Bean Lifecycle Methods

![[Pasted image 20250408181819.png]]

![[Pasted image 20250408182301.png]]

### Init Configuration

![[Pasted image 20250408182355.png]]

### Destroy Configuration

![[Pasted image 20250408182421.png]]

For "prototype" scoped beans, Spring does not call the destroy method

In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean: the container instantiates, configures, and otherwise assembles a prototype object, and hands it to the client, with no further record of that prototype instance

## Java Config Bean

### Development Process

![[Pasted image 20250408182557.png]]

#### 1. Create a Java Class and Annotate as `@Configuration`

![[Pasted image 20250408182639.png]]

#### 2. Define `@Bean` method to Configure the Bean

![[Pasted image 20250408182710.png]]

#### 3. Inject the Bean into our Controller

![[Pasted image 20250408182734.png]]

### Use case for `@Bean`

![[Pasted image 20250408182814.png]]

### Example: Configure AWS S3 Client using `@Bean`

![[Pasted image 20250408183044.png]]

![[Pasted image 20250408183123.png]]



# Hibernate/JPA CRUD

## Hibernate

**Hibernate** - A framework for persisting/saving objects in a database

![[Pasted image 20250410102634.png]]

### Benefits of Hibernate

![[Pasted image 20250410104713.png]]

### Object-to-Relational Mapping (ORM)

![[Pasted image 20250410104748.png]]

Class maps to database table

## Jakarta Persistence API - JPA

Or Java Persistence API

The standard API for ORM

- Defines a set of interfaces
- Requires an implementation to be usable

Hibernate and EclipseLink are JPA implementations

### Benefits of JPA

![[Pasted image 20250410105040.png]]

### Sava a Java Object with JPA

![[Pasted image 20250410105253.png]]

### Retrieving a Java Object with JPA

![[Pasted image 20250410105345.png]]

### Querying for Java Objects

![[Pasted image 20250410105433.png]]

## Hibernate/JPA and JDBC

![[Pasted image 20250410105545.png]]

## Automatic Data Source Configuration

Hibernate is the default implementation of JPA in Spring Boot

`EntityManager` (from JPA) is the main component for creating queries

![[Pasted image 20250410110436.png]]

## Setup Project with Initializr

![[Pasted image 20250410110512.png]]

![[Pasted image 20250410110539.png]]

### `application.properties`

![[Pasted image 20250410110632.png]]

### `CommandLineRunner`

![[Pasted image 20250410110758.png]]

## JPA Annotations

**Entity Class** - Java class that is mapped to a database table

![[Pasted image 20250410111024.png]]

![[Pasted image 20250410111128.png]]

### 1. Map Class to Database Table

![[Pasted image 20250410111212.png]]

### 2. Map Fields to Database Columns

![[Pasted image 20250410111250.png]]

### `@Column`

![[Pasted image 20250410111339.png]]

### Primary Key

![[Pasted image 20250410111455.png]]

#### ID Generation Strategies

![[Pasted image 20250410111537.png]]

#### Define your own Customer Generation Strategy

![[Pasted image 20250410111637.png]]

## Saving a Java Object with JPA

### Data Access Object (DAO)

![[Pasted image 20250410111859.png]]

![[Pasted image 20250410112018.png]]

### JPA Entity Manager

![[Pasted image 20250410112100.png]]

#### `JPARepository` vs `EntityManager`

![[Pasted image 20250410112313.png]]

![[Pasted image 20250410112331.png]]

### DAO Key Steps

![[Pasted image 20250410120509.png]]

#### 1. Define DAO Interface

![[Pasted image 20250410120537.png]]

#### 2. Define DAO Implementation

##### `@Transactional`

Automatically begin and end a transaction for your JPA code

##### `@Repository`

![[Pasted image 20250410120852.png]]

![[Pasted image 20250410132138.png]]

![[Pasted image 20250410132226.png]]

#### 3. Update Main App

![[Pasted image 20250410132309.png]]

## Reading Objects with JPA

![[Pasted image 20250410132824.png]]

### 1. Add new Method to DAO Interface

![[Pasted image 20250410133057.png]]

### 2. Define DAO Implementation

![[Pasted image 20250410133151.png]]

### 3. Update Main App

![[Pasted image 20250410133227.png]]

## Querying Objects with JPA

### JPA Query Language (JPQL)

![[Pasted image 20250410134207.png]]

### Retrieve All

![[Pasted image 20250410134303.png]]

### `FROM WHERE`

![[Pasted image 20250410134320.png]]

### `LIKE`

![[Pasted image 20250410134402.png]]

### Name Parameters

![[Pasted image 20250410134448.png]]

### `SELECT`

![[Pasted image 20250410134532.png]]

### 1. Add new Method to DAO Interface

![[Pasted image 20250410135838.png]]

### 2. Define DAO Implementation

![[Pasted image 20250410135914.png]]

### 3. Update Main App

![[Pasted image 20250410135946.png]]

## Updating Objects with JPA

![[Pasted image 20250410140048.png]]

### Update for All Objects

![[Pasted image 20250410140144.png]]

### 1. Add new Method to DAO Interface

![[Pasted image 20250410143623.png]]

### 2. Define DAO Implementation

![[Pasted image 20250410143719.png]]

### 3. Update Main App

![[Pasted image 20250410143752.png]]

## Deleting Objects with JPA

### Delete an Object

![[Pasted image 20250410144000.png]]

### Delete Based on a Condition

![[Pasted image 20250410144045.png]]

### Delete All

![[Pasted image 20250410144117.png]]

### 1. Add new Method to DAO Interface

![[Pasted image 20250410144149.png]]

### 2. Define DAO Implementation

![[Pasted image 20250410144213.png]]

We add `@Transactional` since we are performing a delete

### 3. Update Main App

![[Pasted image 20250410144304.png]]

## Create Database Tables from Java

![[Pasted image 20250410144358.png]]

### Configuration

![[Pasted image 20250410144429.png]]

![[Pasted image 20250410144750.png]]

Don't use `create` on Production databases as all Production data will be deleted

`create` is useful for small hobby projects

### Create Tables from Code

![[Pasted image 20250410144701.png]]


# REST CRUD APIs

**REST** - **RE**presentationl **S**tate **T**ransfer
- Lightweight communication between application

Most common use of REST is over HTTP

HTTP can be leverage for CRUD operations

![[Pasted image 20250411103722.png]]

## Spring REST Controller

![[Pasted image 20250411104503.png]]

### 1. Add Maven Web Dependency

![[Pasted image 20250411104622.png]]

### 2. Create Service

![[Pasted image 20250411104652.png]]

## Java JSON Data Binding

The process of converting JSON data to a Java POJO

![[Pasted image 20250411120047.png]]

### JSON Data Binding with Jackson

![[Pasted image 20250411120508.png]]

![[Pasted image 20250411120144.png]]

![[Pasted image 20250411120225.png]]

### JSON to Java POJO

![[Pasted image 20250411120346.png]]

### Java POJO to JSON

![[Pasted image 20250411120432.png]]

## Creating Spring REST Service

### Convert Java POJO to JSON

![[Pasted image 20250411120645.png]]

### 1. Create Java POJO Class

![[Pasted image 20250411120940.png]]

### 2. Create `@RestController`

![[Pasted image 20250411121036.png]]

## Spring Boot REST Path Variables

![[Pasted image 20250411121130.png]]

### 1. Add Request Mapping

![[Pasted image 20250411121243.png]]

## Spring Boot REST Exception Handling

### 1. Create Custom Error Response Class

![[Pasted image 20250411143348.png]]

![[Pasted image 20250411143442.png]]

### 2. Create Custom Exception

![[Pasted image 20250411143507.png]]

![[Pasted image 20250411143528.png]]

### 3. Update REST Service to Throw Exception

![[Pasted image 20250411143605.png]]

### 4. Add Exception Handler Method

![[Pasted image 20250411143700.png]]

![[Pasted image 20250411143802.png]]

## Spring Boot REST Global Exception Handling

![[Pasted image 20250411143933.png]]

### `@ControllerAdvice`

![[Pasted image 20250411144020.png]]

### 1. Create new `@ControllerAdvice`

![[Pasted image 20250411144415.png]]

### 2. Remove Exception Handling

![[Pasted image 20250411144446.png]]

### 3. Add Exception Handler to `@ControllerAdvice`

![[Pasted image 20250411144544.png]]

## API Design

![[Pasted image 20250411144734.png]]

### 2. Identify Main Resource/Entity

![[Pasted image 20250411144822.png]]

### 3. Use HTTP Methods to Assign Action on Resource

![[Pasted image 20250411144904.png]]

![[Pasted image 20250411144930.png]]

### Anti-Patterns

![[Pasted image 20250411145014.png]]

## Build a DAO Layer

### DAO Implementation

![[Pasted image 20250414102150.png]]

### Get All

![[Pasted image 20250414102554.png]]

## Service Layer

![[Pasted image 20250414102634.png]]

Provides the controller with a single view of data from multiple backend sources

![[Pasted image 20250414102839.png]]

### `@Service`

1. Define service interface
2. Define service implementation
	- Inject the EmployeeDAO

### 1. Define Service Interface

![[Pasted image 20250414103044.png]]

### 2. Define Service Implementation

![[Pasted image 20250414103118.png]]

## DAO Add, Update, Delete

### Service Layer Transactional Boundaries

![[Pasted image 20250414103455.png]]

### DAO Get Single

![[Pasted image 20250414103543.png]]

### DAO Add or Update

![[Pasted image 20250414103637.png]]

### DAO Delete

![[Pasted image 20250414103705.png]]

## HTTP `PATCH`

Used for a partial update

![[Pasted image 20250414103825.png]]

![[Pasted image 20250414103849.png]]

![[Pasted image 20250414103924.png]]

### 1. Inject Helper Class `ObjectMapper`

![[Pasted image 20250414104019.png]]

![[Pasted image 20250414104042.png]]

### 2. Add Support for `@PatchMapping` Request Method

![[Pasted image 20250414104137.png]]

### 3. Apply Patch Payload

![[Pasted image 20250414104244.png]]

## Spring Data JPA

![[Pasted image 20250414104703.png]]

![[Pasted image 20250414104739.png]]

### 1. Extend `JPARepository` Interface

![[Pasted image 20250414104843.png]]

### 2. Use Repository in your App

![[Pasted image 20250414104929.png]]

## Spring Data REST

![[Pasted image 20250414110226.png]]

![[Pasted image 20250414110252.png]]

![[Pasted image 20250414110321.png]]

### 1. Add Spring Data REST to POM File

![[Pasted image 20250414110406.png]]

![[Pasted image 20250414110427.png]]

### HATEOAS

**H**ypermedia **A**s **T**he **E**ngine **O**f **A**pplication **S**tate

![[Pasted image 20250414110529.png]]

### Config and Sorting

#### Specify Name with Annotation

![[Pasted image 20250414111240.png]]

#### Pagination

![[Pasted image 20250414111315.png]]

#### Configuration

![[Pasted image 20250414111424.png]]

#### Sorting

![[Pasted image 20250414111501.png]]

## REST API Security

### Enabling Spring Security

![[Pasted image 20250414114046.png]]

![[Pasted image 20250414114108.png]]

### Configuration

#### 1. Create Spring Security Configuration

![[Pasted image 20250414115545.png]]

##### Password Storage

![[Pasted image 20250414115630.png]]

#### 2. Add Users, Passwords and Roles

![[Pasted image 20250414115721.png]]

### Restrict URLs Based on Roles

![[Pasted image 20250414155329.png]]

![[Pasted image 20250414155400.png]]

#### Any Role

![[Pasted image 20250414155531.png]]

#### Example

![[Pasted image 20250414155614.png]]

#### CSRF

![[Pasted image 20250414160154.png]]

![[Pasted image 20250414160248.png]]

### JDBC Authentication

![[Pasted image 20250425120039.png]]

#### Default Spring Security Database Schema

![[Pasted image 20250425120340.png]]

#### 1. SQL to Setup Tables

![[Pasted image 20250425120418.png]]

![[Pasted image 20250425120446.png]]

![[Pasted image 20250425120518.png]]

![[Pasted image 20250425120606.png]]

#### 2. Add Database Support to Maven POM File

![[Pasted image 20250425120643.png]]

#### 3. JDBC Properties

![[Pasted image 20250425120724.png]]

#### 4. Update Spring Security to use JDBC

![[Pasted image 20250425120811.png]]

#### BCrypt Encryption

![[Pasted image 20250425121322.png]]

##### Insert Precalculated Password Values

![[Pasted image 20250425121434.png]]

##### Spring Security Login Process

![[Pasted image 20250425121740.png]]

![[Pasted image 20250425133606.png]]

#### Custom Tables

![[Pasted image 20250425134927.png]]

##### 1. Create Custom Tables with SQL

![[Pasted image 20250425135206.png]]

##### 2. Update Spring Security Configuration

![[Pasted image 20250425135258.png]]

# Spring MVC

## Thymeleaf

Java templating engine

Used to generate HTML views for web apps

Thymeleaf is processed on the server

![[Pasted image 20250425135528.png|400]]

### 1. Add Thymeleaf to Maven POM File

![[Pasted image 20250425135630.png]]

### 2. Develop Spring MVC Controller

![[Pasted image 20250425135716.png]]

![[Pasted image 20250425135748.png]]

### 3. Create Thymeleaf Template

![[Pasted image 20250425135838.png]]

### CSS

#### 1. Create CSS File

![[Pasted image 20250425140015.png]]

#### 2. Reference CSS in Thymeleaf Template

![[Pasted image 20250425140051.png]]

#### 3. Apply CSS

![[Pasted image 20250425140116.png]]

#### Remote Bootstrap Reference

![[Pasted image 20250425140216.png]]

## Spring MVC Behind the Scenes

### Components of a Spring MVC Application

![[Pasted image 20250425140558.png]]

![[Pasted image 20250425140654.png]]

### Controller

![[Pasted image 20250425140915.png]]

### Model

![[Pasted image 20250425140948.png]]

### View Template

![[Pasted image 20250425141034.png]]

## Adding Data to MVC Model

![[Pasted image 20250429103236.png]]

## Bind Variable with `@RequestParam`

![[Pasted image 20250429103951.png]]

## Sending Data with `GET`

![[Pasted image 20250429104119.png]]

## Handling Form Submission

![[Pasted image 20250429104211.png]]

### Constrain to `GET`

![[Pasted image 20250429104237.png]]

### Constrain to `POST`

![[Pasted image 20250429104327.png]]

## MVC Form Data Binding

**Data Binding** - Automatically setting/retrieving data from a Java object/bean

![[Pasted image 20250429104542.png]]

![[Pasted image 20250429104716.png]]

### When Form is Loaded

![[Pasted image 20250429105821.png]]

### When Form is Submitted

![[Pasted image 20250429110024.png]]

### Handle Form Submission in Controller

![[Pasted image 20250429110120.png]]

### Radio Buttons - Thymeleaf

![[Pasted image 20250429110418.png]]

### Check Boxes - Thymeleaf

![[Pasted image 20250429110514.png]]

## Validation

### Validation Annotations

![[Pasted image 20250429114331.png]]

### 1. Add Validation Rules

![[Pasted image 20250429114633.png]]

### 2. Controller Code to Show HTML Form

![[Pasted image 20250429114730.png]]

### 3. HTML Form & Add Validation Support

![[Pasted image 20250429114915.png]]

### 4. Perform Validation in Controller

![[Pasted image 20250429115010.png]]

### `@InitBinder`

![[Pasted image 20250429121132.png]]

![[Pasted image 20250429121331.png]]

### Regular Expressions

![[Pasted image 20250429121604.png]]

### Custom Validation

![[Pasted image 20250429151722.png]]

#### 1. Create Annotation

![[Pasted image 20250429151838.png]]

![[Pasted image 20250429152043.png]]

#### Create Validator

![[Pasted image 20250429152214.png]]

# MVC CRUD

![[Pasted image 20250429152517.png]]

## Add Employees

![[Pasted image 20250530143146.png]]

>[!info]
>@ symbol references the application root

With bootstrap styling:

![[Pasted image 20250530143534.png]]

![[Pasted image 20250530143732.png]]

![[Pasted image 20250530144343.png]]

Thymeleaf has special expressions for binding spring MVC form data

![[Pasted image 20250530144650.png]]

### Create HTML form for New Employee

![[Pasted image 20250627145518.png]]

>[!info]
>* {...} selects property on referenced `th:object`

![[Pasted image 20250627145700.png]]

### Process Form Data to Save Employee

![[Pasted image 20250627145816.png]]

## Update Employee

### Update Button

![[Pasted image 20250627145941.png]]

### Pre-populate Form

![[Pasted image 20250627150027.png]]

![[Pasted image 20250627150055.png]]

### Process Form Data to Save Employee

![[Pasted image 20250627152910.png]]

## Delete Employee

### Delete Button

![[Pasted image 20250627153035.png]]

### Controller Code for Delete

![[Pasted image 20250627153112.png]]

# Spring MVC Security

## Spring Security Model

![[Pasted image 20250627153241.png]]

![[Pasted image 20250627153303.png]]

![[Pasted image 20250627153335.png]]

## Declarative Security

![[Pasted image 20250627153500.png]]

## Programmatic Security

![[Pasted image 20250627153535.png]]

## Enabling Spring Security

![[Pasted image 20250627153622.png]]

