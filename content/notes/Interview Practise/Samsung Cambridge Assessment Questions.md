Given a list of four "(x y)"s, calculate the area of the rectangle

```java
import java.util.*; 
import java.io.*;
import java.util.regex.*;

class Main {

  public static String ArrayChallenge(String[] strArr) {

    //regex for matching input strings
    Pattern p = Pattern.compile("\\((\\d*)\\s(\\d*)\\)");

    int max_x = 0;
    int min_x = 0;
    int max_y = 0;
    int min_y = 0;


    for (int i=0;i<strArr.length;i++) {
      String str = strArr[i];
      Matcher m = p.matcher(str);
      m.matches();

      int x = Integer.parseInt(m.group(1));
      int y = Integer.parseInt(m.group(2));
      
      if (i == 0) {min_x = x; max_x = x; min_y = y; max_y = y;}

      else {
        if (x < min_x) {min_x = x;}
        if (x > max_x) {max_x = x;}
        if (y < min_y) {min_y = y;}
        if (y > max_y) {max_y = y;}
      }
    }
    
    int dx = max_x - min_x;
    int dy = max_y - min_y;

    return Integer.toString(dx*dy);
  }

  public static void main (String[] args) {  
    // keep this function call here     
    Scanner s = new Scanner(System.in);
    System.out.print(ArrayChallenge(s.nextLine())); 
  }

}
```

Improvements

- Uses Matcher.matches to verify the input is the correct format and throw an error if not
- Could have used Integer.minValue and maxValue to help find min and max x and y
	- Then can remove the `i == 0` conditional
- 


Make sure the string doesn't contain "password", is between 7 and 31 chars long, contains at least one digit, has a ! or mathematical symbol

```java
import java.util.*; 
import java.io.*;

class Main {

  public static String StringChallenge(String str) {
    //invalid if contains 'password'
    if (str.contains("password")) {return "false";}
    //only valid between 7 and 31 chars
    if (str.length() > 31 || str.length() < 7) {return "false";}
    //invalid if contains no digits
    if (!str.matches(".*\\d.*")) {return "false";}
    //invalid if no ! and no mathematical symbol
    if (!str.contains("!") && !str.matches(".*[\\+\\-=/\\*].*")) {return "false";}

    //otherwise valid
    return "true";
  }

  public static void main (String[] args) {  
    // keep this function call here     
    Scanner s = new Scanner(System.in);
    System.out.print(StringChallenge(s.nextLine())); 
  }

}
```