#java 

---

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherExample {

    public static void main(String[] args) {

        String text    =
            "This is the text to be searched " +
            "for occurrences of the http:// pattern.";

        String patternString = ".*http://.*";

        Pattern pattern = Pattern.compile(patternString);

        Matcher matcher = pattern.matcher(text);
        boolean matches = matcher.matches();
    }
}
```

First a `Pattern` instance is created from a regular expression, and from the `Pattern` instance a `Matcher` instance is created. Then the `matches()` method is called on the `Matcher` instance. The `matches()` returns `true` if the regular expression matches the text, and `false` if not

Creating a `Matcher` is done via the `matcher()` method in the `Pattern` class

# `matches()`

The `matches()` method in the `Matcher` class matches the regular expression against the whole text passed to the `Pattern.matcher()` method, when the `Matcher` was created

```java
String patternString = ".*http://.*";
Pattern pattern = Pattern.compile(patternString);

boolean matches = matcher.matches();
```

If the regular expression matches the whole text, then the `matches()` method returns true. If not, the `matches()` method returns false

You cannot use the `matches()` method to search for multiple occurrences of a regular expression in a text. For that, you need to use the `find()`, `start()` and `end()` methods

# `lookingAt()`

The `Matcher` `lookingAt()` method works like the `matches()` method with one major difference. The `lookingAt()` method only matches the regular expression against the beginning of the text, whereas `matches()` matches the regular expression against the whole text. In other words, if the regular expression matches the beginning of a text but not the whole text, `lookingAt()` will return true, whereas `matches()` will return false.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class CreateMatcherExample {

    public static void main(String[] args) {

        String text    =
                "This is the text to be searched " +
                "for occurrences of the http:// pattern.";

        String patternString = "This is the";

        Pattern pattern = Pattern.compile(patternString, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(text);

        System.out.println("lookingAt = " + matcher.lookingAt());
        System.out.println("matches   = " + matcher.matches());
    }
}
```

This example matches the regular expression `"this is the"` against both the beginning of the text, and against the whole text. Matching the regular expression against the beginning of the text (`lookingAt()`) will return true

Matching the regular expression against the whole text (`matches()`) will return false, because the text has more characters than the regular expression. The regular expression says that the text must match the text `"This is the"` exactly, with no extra characters before or after the expression

# `find() + start() + end()`

The `Matcher` `find()` method searches for occurrences of the regular expressions in the text passed to the `Pattern.matcher(text)` method, when the `Matcher` was created. If multiple matches can be found in the text, the `find()` method will find the first, and then for each subsequent call to `find()` it will move to the next match

The methods `start()` and `end()` will give the indexes into the text where the found match starts and ends. Actually `end()` returns the index of the character _just after_ the end of the matching section. Thus, you can use the return values of `start()` and `end()` inside a `String.substring()` call

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherFindStartEndExample {

    public static void main(String[] args) {

        String text    =
                "This is the text which is to be searched " +
                "for occurrences of the word 'is'.";

        String patternString = "is";

        Pattern pattern = Pattern.compile(patternString);
        Matcher matcher = pattern.matcher(text);

        int count = 0;
        while(matcher.find()) {
            count++;
            System.out.println("found: " + count + " : "
                    + matcher.start() + " - " + matcher.end());
        }
    }
}
```

This example will find the pattern "is" four times in the searched string. The output printed will be this:

```
found: 1 : 2 - 4
found: 2 : 5 - 7
found: 3 : 23 - 25
found: 4 : 70 - 72
```

# `group()`

You access a group using the `group(int groupNo)` method. A regular expression can have more than one group. Each group is thus marked with a separate set of parentheses. To get access to the text that matched the subpart of the expression in a specific group, pass the number of the group to the `group(int groupNo)` method

The group with number 0 is always the whole regular expression. To get access to a group marked by parentheses you should start with group numbers 1

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherGroupExample {

    public static void main(String[] args) {

        String text    =
                  "John writes about this, and John writes about that," +
                          " and John writes about everything. "
                ;

        String patternString1 = "(John)";

        Pattern pattern = Pattern.compile(patternString1);
        Matcher matcher = pattern.matcher(text);

        while(matcher.find()) {
            System.out.println("found: " + matcher.group(1));
        }
    }
}
```

This example searches the text for occurrences of the word `John`. For each match found, group number 1 is extracted, which is what matched the group marked with parentheses

The output of the example is:

```
found: John
found: John
found: John
```

# Multiple Groups

```
(John) (.+?)
```

This expression matches the text `"John"` followed by a space, and then one or more characters. You cannot see it in the example above, but there is a space after the last group too

This expression contains a few characters with special meanings in a regular expression. The . means "any character". The + means "one or more times", and relates to the . (any character, one or more times). The ? means "match as small a number of characters as possible"

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherGroupExample {

    public static void main(String[] args) {

        String text    =
                  "John writes about this, and John Doe writes about that," +
                          " and John Wayne writes about everything."
                ;

        String patternString1 = "(John) (.+?) ";

        Pattern pattern = Pattern.compile(patternString1);
        Matcher matcher = pattern.matcher(text);

        while(matcher.find()) {
            System.out.println("found: " + **matcher.group(1)** +
                               " "       + **matcher.group(2))**;
        }
    }
}
```

Notice the reference to the two groups, marked in bold. The characters matched by those groups are printed to `System.out`. Here is what the example prints out:

```
found: John writes
found: John Doe
found: John Wayne
```

# `replaceAll() + replaceFirst()`

The `Matcher` `replaceAll()` and `replaceFirst()` methods can be used to replace parts of the string the `Matcher` is searching through. The `replaceAll()` method replaces all matches of the regular expression. The `replaceFirst()` only replaces the first match

Before any matching is carried out, the `Matcher` is reset, so that matching starts from the beginning of the input text

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherReplaceExample {

    public static void main(String[] args) {

        String text    =
                  "John writes about this, and John Doe writes about that," +
                          " and John Wayne writes about everything."
                ;

        String patternString1 = "((John) (.+?)) ";

        Pattern pattern = Pattern.compile(patternString1);
        Matcher matcher = pattern.matcher(text);

        String replaceAll = matcher.replaceAll("Joe Blocks ");
        System.out.println("replaceAll   = " + replaceAll);

        String replaceFirst = matcher.replaceFirst("Joe Blocks ");
        System.out.println("replaceFirst = " + replaceFirst);
    }
}
```

And here is what the example outputs:

```
replaceAll   = Joe Blocks about this, and Joe Blocks writes about that,
    and Joe Blocks writes about everything.
replaceFirst = Joe Blocks about this, and John Doe writes about that,
    and John Wayne writes about everything.
```

Notice how the first string printed has all occurrences of `John` with a word after, replaced with the string `Joe Blocks`. The second string only has the first occurrence replaced