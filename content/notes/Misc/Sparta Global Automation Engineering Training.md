# Agile

![[Images/Pasted image 20241213142949.png]]

![[Images/Pasted image 20241213143153.png]]

![[Images/Pasted image 20241217155052.png]]
![[Images/Pasted image 20241218120308.png]]

Being unwilling to compromise and refusing to acknowledge technical limitations is indicative of an Opponent attitude

a Blocker would be indicated by someone hindering a project (for example withholding resources) either intentionally or unintentionally

![[Images/Pasted image 20241218120454.png]]

![[Images/Pasted image 20241219105604.png]]

1. Frequent communication with the Product Owner
2. Transparency pillar

![[Images/Pasted image 20241219111422.png]]

![[Images/Pasted image 20241219111722.png]]
![[Images/Pasted image 20241219111953.png]]

![[Images/Pasted image 20241219114535.png]]
![[Images/Pasted image 20241219114938.png]]![[Images/Pasted image 20241219115238.png]]

![[Images/Pasted image 20241219120215.png]]
![[Images/Pasted image 20241219121137.png]]
![[Images/Pasted image 20241219122023.png]]

![[Images/Pasted image 20241219122049.png]]![[Images/Pasted image 20241219122244.png]]

![[Images/Pasted image 20241219135715.png]]

![[Images/Pasted image 20241219140146.png]]

![[Images/Pasted image 20241219142826.png]]

![[Images/Pasted image 20241219142908.png]]
![[Images/Pasted image 20241219143132.png]]

![[Images/Pasted image 20241219144321.png]]

![[Images/Pasted image 20241219144634.png]]

![[Images/Pasted image 20241219144821.png]]

![[Images/Pasted image 20241219145137.png]]

![[Images/Pasted image 20241219145149.png]]


![[Images/Pasted image 20241219145412.png]]

![[Images/Pasted image 20241219150046.png]]

![[Images/Pasted image 20241219151046.png]]

![[Images/Pasted image 20241219151129.png]]

The three amigos:
- Testers
- Developers
- Business

# Testing

## Seven Testing Principles

1. **Testing shows the presence of defects, not their absence**  
    Testing can show that defects are present, but cannot prove that there are no defects. Testing reduces the probability of undiscovered defects remaining in the software but, even if no defects are found, testing is not a proof of correctness.
2. **Exhaustive testing is impossible**  
    Testing everything (all combinations of inputs and preconditions) is not feasible except for trivial cases. Rather than attempting to test exhaustively, risk analysis, test techniques, and priorities should be used to focus test efforts.
3. **Early testing saves time and money**  
    To find defects early, both static and dynamic test activities should be started as early as possible in the software development lifecycle. Early testing is sometimes referred to as shift left. Testing early in the software development lifecycle helps reduce or eliminate costly changes (see section 3.1).
4. **Defects cluster together**  
    A small number of modules usually contains most of the defects discovered during pre-release testing or is responsible for most of the operational failures. Predicted defect clusters, and the actual observed defect clusters in test or operation, are important input into a risk analysis used to focus the test effort (as mentioned in principle 2).
5. **Beware of the pesticide paradox**  
    If the same tests are repeated over and over again, eventually these tests no longer find any new defects. To detect new defects, existing tests and test data may need changing, and new tests may need to be written. (Tests are no longer effective at finding defects, just as pesticides are no longer effective at killing insects after a while.) In some cases, such as automated regression testing, the pesticide paradox has a beneficial outcome, which is the relatively low number of regression defects.
6. **Testing is context-dependent**  
    Testing is done differently in different contexts. For example, safety-critical industrial control software is tested differently from an e-commerce mobile app. As another example, testing in an Agile project is done differently than testing in a sequential software development lifecycle project (see section 2.1).
7. **Absence-of-errors is a fallacy**  
    Some organizations expect that testers can run all possible tests and find all possible defects, but principles 2 and 1, respectively, tell us that this is impossible. Further, it is a fallacy (i.e., a mistaken belief) to expect that just finding and fixing a large number of defects will ensure the success of a system. For example, thoroughly testing all specified requirements and fixing all defects found could still produce a system that is difficult to use, that does not fulfil the users’ needs and expectations, or that is inferior compared to other competing systems.

**Fragmentation** - The inability to write once and run anywhere

## Agile Test Quadrants

![[Images/Pasted image 20250106134755.png]]

## Test Pyramid

![[Images/Pasted image 20250106135306.png]]

Choose a website and use the Chrome Dev tool to emulate its behaviour on different devices..

Record any defects you find in a spreadsheet with columns titled:

- Unique identifier
- Title
- Emulated device type
- Device dimensions
- Description of the defect
- Severity of the defect

## Visual Testing

![[Images/Pasted image 20250106144550.png]]

![[Images/Pasted image 20250106144648.png]]

## Exploratory Testing

![[Images/Pasted image 20250106150951.png]]

![[Images/Pasted image 20250106151600.png]]

![[Images/Pasted image 20250106152825.png]]

![[Images/Pasted image 20250106152854.png]]

![[Images/Pasted image 20250106152940.png]]

![[Images/Pasted image 20250106153145.png]]

## Charters

![[Images/Pasted image 20250106153635.png|400]]

![[Images/Pasted image 20250106153922.png]]

# Defect Management

## What is a Defect

![[Images/Pasted image 20250106154558.png]]

## Defect Lifecycle

![[Images/Pasted image 20250106154919.png]]

## Defect Severity Classification

![[Images/Pasted image 20250106155549.png]]

## Defect Priority

![[Images/Pasted image 20250106155643.png]]

## Severity-Priority Matrix

![[Images/Pasted image 20250106155742.png]]


**Dynamic Testing** - Testing running code
- e.g. add something to the shopping basket and see if the shopping cart graphic updates
**Static Testing** - Reading code
- e.g. Peer code review

## Defect Report

![[Images/Pasted image 20250107101316.png]]


Traceability - The degree to which a relationship can be established between two or more work products

![[Images/Pasted image 20250107101951.png]]

## Traceability Matrix

![[Images/Pasted image 20250107102045.png]]

![[Images/Pasted image 20250107102312.png]]

## Defect Management Committee

![[Images/Pasted image 20250107102522.png]]

![[Images/Pasted image 20250107102623.png]]

![[Images/Pasted image 20250107102746.png]]

# Usability Testing

## Usability

![[Images/Pasted image 20250107104920.png|400]]

![[Images/Pasted image 20250107105417.png|400]]

## User Experience

![[Images/Pasted image 20250107104952.png|400]]

![[Images/Pasted image 20250107111030.png]]

## Usability Testing

![[Images/Pasted image 20250107121556.png]]

## Representative Users

![[Images/Pasted image 20250107121829.png]]

## Usability Testing Methods

![[Images/Pasted image 20250107122007.png]]

![[Images/Pasted image 20250107122228.png]]

![[Images/Pasted image 20250107122422.png]]

# Accessibility Testing

[🔗Web Accessibility Evaluation](https://wave.webaim.org/)

![[Images/Pasted image 20250107143209.png]]

## WCAG

WCAG are standards
- WAI-ARIA are technical features to support WCAG
- BS 8878 is the British version

![[Images/Pasted image 20250107143718.png]]

## Principles of Accessibility

![[Images/Pasted image 20250107143930.png]]

![[Images/Pasted image 20250107144203.png]]

![[Images/Pasted image 20250107144211.png]]

![[Images/Pasted image 20250107144343.png]]

![[Images/Pasted image 20250107144606.png]]

## WCAG Conference Levels

![[Images/Pasted image 20250107144722.png]]

![[Images/Pasted image 20250107144938.png]]

## Tools to Assess Accessibility

[🔗Validator](https://validator.w3.org/)

[🔗Jigsaw](https://jigsaw.w3.org/css-validator/)

[🔗Link Checker](https://validator.w3.org/checklink?uri=)

[🔗ColorBlindly](https://chromewebstore.google.com/detail/colorblindly/floniaahmccleoclneebhhmnjgdfijgg?hl=en)

[🔗ScreenReader](https://chromewebstore.google.com/detail/screen-reader/kgejglhpjiefppelpmljglcjbhoiplfn)

## Accessibility Testing Importance

![[Images/Pasted image 20250107145559.png]]

# Acceptance Testing

![[Images/Pasted image 20250107150811.png|400]]

![[Images/Pasted image 20250107150842.png]]

## Types of Acceptance Testing

![[Images/Pasted image 20250107151001.png]]

## Alpha and Beta Testing

![[Images/Pasted image 20250107151102.png]]

## User Acceptance Testing

![[Images/Pasted image 20250107151245.png]]

![[Images/Pasted image 20250107151423.png]]

![[Images/Pasted image 20250107151616.png]]

## Operational Acceptance Testing

![[Images/Pasted image 20250107151718.png]]

![[Images/Pasted image 20250107151825.png]]

## Regulation Acceptance Testing

![[Images/Pasted image 20250107152011.png]]

![[Images/Pasted image 20250107152255.png]]

![[Images/Pasted image 20250107152438.png]]

## Contract Acceptance Testing

![[Images/Pasted image 20250107152523.png]]

![[Images/Pasted image 20250107152825.png]]

## A/B Testing

![[Images/Pasted image 20250107153120.png]]

# Testing Practises

## Testing and Quality Assurance

![[Images/Pasted image 20250108101816.png]]

## Test Activities, Testware and Test Role Definitions

![[Images/Pasted image 20250108102345.png]]

## Test Activities

![[Images/Pasted image 20250108102839.png]]

![[Images/Pasted image 20250108103036.png]]
## Testware

![[Images/Pasted image 20250108103221.png]]

## Roles in Testing

![[Images/Pasted image 20250108103503.png]]

![[Images/Pasted image 20250108104208.png]]

![[Images/Pasted image 20250108104233.png]]

## Maintenance Testing

![[Images/Pasted image 20250108104508.png]]

![[Images/Pasted image 20250108104701.png|300]]

## Black Box Techniques

![[Images/Pasted image 20250108105045.png]]

## White Box Techniques

![[Images/Pasted image 20250108105822.png]]

## Experience-Based Techniques

![[Images/Pasted image 20250108110039.png]]

![[Images/Pasted image 20250108110121.png]]

## Checklist-based Testing

![[Images/Pasted image 20250108110302.png]]

# Performance Testing

![[Images/Pasted image 20250108112258.png]]

## Factors Affecting Performance

- Page Weight

![[Images/Pasted image 20250108121120.png]]

- Minification

[🔗JS/CSS](https://www.minifier.org/)

[🔗HTML](http://minifycode.com/html-minifier/)

![[Images/Pasted image 20250108121313.png|400]]

- GZipping

Removing repeated strings - compression

![[Images/Pasted image 20250108121720.png]]

- Number of HTTP Requests

![[Images/Pasted image 20250108121929.png|400]]

Reduce with in-document styles and script concatenation

![[Images/Pasted image 20250108122011.png|400]]

![[Images/Pasted image 20250108122111.png|400]]

- Caching

Can be within a proxy server or the client computer

![[Images/Pasted image 20250108122510.png|500]]

# Performance Testing

![[Images/Pasted image 20250108133740.png]]

## Performance Testing Types

![[Images/Pasted image 20250108133955.png]]

## Load/Capacity Testing

![[Images/Pasted image 20250108134942.png]]

## Stress Testing

![[Images/Pasted image 20250108135042.png]]

How to create Load Tests using KPIs

+10% is the minimum acceptable load

![[Images/Pasted image 20250108135453.png|400]]

![[Images/Pasted image 20250108135555.png]]

![[Images/Pasted image 20250108135701.png]]

![[Images/Pasted image 20250108135836.png]]

![[Images/Pasted image 20250108135909.png]]

![[Images/Pasted image 20250108140005.png]]

![[Images/Pasted image 20250108140142.png]]

[JMeter Tutorial](https://www.youtube.com/watch?v=SoW2pBak1_Q)

# Test Driven Development

Writing tests first

[Best Practises](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)

## Characteristics of a good unit test

- **Fast**: It isn't uncommon for mature projects to have thousands of unit tests. Unit tests should take little time to run. Milliseconds.
- **Isolated**: Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
- **Repeatable**: Running a unit test should be consistent with its results, that is, it always returns the same result if you don't change anything in between runs.
- **Self-Checking**: The test should be able to automatically detect if it passed or failed without any human interaction.
- **Timely**: A unit test shouldn't take a disproportionately long time to write compared to the code being tested. If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable

## JUnit

| Annotation     | Description                              |
| -------------- | ---------------------------------------- |
| `@BeforeAll`   | Run before all unit tests. Static method |
| `@BeforeEach`  | Run before each unit test                |
| `@AfterAll`    | Run after all unit tests. Static method  |
| `@AfterEach`   | Run after each unit tests                |
| `@DisplayName` | Test display name                        |
| `@ValueSource` | Values for parameterized test            |

- `BeforeAll`s ran
- Test class is instantiated for each test
- `BeforeEach`s ran
- Tests ran
- `AfterEach`s ran
- `AfterAll`s ran
# Test Automation Pyramid

![[Images/Pasted image 20250113140223.png]]

# Selenium

![[Images/Pasted image 20250113141642.png|400]]

Record manual tests on websites

You can export recordings to JUnit

# BDD

![[Images/Pasted image 20250113142608.png]]

![[Images/Pasted image 20250113142807.png]]

Given - Pre-condition
When - The trigger

![[Images/Pasted image 20250113142840.png]]

![[Images/Pasted image 20250114115411.png]]

### **Page Object Model (POM)**

- **Definition**: POM is a design pattern commonly used in automated UI testing, especially in frameworks like Selenium. It represents a web page as a class, where the elements on the page are treated as objects
    
- **Purpose**: To improve test code organization, maintainability, and readability
    
- **Structure**:
    
    - Each web page in the application is represented by a separate class
    - The class contains locators for web elements and methods to perform actions on those elements (e.g., click, input text)

### **Document Object Model (DOM)**

- **Definition**: The DOM is a programming interface for HTML and XML documents. It represents the structure of a web page as a tree of objects, where each node is an element or a piece of data
    
- **Purpose**: To allow scripts (like JavaScript) to dynamically access and manipulate the content, structure, and styles of a webpage
    
- **Structure**:
    
    - The DOM is hierarchical, starting from the root `<html>` element
    - Nodes represent elements (e.g., `<div>`, `<p>`), attributes, and text

# Difference between Hamcrest and JUnit

More readable interface for Matchers

JUnit - Assert
Hamcrest - Matchers

# Mockito/Mocking

| Test Double | Included Here | Description                                                                                                                                                                                                                                                                                                                               |
| ----------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fake        | No            | A working implementation, suitable for testing but not for a production environment - think of an in-memory database substituted for a production database                                                                                                                                                                                |
| Dummy       | Yes           | An object just used to pass as a value - think about our initial use of `mock1`/`mock2` to populate the `ArrayList` in `SpartanRepository`                                                                                                                                                                                                |
| Stub        | Yes           | Objects with pre-defined responses to calls on their methods - where we needed our `mock1`/`mock2` objects to respond in a certain way                                                                                                                                                                                                    |
| Spy         | Yes           | Stubs that keep a record of how they were called - where we wanted to verify code behaviour, for example, how many times a method was called - with Mockito, you can also 'spy' on a real object (`Mockito.spy(sut)') [https://www.baeldung.com/mockito-spy](https://www.baeldung.com/mockito-spy "https://www.baeldung.com/mockito-spy") |
| Mock        | Yes           | Where a mocked object throws an exception if they don't receive all of the calls they expect, or if they receive an unexpected call - think about the extended checking for expected parameter example                                                                                                                                    |

# API Testing

## Definition

![[Images/Pasted image 20250120135024.png|400]]

## Why API Testing

![[Images/Pasted image 20250120135129.png]]

![[Images/Pasted image 20250120135159.png]]

## Sources for API Test Generation

![[Images/Pasted image 20250120135221.png]]

## What to Test

![[Images/Pasted image 20250120135244.png]]

## API Test Scenarios

![[Images/Pasted image 20250120135304.png]]

## Creating API Test Cases with Gherkin

![[Images/Pasted image 20250120135338.png]]

![[Images/Pasted image 20250120135358.png]]

![[Images/Pasted image 20250120135433.png]]