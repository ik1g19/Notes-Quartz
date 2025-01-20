>[!INFO]
>Hamcrest is the well-known framework used for unit testing in the Java ecosystem. It’s bundled in JUnit and simply put, it uses existing predicates – called matcher classes – for making assertions

We can use **Hamcrest** with [[notes/Java/Maven|Maven]] by adding the following dependency to our `pom.xml` file:

```xml
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest-all</artifactId>
    <version>1.3</version>
</dependency>
```

## Example Test

Hamcrest is commonly used with junit and other testing frameworks for making assertions

Instead of using junit‘s numerous assert methods, we only use the API’s single `assertThat` statement with appropriate matchers

Let’s look at an example that tests two Strings for equality regardless of case. This should give us a clear idea about how Hamcrest fits in to a testing method:

```java
public class StringMatcherTest {
    
    @Test
    public void given2Strings_whenEqual_thenCorrect() {
        String a = "foo";
        String b = "FOO";
        assertThat(a, equalToIgnoringCase(b));
    }
}
```

## The Object Matcher

Making assertions on arbitrary Java objects

To assert that the `toString` method of an _Object_ returns a specified `String`:

```java
@Test
public void givenBean_whenToStringReturnsRequiredString_thenCorrect(){
    Person person=new Person("Barrack", "Washington");
    String str=person.toString();
    assertThat(person,hasToString(str));
}
```

We can also check that one class is a sub-class of another:

```java
@Test
public void given2Classes_whenOneInheritsFromOther_thenCorrect(){
        assertThat(Cat.class,typeCompatibleWith(Animal.class));
    }
}
```

## Bean Matcher

We can use **Hamcrest**‘s Bean matcher to inspect properties of a Java [[notes/Java/Beans|Bean]].

Assume the following _Person_ bean:

```java
public class Person {
    String name;
    String address;

    public Person(String personName, String personAddress) {
        name = personName;
        address = personAddress;
    }
}
```

We can check if the bean has the property, _name_ like so:

```java
@Test
public void givenBean_whenHasValue_thenCorrect() {
    Person person = new Person("Baeldung", 25);
    assertThat(person, hasProperty("name"));
}
```

We can also check if _Person_ has the _address_ property, initialized to New York:

```java
@Test
public void givenBean_whenHasCorrectValue_thenCorrect() {
    Person person = new Person("Baeldung", "New York");
    assertThat(person, hasProperty("address", equalTo("New York")));
}
```

We can as well check if two _Person_ objects are constructed with the same values:

```java
@Test
public void given2Beans_whenHavingSameValues_thenCorrect() {
    Person person1 = new Person("Baeldung", "New York");
    Person person2 = new Person("Baeldung", "New York");
    assertThat(person1, samePropertyValuesAs(person2));
}
```

## Collection Matcher

**Hamcrest** provides matchers for inspecting Collections

Simple check to find out if a _Collection_ is empty:

```java
@Test
public void givenCollection_whenEmpty_thenCorrect() {
    List<String> emptyList = new ArrayList<>();
    assertThat(emptyList, empty());
}
```

To check the size of a _Collection:_

```java
@Test
public void givenAList_whenChecksSize_thenCorrect() {
    List<String> hamcrestMatchers = Arrays.asList(
      "collections", "beans", "text", "number");
    assertThat(hamcrestMatchers, hasSize(4));
}
```

We can also use it to assert that an array has a required size:

```java
@Test
public void givenArray_whenChecksSize_thenCorrect() {
    String[] hamcrestMatchers = { "collections", "beans", "text", "number" };
    assertThat(hamcrestMatchers, arrayWithSize(4));
}
```

To check if a _Collection_ contains given members, regardless of order:

```java
@Test
public void givenAListAndValues_whenChecksListForGivenValues_thenCorrect() {
    List<String> hamcrestMatchers = Arrays.asList(
      "collections", "beans", "text", "number");
    assertThat(hamcrestMatchers,
    containsInAnyOrder("beans", "text", "collections", "number"));
}
```

To further assert that the _Collection_ members are in given order:

```java
@Test
public void givenAListAndValues_whenChecksListForGivenValuesWithOrder_thenCorrect() {
    List<String> hamcrestMatchers = Arrays.asList(
      "collections", "beans", "text", "number");
    assertThat(hamcrestMatchers,
    contains("collections", "beans", "text", "number"));
}
```

To check if an array has a single given element:

```java
@Test
public void givenArrayAndValue_whenValueFoundInArray_thenCorrect() {
    String[] hamcrestMatchers = { "collections", "beans", "text", "number" };
    assertThat(hamcrestMatchers, hasItemInArray("text"));
}
```

We can also use an alternative matcher for the same test:

```java
@Test
public void givenValueAndArray_whenValueIsOneOfArrayElements_thenCorrect() {
    String[] hamcrestMatchers = { "collections", "beans", "text", "number" };
    assertThat("text", isOneOf(hamcrestMatchers));
}
```

Or still we can do the same with a different matcher like so:

```java
@Test
public void givenValueAndArray_whenValueFoundInArray_thenCorrect() {
    String[] array = new String[] { "collections", "beans", "text",
      "number" };
    assertThat("beans", isIn(array));
}
```

We can also check if the array contains given elements regardless of order:

```java
@Test
public void givenArrayAndValues_whenValuesFoundInArray_thenCorrect() {
    String[] hamcrestMatchers = { "collections", "beans", "text", "number" };
      assertThat(hamcrestMatchers,
    arrayContainingInAnyOrder("beans", "collections", "number",
      "text"));
}
```

To check if the array contains given elements but in the given order:

```java
@Test
public void givenArrayAndValues_whenValuesFoundInArrayInOrder_thenCorrect() {
    String[] hamcrestMatchers = { "collections", "beans", "text", "number" };
    assertThat(hamcrestMatchers,
    arrayContaining("collections", "beans", "text", "number"));
}
```

When our _Collection_ is a _Map,_ we can use the following matchers in these respective functions:

To check if it contains a given key:

```java
@Test
public void givenMapAndKey_whenKeyFoundInMap_thenCorrect() {
    Map<String, String> map = new HashMap<>();
    map.put("blogname", "baeldung");
    assertThat(map, hasKey("blogname"));
}
```

and a given value:

```java
@Test
public void givenMapAndValue_whenValueFoundInMap_thenCorrect() {
    Map<String, String> map = new HashMap<>();
    map.put("blogname", "baeldung");
    assertThat(map, hasValue("baeldung"));
}
```

and finally a given entry (key, value):

```java
@Test
public void givenMapAndEntry_whenEntryFoundInMap_thenCorrect() {
    Map<String, String> map = new HashMap<>();
    map.put("blogname", "baeldung");
    assertThat(map, hasEntry("blogname", "baeldung"));
}
```

## Number Matcher

Used to perform assertions on variables of the _Number_ class

To check _greaterThan_ condition:

```java
@Test
public void givenAnInteger_whenGreaterThan0_thenCorrect() {
    assertThat(1, greaterThan(0));
}
```

To check _greaterThan_ or _equalTo_ condition:

```java
@Test
public void givenAnInteger_whenGreaterThanOrEqTo5_thenCorrect() {
    assertThat(5, greaterThanOrEqualTo(5));
}
```

To check _lessThan_ condition:

```java
@Test
public void givenAnInteger_whenLessThan0_thenCorrect() {
    assertThat(-1, lessThan(0));
}
```

To check _lessThan_ or _equalTo_ condition:

```java
@Test
public void givenAnInteger_whenLessThanOrEqTo5_thenCorrect() {
    assertThat(-1, lessThanOrEqualTo(5));
}
```

To check _closeTo_ condition:

```java
@Test
public void givenADouble_whenCloseTo_thenCorrect() {
    assertThat(1.2, closeTo(1, 0.5));
}
```

## Text Matcher

Assertion on Strings is made easier, neater and more intuitive with **Hamcrest**‘s text matchers

To check if a _String_ is empty:

```java
@Test
public void givenString_whenEmpty_thenCorrect() {
    String str = "";
    assertThat(str, isEmptyString());
}
```

To check if a _String_ is empty or _null_:

```java
@Test
public void givenString_whenEmptyOrNull_thenCorrect() {
    String str = null;
    assertThat(str, isEmptyOrNullString());
}
```

To check for equality of two String while ignoring white space:

```java
@Test
public void given2Strings_whenEqualRegardlessWhiteSpace_thenCorrect() {
    String str1 = "text";
    String str2 = " text ";
    assertThat(str1, equalToIgnoringWhiteSpace(str2));
}
```

We can also check for the presence of one or more sub-strings in a given _String_ in a given order:

```java
@Test
public void givenString_whenContainsGivenSubstring_thenCorrect() {
    String str = "calligraphy";
    assertThat(str, stringContainsInOrder(Arrays.asList("call", "graph")));
}
```

Finally, we can check for equality of two String regardless of case:

```java
@Test
 public void given2Strings_whenEqual_thenCorrect() {
    String a = "foo";
    String b = "FOO";
    assertThat(a, equalToIgnoringCase(b));
}
```

## Core API

Readability with the _is_ construct on a matcher:

```java
@Test
public void given2Strings_whenIsEqualRegardlessWhiteSpace_thenCorrect() {
    String str1 = "text";
    String str2 = " text ";
    assertThat(str1, is(equalToIgnoringWhiteSpace(str2)));
}
```

The _is_ construct on a simple data type:

```java
@Test
public void given2Strings_whenIsEqual_thenCorrect() {
    String str1 = "text";
    String str2 = "text";
    assertThat(str1, is(str2));
}
```

Negation with the _not_ construct on a matcher:

```java
@Test
public void given2Strings_whenIsNotEqualRegardlessWhiteSpace_thenCorrect() {
    String str1 = "text";
    String str2 = " texts ";
    assertThat(str1, not(equalToIgnoringWhiteSpace(str2)));
}
```

The _not_ construct on a simple data type:

```java
@Test
public void given2Strings_whenNotEqual_thenCorrect() {
    String str1 = "text";
    String str2 = "texts";
    assertThat(str1, not(str2));
}
```

Check if a _String_ contains a given sub-string:

```java
@Test
public void givenAStrings_whenContainsAnotherGivenString_thenCorrect() {
    String str1 = "calligraphy";
    String str2 = "call";
    assertThat(str1, containsString(str2));
}
```

Check if a _String_ starts with given sub-string:

```java
@Test
public void givenAString_whenStartsWithAnotherGivenString_thenCorrect() {
    String str1 = "calligraphy";
    String str2 = "call";
    assertThat(str1, startsWith(str2));
}
```

Check if a _String_ ends with given sub-string:

```java
@Test
public void givenAString_whenEndsWithAnotherGivenString_thenCorrect() {
    String str1 = "calligraphy";
    String str2 = "phy";
    assertThat(str1, endsWith(str2));
}
```

Check if two _Object_ are of the same instance:

```java
@Test
public void given2Objects_whenSameInstance_thenCorrect() {
    Cat cat=new Cat();
    assertThat(cat, sameInstance(cat));
}
```

Check if an _Object_ is an instance of a given class:

```java
@Test
public void givenAnObject_whenInstanceOfGivenClass_thenCorrect() {
    Cat cat=new Cat();
    assertThat(cat, instanceOf(Cat.class));
}
```

Check if all members of a _Collection_ meet a condition:

```java
@Test
public void givenList_whenEachElementGreaterThan0_thenCorrect() {
    List<Integer> list = Arrays.asList(1, 2, 3);
    int baseCase = 0;
    assertThat(list, everyItem(greaterThan(baseCase)));
}
```

Check that a _String_ is not _null_:

```java
@Test
public void givenString_whenNotNull_thenCorrect() {
    String str = "notnull";
    assertThat(str, notNullValue());
}
```

Chain conditions together, test passes when target meets any of the conditions, similar to logical OR:

```java
@Test
public void givenString_whenMeetsAnyOfGivenConditions_thenCorrect() {
    String str = "calligraphy";
    String start = "call";
    String end = "foo";
    assertThat(str, anyOf(startsWith(start), containsString(end)));
}
```

Chain conditions together, test passes only when target meets all conditions, similar to logical AND:

```java
@Test
public void givenString_whenMeetsAllOfGivenConditions_thenCorrect() {
    String str = "calligraphy";
    String start = "call";
    String end = "phy";
    assertThat(str, allOf(startsWith(start), endsWith(end)));
}
```

## Custom Matcher

We can define our own matcher by extending _TypeSafeMatcher_. In this section, we will create a custom matcher which allows a test to pass only when the target is a positive integer.

```java
public class IsPositiveInteger extends TypeSafeMatcher<Integer> {

    public void describeTo(Description description) {
        description.appendText("a positive integer");
    }

    @Factory
    public static Matcher<Integer> isAPositiveInteger() {
        return new IsPositiveInteger();
    }

    @Override
    protected boolean matchesSafely(Integer integer) {
        return integer > 0;
    }

}
```

We need only to implement the _matchSafely_ method which checks that the target is indeed a positive integer and the _describeTo_ method which produces a failure message in case the test does not pass.

Here is a test that uses our new custom matcher:

```java
@Test
public void givenInteger_whenAPositiveValue_thenCorrect() {
    int num = 1;
    assertThat(num, isAPositiveInteger());
}
```

and here is a failure message we get since we have passed in a non-positive integer:

```java
java.lang.AssertionError: Expected: a positive integer but: was <-1>
```

