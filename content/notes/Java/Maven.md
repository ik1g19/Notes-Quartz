>[!INFO]
>Maven is a popular build automation tool used in Java development to manage project dependencies and build configurations

- `pom.xml` stands for **Project Object Model** file.
- It is the core file in a Maven project that defines the project structure, dependencies, and other build-related configurations

# Recommended Maven Archetypes

## `maven-archetype-quickstart` (Most Common for Simple Java Applications)

Description: This is a basic Maven archetype for starting a simple Java project. It generates:
- A basic directory structure (`src/main/java` and `src/test/java`).
- A sample App class and a corresponding unit test
	
Use Case: Ideal for small projects and learning Maven, such as experimenting with Hamcrest

How to Find It:
- In IntelliJ, search for `maven-archetype-quickstart`
- Typically has the coordinates:

```xml
<groupId>org.apache.maven.archetypes</groupId>
<artifactId>maven-archetype-quickstart</artifactId>
<version>1.4</version>
```

## `maven-archetype-webapp` (For Web Projects)
Description: Creates a basic structure for a Java web application

Use Case: Choose this if your project involves developing web applications and you want to experiment with servlets, JSP, or other web-related functionality

Generated Structure:
	src/main/webapp/ for web resources (HTML, JSP, etc.).
	Includes a web.xml file for web configuration.

## `maven-archetype-simple` (Minimalist Option)

Description: This archetype generates a very barebones Maven project with just the essential pom.xml and no pre-generated code

Use Case: If you want full control over the structure or are following a tutorial that builds everything from scratch

## `maven-archetype-junit` (For Projects Focused on Testing)

Description: Creates a project that is pre-configured for testing with JUnit

Use Case: If you’re focusing heavily on learning Hamcrest and writing unit tests, this archetype might save you some setup